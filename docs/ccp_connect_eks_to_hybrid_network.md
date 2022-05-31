# Connect AWS EKS Kubernetes Cluster to Hybrid Network

After successfully created EKS cluster, now it is a time to connect it to VPN connection towards On-Premise Data Center.
CCP created dedicated VPC for every Kubernetes EKS Cluster. You can now start working on it and deploying applicaitons, however your services and applications will be exposed to public Internet. In our scenario, we will be deploying backend part of our application in EKS cluster that needs to have connectivity to database that you will deploy on-premise.

In order to provider secure connectivity between application components, we would need to establish IPSec Tunnel between AWS and on-premise data center.

<img src="https://raw.githubusercontent.com/marcinduma/HOLCLD-2101/master/images/vpn-basic-diagram.png">

The VPC has an attached virtual private gateway, and your on-premises (remote) network includes a customer gateway device, which you must configure to enable the Site-to-Site VPN connection. You set up the routing so that any traffic from the VPC bound for your network is routed to the virtual private gateway.
Site-to-Site VPN is used to build eBGP connection between Amazon and on-prem router to exchange networks used for Kubernetes services in secured manner.

This solution is well described in the following white paper:

<a href="https://docs.aws.amazon.com/vpn/latest/s2svpn/VPC_VPN.html" target="_blank">https://docs.aws.amazon.com/vpn/latest/s2svpn/VPC_VPN.html</a>

In our excercise you will need to:

- Define Virtual Private Gateway
- Bound it with VPC created by CCP
- Create Site-to-Site Tunnel
- Paste configuration to your on-prem CSR1000v - configuration will be provided by AWS

## Create AWS VPN Gateway 

- **Step 1.** Open AWS dashboard, and select VPC service, as on the following picture:

<img src="https://raw.githubusercontent.com/marcinduma/HOLCLD-2101/master/images/aws-vpc-enter.png">

Next check the VPC has been created with the name you have provided in CCP (aws-student-XX). 

!!! info
    Make sure your AWS web console is set to use Frankfurt (eu-central-1) region.

<img src="https://raw.githubusercontent.com/marcinduma/HOLCLD-2101/master/images/aws-vpc-find.png">

- **Step 2.** Create new Virtual Private Gateway

From the left menu, scrol down and select Virtual Private Gateways

<img src="https://raw.githubusercontent.com/marcinduma/HOLCLD-2101/master/images/aws-vpc-vgw-enter.png">

Press button *Create Virtual Private Gateway*

Enter your username as a name of Virtual Private Gateway (studentXX) and leave *default ASN* selected (autonomous system number for BGP).

<img src="https://raw.githubusercontent.com/marcinduma/HOLCLD-2101/master/images/aws-vgw-creating.png">

Once create successfully you should see similar screen

<img src="https://raw.githubusercontent.com/marcinduma/HOLCLD-2101/master/images/aws-vgw-created.png">

- **Step 3.** Attach Virtual Private Gateway to your VPC. Select your newely created Gateway and click on *Actions* menu. Select *attach to VPC* option.

<img src="https://raw.githubusercontent.com/marcinduma/HOLCLD-2101/master/images/aws-vgw-attaching.png">

In the new window select your VPC to which Virtual Private Gateway will be attached.

<img src="https://raw.githubusercontent.com/marcinduma/HOLCLD-2101/master/images/aws-vgw-attaching-to-vpc.png">

You can see *attaching* status, you can refresh page by clicking refresh button in the right top corner, the status should change to *attached* for your Virtual Private Gateway.

<img src="https://raw.githubusercontent.com/marcinduma/HOLCLD-2101/master/images/aws-vgw-attached.png">

## Create Site-to-Site VPN Connection

Select *Site-to-Site VPN Connections* section from left navigation panel. Click on **Create VPN Connection** as shown on figure below.

<img src="https://raw.githubusercontent.com/marcinduma/HOLCLD-2101/master/images/aws-l2l-create.png">

New configuration wizard will open in the browser. Configure your new VPN Tunnel as follows.

1. Name tag, use **studentID** i.e. student01.

2. In Virtual Private Gateway select previously created VGW, search for *studentXX*.

3. Next, select *Customer Gateway ID*. From drop down menu select **cgw-lon-dcloud**.

<img src="https://raw.githubusercontent.com/marcinduma/HOLCLD-2101/master/images/aws-l2l.png">

Leave rest of the Site-2-Site VPN attributes unchanged. Scroll down to the bottom of the screen and click ** Create VPN Connection**.

!!! info
    Creation time for site-to-site VPN may take several minutes, use refresh button to check if state has changed.

Once completed, select your newly created Site-2-Site VPN from the list. Once done click on button above **Download Configuration**.

<img src="https://raw.githubusercontent.com/marcinduma/HOLCLD-2101/master/images/aws-l2l-csr1kv.png">

1. Click **Download Configuration**
2. Select Cisco Systems, Inc. from the *Vendor* drop-down menu
3. Select CSRv AMI from *Platform* list
4. Leave software version selected 
5. Click **Download** button
6. Save file on your PC or on Virtual RDP.

!!! tip
	When you use webRDP, please use ***WordPad*** to edit the configuration file.
	
When file is downloaded, open it using text file editor. You will see IOS-XE configuration for your ON-PREM router.
In be *HEADER* section you will find <b><interface_name/private_IP_on_outside_interface\></b> which has to be replaced in entire file.

<img src="https://raw.githubusercontent.com/marcinduma/HOLCLD-2101/master/images/aws-l2l-csr-txt.png">

Using **Replace** function in your text editor, please replace the mentioned phrase by IP address of your CSR1000v Router:
```
<interface_name/private_IP_on_outside_interface>
```
```
198.18.133.254
```

Now you can copy/paste configuration of Site-2-Site VPN to your on-prem Cisco CRS1kv router ```ssh admin@198.18.133.254```.

!!! hint
	In the configuration template you will find command: `crypto isakmp keepalive threshold 10 retry 10`.
	You will get an error when paste it to CSR CLI. You can ignore it or correct it: `crypto isakmp keepalive threshold 10 10`.
	
Please copy not-commented lines. You can read comments, which describe each part of configuration.

Finally, when copied you will have TWO Site-2-Site VPN tunnels UP and TWO eBGP Sessions UP with AWS peers. Check status of the IPSec tunnels:

	show crypto session

<img src="https://raw.githubusercontent.com/marcinduma/HOLCLD-2101/master/images/aws-l2l-csr-crypto-session.png">

Check BGP peering `show ip bgp summary` - you should receive 1 prefix from each peer.

	show ip bgp summary
		
<img src="https://raw.githubusercontent.com/marcinduma/HOLCLD-2101/master/images/aws-l2l-csr-bgp.PNG">

On the AWS Dashboard you will see eBGP Peers UP in that section.

<img src="https://raw.githubusercontent.com/marcinduma/HOLCLD-2101/master/images/aws-l2l-status.png">

Tunnels are UP, eBGP is UP and routes are exchanged. Next section is about steering traffic to right VPN tunnel for on-prem subnets.

## Add routes for return traffic to on-premise Data Center

- **Step 1.** Select your Route Tables from the left menu, and find your VPC.

<img src="https://raw.githubusercontent.com/marcinduma/HOLCLD-2101/master/images/aws-vpc-rt-find.png">

- **Step 2.** Edit VPC Main Routing Table. Check in which row the *Main* column contains *Yes*. Make sure you selected Main route table for your VPC and not the *default VPC*.
Select that route table (usually it does not have a name) and select Routes tab from the bottom panel. Click on *Edit routes* button here.

<img src="https://raw.githubusercontent.com/marcinduma/HOLCLD-2101/master/images/aws-vpc-rt-edit-route.png">

- **Step 3.** Add route to On-Premise data center. Enter following parameters:

    - **Prefix:** 10.200.0.0/24
    - **Target:** type *vgw-* and you will find your Virtual Private Gateway created earlier.

  Click *Save routes*

!!! info
    Make sure you will see 2 routes in this route table, like in the picture below

<img src="https://raw.githubusercontent.com/marcinduma/HOLCLD-2101/master/images/aws-vpc-add-route.png">

- **Step 4.** Add the same return route under *subnets*. From the panel above select *aws-student-XX-private-route-table1* only and add the same subnet as in Step 3.

<img src="https://raw.githubusercontent.com/marcinduma/HOLCLD-2101/master/images/aws-vpc-rt-subnet-edit.png">

- **Step 5.** Add route to On-Premise data center. Enter following parameters:

    - **Prefix:** 10.200.0.0/24
    - **Target:** type *vgw-* and you will find your Virtual Private Gateway created earlier.

!!! info
    Make sure you will see 3 routes in this route table, like in the picture below

  Click *Save routes*

<img src="https://raw.githubusercontent.com/marcinduma/HOLCLD-2101/master/images/aws-vpc-subnet-add-route.png">

## Update Security Groups rules to allow traffic to on-premise Data Center

- **Step 1.** Select EC2 service

<img src="https://raw.githubusercontent.com/marcinduma/HOLCLD-2101/master/images/aws-ec2-enter3.png">

- **Step 2.** You should see only one ec2 instance, which is a worker node of the Kubernetes cluster.

<img src="https://raw.githubusercontent.com/marcinduma/HOLCLD-2101/master/images/aws-ec2-find-2.png">

- **Step 3.** Update EC2 security group.

Select your EC2 instance, on the bottom details area please click on link to edit Security Groups associated to this VM instance.

<img src="https://raw.githubusercontent.com/marcinduma/HOLCLD-2101/master/images/aws-ec2-sg-find-2.png">

you will be redirected to Security Groups dashboard where you should select *Inbound* and then click on *Edit rules* button.

<img src="https://raw.githubusercontent.com/marcinduma/HOLCLD-2101/master/images/aws-sg-enter-2.png">

- **Step 4.** Add new rule to allow ingress traffic to EC2 instance from On-Premise prefix.

Add new rule with following parameters:

  - **Type:** All traffic
  - **Source:** 10.200.0.0/24

Click Save.

<img src="https://raw.githubusercontent.com/marcinduma/HOLCLD-2101/master/images/aws-sg-add-rule-prefix-2.png">

## Validate connectivity

From Linux jumphost machine, ping IP address of your EC2 instance. 
To find out your EC2 instance IP address, go to EC2 dashboard and select *Instances* and your instance (1). In the bottom panel in *Details* tab (2), look for the IPv4 address (3) associated with the DNS name (4).

<img src="https://raw.githubusercontent.com/marcinduma/HOLCLD-2101/master/images/aws-ec2-ip.png">

You can try to ping this IP address from Linux Jumphost. 

<img src="https://raw.githubusercontent.com/marcinduma/HOLCLD-2101/master/images/linux-vpn-validation-2.png">