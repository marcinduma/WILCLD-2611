# Explore Cisco Intersight Dashboard

## 1. Accessing Cisco Intersight Platform

Cisco Intersight Platform manages Kuberenetes clusters in the private infrasturcture. You will have access to dedicated instance of Cisco Intersight, from which you will manage your own Kuberenetes Clusters used later on to deploy application.

Please find login credentials and URL to your IKS instance below:

URL:
	
	https://intersight.com/
User name:
	
	holcld2611+pod'X'@gmail.com

Where X will be provided by proctor	

User password:
	
	CiscoLive!2022

!!! warning
	You can explore Cisco Intersight through the GUI, but please do not delete content already created.

### Access Intersight using following steps:

Open WebBrowser (Chrome) and connect to https://intersight.com 
Select *Sign In with Cisco ID* option on the first screen - as shown on figure below.

<img src="https://raw.githubusercontent.com/marcinduma/WILCLD-2611/master/images/intersight-access.png" width = 800>

Enter e-mail provided by proctor to your POD:

<img src="https://raw.githubusercontent.com/marcinduma/WILCLD-2611/master/images/intersight-e-mail.png" width = 800>

Click next and fill password.

!!! tip
	credentials for the session can be found in WIL Assistant portal. In case of issues, ask proctor to help.
	
## 2. Intersigh Dashboard Target

When you are loged to Cisco Intersight, first page you see is *Monitor* section.

<img src="https://raw.githubusercontent.com/marcinduma/WILCLD-2611/master/images/intersight-monitor.png" width = 800>

Navigate to *Admin* section in the bottom of Navigation Pane on Left. Click on *Target*

<img src="https://raw.githubusercontent.com/marcinduma/WILCLD-2611/master/images/intersight-nav-target.png" width = 800>

Target section shows already Claimed services - in our case it is Cisco Intersight Assist installed "on-prem" together with vCenter.

<img src="https://raw.githubusercontent.com/marcinduma/WILCLD-2611/master/images/intersight-target.png" width = 800>

You can see status of claim, date and who executed it.
Click on our Intersight Assist - iva.dcloud.cisco.com to see details of the Target.

<img src="https://raw.githubusercontent.com/marcinduma/WILCLD-2611/master/images/intersight-target-details.png" width = 800>

## 3. Intersight Dashboard Operate

Most information from claimed targets are visible under *Operate* section. The section is divided to two sub categories: Virtualization and Kuberenetes.

### Virtualization

When exloring first of them, you will see information about all VMs managed by vCenter claimed in *Target* section.

<img src="https://raw.githubusercontent.com/marcinduma/WILCLD-2611/master/images/intersight-virtualization.png" width = 800>

By using three dots button on right column, you are able to manage each of VM:

<img src="https://raw.githubusercontent.com/marcinduma/WILCLD-2611/master/images/intersight-virtualization-menu.png" width = 800>

Option when open the *Menu*:

<img src="https://raw.githubusercontent.com/marcinduma/WILCLD-2611/master/images/intersight-virtualization-menu-open.png" width = 800>


On the other Tabs, you can verify details of Hosts, Storage, etc. Please explore yourself rest of the tab when interested.

<img src="https://raw.githubusercontent.com/marcinduma/WILCLD-2611/master/images/intersight-virtualization-tabs.png" width = 800>

### Kuberenetes

Second section contain informations about deployed Intersight Kuberenetes Clusters (IKS).

<img src="https://raw.githubusercontent.com/marcinduma/WILCLD-2611/master/images/intersight-k8s.png" width = 800>

You will see one IKS cluster, which is deployed on-prem. On main screen you see general information about its status - numbers of control plane nodes, workers, associated profile.
Using three dots button on most right column you open menu where you are able to download kubeconfig, undeploy Cluster or Open TAC case.

<img src="https://raw.githubusercontent.com/marcinduma/WILCLD-2611/master/images/intersight-k8s-menu.png" width = 800>

