# Welcome to our Cisco Live Hands-on Lab

Speakers:

*Faisal Chaudhry*, Distinguished Engineer, Cisco Systems, Inc. - **Distinguished Speaker**

*Filip Wardzichowski*, Software Engineering Technical Leader, Cisco Systems, Inc. - **Distinguished Speaker**

*Marcin Duma*, Customer Delivery Architect, Cisco Systems, Inc.

## Containerized Applications on Hybrid Cloud Environments

Nowadays application world is very dynamic. Changes in the infrastructures happens fast, requirements changes even faster.
Application components starts to be deployed in different locations based on various technical and business requirements.
It's nothing rare to deploy different layers of applications in physically different locations. Rate of use of Public Clouds vs on premise resources changes. Public Cloud become more and more considered for applications which can be hosted outside of own physicall capacity.

Rate of containeraized applications grow. Customers are deploying Kubernetes to orchestrate tenants, where they run their systems. Very often having dozens of Kubernetes deployments is nothing strange. However management of them become complicated.

Important is to have control at your overall environment. Cisco Intersight gives the possibility to deploy, orchestrate and provide a controll for all your Kubernetes clusters regardless of locations they are deployed*(Roadmap)*.

## High Level Design of Lab scenario.

During this lab session you will be able to experience of deployment multi-cloud application run on Kubernetes tenants. Three tier application is running in two different locations:

* On-Prem
* AWS

Components of the application and their interconnection is presented on the figure below.

<img src="https://raw.githubusercontent.com/marcinduma/WILCLD-2611/master/images/Overal-HybridApp.png">

By using Cisco Intersight, you will be able to operate Kubernetes clusters in vSphere - on premise.
You will manage each of Kubernetes tenant from central terminal server running Kubernetes commands to deploy our App.
Outcome of the lab is showing to attendees how to leverage Cisco Intersight and Kubernetes add-ons in daily K8s operations.
In the end of excercise you finally will see the results of Web-based interface showing you data processes by the app.

**<p style="text-align: center;">Enjoy!</p>**