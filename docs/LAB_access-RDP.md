# Connectivity Check

## 1. Lab access general description

The lab has been built leveraging multiple cloud environments as following:

- Amazon Web Services
- Private intrastructure on-prem

You will have access to Cisco Intersight GUI, where you will see  Kubernetes Clusters deployed On-Prem. In the end you will manage your application that will be deployed in 2 different environments. The infrastructure between On-prem and AWS is ready and functioning. In this lab you will see how to connect microservices together to make whole application work.
Most of the tasks you will do from Linux Jumphost that is running on-premise. From there you will deploy components of your application in Kubernetes Cluster in AWS and on-prem.

## 2. Cisco dCloud dashboard

The entire lab for the session is built using Cisco dCloud environment.
Details of the session are provided in POD assigned to you. You will find there "Connect VPN" link which allow you connection to dCloud session.

### VPN connection to dCloud infrastructure

Once you get VPN credentials, open VPN client on CiscoLive PC or your own in case you use BYOD.
Login to dCloud VPN network, once connected you can proceed.

### Access session with RDP

Once logged to the dCloud session, you will be able to RDP Windows workstation ready to use for you

Open RDP client and use credentials provided below:

IP Address:

	198.18.133.10

Username:
	
	administrator

User password:
	
	C1sco12345

When you login to Remote Desktop, you will find installed Chrome as web browser, from where you get access to Cisco Intersight page.
To access CSR router and Linux jumphost, use Putty installed - shortcut is on Desktop.

## 3. Accessing Linux Jumphost

Open PuTTY client on RDP-workstation taskbar.

PuTTY has pre-defined session to CSR router as well as to ubuntu-terminal. Use predefined ubuntu-terminal session by selecting it and click Open button.

Username:
	
	dcloud

User password:
	
	C1sco12345


## 4. Accessing Cisco Intersight Platform

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

## 5. Accessing Cisco Intersight Assist

Cisco Intersight requires installation of local (on-prem) satelite system. Cisco Intersight Assist collect data from local vCenter and send it to Cisco Intersight PaaS in secure manner.
You can login to local Cisco Intersight Assist using credentials provided below:

URL:
	
	https://iva.dcloud.cisco.com
User name:
	
	admin

User password:
	
	C1sco12345

!!! warning
	You can explore Cisco Intersight Assist through the GUI, but please do not delete content already created.

## 5. Accessing CSR1kv Lab router

Your session contain Cisco CSR1kv router. It is used to terminate Site-2-Site tunnels with AWS tenant. All configuration is ready and doesn't require any modifications.

Please find login credentials and IP address to your CSR1kv router below - use PuTTY predefined session:

User name:
	
	admin
User password:
	
	C1sco12345

!!! warning
	Do not delete configuration already existing on the router.

## 6. Accessing vCenter for Lab

Whole setup is done on ESXi in Cisco dCloud environment. During the lab you don't need to perform actions on vCenter itself. However for case of troubleshooting or exploration, credentials to your vCenter below.

URL:
	
	https://vc1.dcloud.cisco.com/ui
User name:
	
	administrator@vsphere.local
User password:
	
	C1sco12345!


!!! warning
	Do not delete configuration nor VM machines already existing on the vCenter.
