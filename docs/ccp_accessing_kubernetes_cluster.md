# Accessing Kubernetes Cluster

## Kubectl - Kubernetes Command Line Interface

### Getting kubeconfig file from both created Kubernetes Clusters

While most of the options in Kubernetes are available through the dashboard, CLI commands are also available, and convenient to use. Kubectl is a software leveraging Kubernetes API and translate commands to specific API calls. This tool will be used during the lab.

Once connectivity to your new EKS Kubernetes Cluster is confirmed, go back to Cisco Container Platform (CCP) web page, login if required and select Clusters -> vSphere to display your newely created Kubernetes cluster.

<img src="https://raw.githubusercontent.com/marcinduma/HOLCLD-2101/master/images/ccp-cluster-onprem-5.png">

- **Step 1:** Accessing new Kubernetes cluster requires to obtain the kubeconfig file. Click on the name of your cluster to see the detailed view.

<img src="https://raw.githubusercontent.com/marcinduma/HOLCLD-2101/master/images/ccp-download-kubeconfig-onprem.png">

- **Step 2:** Download kubeconfig file, make sure the file name is ```on-prem-backend-kubeconfig.yaml```.

- **Step 3:** Copy kubeconfig file to your linux jumphost machine using SCP. Open WinSCP from the desktop, and login to Linux Jumphost using your credentials.

<img src="https://raw.githubusercontent.com/marcinduma/HOLCLD-2101/master/images/scp.png">

Copy kubeconfig file into your home directory (this is the directory opened after successful login)


Time to copy second kubeconfig for your AWS Kubernetes Cluster.

On CCP Dashboard go to **Clusters -> AWS** to display your newely created Kubernetes EKS cluster.

- **Step 1:** Accessing new Kubernetes cluster requires to obtain the kubeconfig file. Click on the name of your cluster to see the detailed view.

<img src="https://raw.githubusercontent.com/marcinduma/HOLCLD-2101/master/images/ccp-eks-download-kubeconfig.png">

- **Step 2:** Copy kubeconfig file to your linux jumphost machine using SCP. Open WinSCP from the desktop, and login to Linux Jumphost using your credentials.

<img src="https://raw.githubusercontent.com/marcinduma/HOLCLD-2101/master/images/scp.png">

Copy kubeconfig file into your home directory (this is the directory opened after successful login)



### Merge EKS kubeconfig file with existing kubeconfig file for on-premise Kubernetes.

SSH to Linux jumphost using PuTTY, confirm that BOTH your kubeconfig files have been copied to home directory

    ls -lt

<img src="https://raw.githubusercontent.com/marcinduma/HOLCLD-2101/master/images/linux-kubeconfig-in-home-2.png">

Merging kubeconfig files let you switch between contexts using kubectl tool, rather specifying full path to your kubeconfig file in every command.
This command will merge kubeconfig files and create new file in `~/.kube/config`. This is the default location for kubectl to find access information to particular Kubernetes Cluster.

!!! tip
	Before you merge the kubeconfig files, please verify file extention. It can happen that it is saved as **.yml** not **.yaml**. Correct next command when necessary.

Merge command:
	
	KUBECONFIG=~/on-prem-backend-kubeconfig.yaml:~/kubeconfig.yaml kubectl config view --flatten > ~/.kube/config

List files again in `~/.kube/config` directory to make sure that new `config` file is there.

    cd .kube
    ls -la

<img src="https://raw.githubusercontent.com/marcinduma/HOLCLD-2101/master/images/linux-kubeconfig-merge-2.png">

### IAM AWS Authentication for EKS cluster

- **Step 1:** Kubeconfig file usually contains private certificate that is uathorized by kubernetes directly. In case of EKS, AWS IAM authenthentication is involved. Instead of certificate, we will use your AWS access keypair to authenticate. On the linux jumphost, aws cli tool is installed. Similarily to kubectl this tool provides management access to your AWS account. Using this tool you can spawn new VM or create new networking infrastructure like VPC, subnets etc. In this lab, aws cli is leveraged by IAM-Authenticator module to sign kubectl requests towards EKS using Secure Token Service (STS) in AWS.

- **Step 2:** Configure aws cli with your access key.

In Linux jumphost console, type:

    aws configure

Provide the Access Key and Secret obtained in the previous task (AWS Tenant Cluster creation), you should have them saved in notepad.

        AWS Access Key ID [None]:
        AWS Secret Access Key [None]:
        Default region name [None]: eu-central-1
        Default output format [None]: text

> Make sure to enter exact name of region: **eu-central-1** and **text** as a default output format.

<img src="https://raw.githubusercontent.com/marcinduma/HOLCLD-2101/master/images/aws-cli-configure-2.png">

## Validate access to K8s Clusters from jumphost

Validate if your kubeconfigs has been correctly imported:

!!! info 
    For AWS EKS Cluster, as well as for on-prem you will have full admin rights.

List updated contexts:

    kubectl config get-contexts

<img src="https://raw.githubusercontent.com/marcinduma/HOLCLD-2101/master/images/kubectl-config-get-contexts.png">

!!! info
    Star indicates which kubernetes cluster you will manage using kubectl

If you would like to change context to aws EKS Kubernetes Cluster, please use following command:

    kubectl config use-context aws
    kubectl config get-contexts

<img src="https://raw.githubusercontent.com/marcinduma/HOLCLD-2101/master/images/kubectl-context-aws.png">

Validate your access and list Kubernetes nodes in AWS EKS Cluster

    kubectl get nodes

<img src="https://raw.githubusercontent.com/marcinduma/HOLCLD-2101/master/images/kubectl-get-nodes-aws-2.png">

To change context to on-premise Kuberenetes Cluster use follwing command:
        
    kubectl config use-context admin@on-prem-backend
    kubectl config get-contexts

Validate your access and list Kubernetes nodes in on-premise Cluster

    kubectl get nodes

<img src="https://raw.githubusercontent.com/marcinduma/HOLCLD-2101/master/images/kubectl-nodes-on-prem.png">