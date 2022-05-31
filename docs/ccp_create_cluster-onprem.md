## Create Tenant Data Cluster

After login to Cisco Container Platform, go to **Clusters** click on **vSphere** tab and click `New Cluster` button. You will be redirected to the new page where you will provide details of your new *Kubernetes on-prem cluster*.

<img src="https://raw.githubusercontent.com/marcinduma/HOLCLD-2101/master/images/ccp-newcluster-onprem.png">


- **Step 1:** Basic Information - select infrastructure provider, Kubernetes cluster version and name. Please use following parameters.

  - **Infrastructure Provider:** *vsphere*
  - **Kubernetes Cluster Name:**
		
		on-prem-backend
	
  - **Kubernetes Version:** *1.17.6*


<img src="https://raw.githubusercontent.com/marcinduma/HOLCLD-2101/master/images/ccp-cluster-onprem-1.PNG">

- **Step 2:** Provider Settings - here you will configure how your on-prem cluster will be deployed. You need to define Data Center name, Cluster name, Datastore and more.

**Please use exact paramaters as instruction says.**

  - **DATA CENTER NAME:** *datacenter*
  - **CLUSTER NAME:** *CCP*
  - **DATASTORE NAME:** *datastore1*
  - **VM TEMPLATE NAME:** *ccp-tenant-image-1.17.6-ubuntu18-7.0.0*
  - **VM NETWORK NAME:** *CCP_Intra*

<img src="https://raw.githubusercontent.com/marcinduma/HOLCLD-2101/master/images/ccp-cluster-onprem-2.PNG">

- **Step 3:** Node Configuration - here you will configure capacity of your Kubernetes Nodes. You are able to configure amount of Workers, their vCPU or vRAM amount. In this section you need to configure SSH settings to be able to connect directly to your Kubernetes Nodes (Master as well as Workers). Finally you can allocate numbers of Load Balancer VIPs, subnet as well as POD CIDR.

**Please use exact paramaters as instruction says.**

  - **WORKER NODES:** *2*
  - **SSH User:**
	
		ccpuser
	
  - **SSH KEY:**
		
		ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIJeLi4z9dYE+6tqTXzsELMch2RjR6R+rl57UEJzMuPkO
	
  - **LOAD BALANCER VIP:** *2*
  - **SUBNET:** *default-network-subnet*
  - **POD CIDR:** *192.168.0.0/16*

<img src="https://raw.githubusercontent.com/marcinduma/HOLCLD-2101/master/images/ccp-cluster-onprem-3.PNG">

Rest of variables please leave blank.

- **Step 4:** Next screen summarizes all variables you did choice. Please review them before you click `Finish`.

<img src="https://raw.githubusercontent.com/marcinduma/HOLCLD-2101/master/images/ccp-cluster-onprem-4.PNG">


## Monitor cluster creation

You can observe tenant cluster creation from CCP Dashboard. Another place you can observe whats happening on vCenter by connecting via User Interface.

Once finished, you should see in CCP GUI that the Kubernetes Cluster in vSphere has been deployed successfully.

<img src="https://raw.githubusercontent.com/marcinduma/HOLCLD-2101/master/images/ccp-cluster-onprem-5.png">

At this point go to the next chapter to create your Kubernetes Cluster in AWS Public Cloud.