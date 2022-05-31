## Create AWS Infrastructure Provider

Before you will attempt to create cluster, you will create an infrastructure provider profile for AWS. 

- **Step 1:** Login to AWS console, and click on your username in the right top corner as in the figure:
- **Step 2:** Select "My Security Credentials" 

<img src="https://raw.githubusercontent.com/marcinduma/HOLCLD-2101/master/images/aws-access-key-enter.png" width="250">


- **Step 3:** Click "Create access key" button
<img src="https://raw.githubusercontent.com/marcinduma/HOLCLD-2101/master/images/aws-access-key-create-new.png">

- **Step 4:** Copy to Access Key ID and Secret access key. Please note that the "Secret access key" is displayed only during creation of the key, and will not be visible after closing this wizzard.

!!! Attention
	<span style="color:red">
	**Please save the ACCESS KEY and SECRET KEY in the notepad, it will be necessary in the later stage**
	</span>

<img src="https://raw.githubusercontent.com/marcinduma/HOLCLD-2101/master/images/aws-access-cred.png">

- **Step 5:** Go back to CCP Control Plane panel. From the left panel in CCP, select "Infrastructure Providers" and select "AWS" in the main section. 

<img src="https://raw.githubusercontent.com/marcinduma/HOLCLD-2101/master/images/ccp-aws-infra-prov.png">

- **Step 6:** Create a "New Provider" profile, provide following parameters:
    - **Provider Name** *studentXX*
    - **ACCESS KEY ID** *use access key id copied from AWS*
    - **SECRET ACCESS KEY** *use secret access key copied during creation of secret access key in AWS*

<img src="https://raw.githubusercontent.com/marcinduma/HOLCLD-2101/master/images/ccp-aws-infra-prov-key.png">

Check if new key has been created, remember the infrastructure provider profile name.

## Create Tenant Data Cluster

After login to Cisco Container Platform, go to **AWS** tab and click `New Cluster` button. You will be redirected to the new page where you will provide details of your new Kubernetes EKS cluster.

<img src="https://raw.githubusercontent.com/marcinduma/HOLCLD-2101/master/images/ccp5-aws-new-cluster.png">


- **Step 1:** Basic Information - select infrastructure provider, AWS Region and Kubernetes cluster version and name. 

Please use following parameters.

  - **Infrastructure Provider:** *studentXX*
  - **Kubernetes Cluster Name:** *aws-student-XX*
  - **AWS Region:** *eu-central-1*
  - **Kubernetes Version:** *1.15*


*studentXX - XX is your unique student ID, assigned by speakers.*

<img src="https://raw.githubusercontent.com/marcinduma/HOLCLD-2101/master/images/ccp-aws-cluster-create-1.png">

- **Step 2:** Node Configuration - here you will configure how EKS nodes will be setup. You will specify EC2 instance type, AMI image, number of worker nodes, IAM Role and SSH public key, so you could ssh into the node for troubleshooting purposes. 

**Please use exact paramaters as instruction says.**

  - **Instance Type:** *t2.small*
  - **Machine Image:** *hvm-ssd/ccp-ubuntu-bionic-18.04-amd64-server-20200729-7.0.0*
  - **Worker Count:** 1
  - **IAM Access Role ARN:** *studentXX-role* - provided by speakers
  - **SSH KEY:**
	
		ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIJeLi4z9dYE+6tqTXzsELMch2RjR6R+rl57UEJzMuPkO
	


Select Machine Image by expanding the list, from the drop-down list click on "SHOW 3 FILTERERD OPTIONS" then select the 2nd image.

<img src="https://raw.githubusercontent.com/marcinduma/HOLCLD-2101/master/images/ccp-aws-cluster-create-2.png">

You should have similar options selected

<img src="https://raw.githubusercontent.com/marcinduma/HOLCLD-2101/master/images/ccp-aws-cluster-create-3.png">

Your AWS user is configured with IAM policy that allows to assume this specific role. For this CCP leverages IAM-Authenticator add-on, that is installed in Linux jumphost. Later on the Linux jumphost you will login to your aws cli with your associated aws credentials and then you will be able to manage you new EKS Kubernetes Cluster. Instead of using username and password or private certificates, IAM Authenticator leverages AWS STS (Secure Token Service) to tokenize and sign URL requests towards your EKS Cluster. AWS IAM is responsible to authorize request and pass commands to your Kubernetes Cluster.
During creation of EKS Cluster, this role is associated with Kubernets System:Masters group which provides full access to your cluster.


- **Step 3:** VPC configuration - here specify your VPC subnets. CCP will request VPC creation in AWS, with subnets, internet gateway, nat gateways. It is creating 3 private and 3 public subnets. Please use default subnet's from CIDR: 10.0.0.0/16.

<img src="https://raw.githubusercontent.com/marcinduma/HOLCLD-2101/master/images/ccp-cluster-aws-3.png">

Click Next to enter the summary page, and just confirm all data. Once confirmed please click `Finish`

<img src="https://raw.githubusercontent.com/marcinduma/HOLCLD-2101/master/images/ccp-aws-summary.png">

Once finished, you will see progress bar to check status of the cluster creation. 

<img src="https://raw.githubusercontent.com/marcinduma/HOLCLD-2101/master/images/ccp5-eks-creating.png">

## Monitor cluster creation

You can observe tenant cluster creation from CCP Dashboard, however, if you are interested to see more details, you can login to AWS dashboard and go to EKS to monitor master creation, and then to CloudFormation to see status of CloudFormation Stack deployment. CloudFormation is a AWS tool to automate creation of different objects.

Login to AWS dashboard, and select EKS service. **Use credentials provided to you by speakers.**

<img src="https://raw.githubusercontent.com/marcinduma/HOLCLD-2101/master/images/aws-eks-find.png">

In EKS dashboard you will see EKS service creation progress. Once finished you can move to CloudFormation dashboard.

<img src="https://raw.githubusercontent.com/marcinduma/HOLCLD-2101/master/images/aws-cloudformation-find.png">

From there find your stack (based on your username) and watch deployment progress.

<img src="https://raw.githubusercontent.com/marcinduma/HOLCLD-2101/master/images/aws-cloudformation-watch.png">

Once finished, you should see in CCP GUI that the Kubernetes Cluster in AWS has been deployed successfully.

<img src="https://raw.githubusercontent.com/marcinduma/HOLCLD-2101/master/images/ccp-eks-ready.png">

At this point go to the next chapter to connect your Kubernetes Cluster in AWS to Hybrid Network that provides access to on-premise Data Center.