# Welcome to our Cisco Live Hands-on Lab

Speakers:

*Faisal Chaudhry*, Distinguished Engineer, Cisco Systems, Inc. - **Distinguished Speaker**

*Filip Wardzichowski*, Consulting Engineer, Cisco Systems, Inc. - **Distinguished Speaker**

*Marcin Duma*, Consulting Engineer, Cisco Systems, Inc.

## Containerized Applications on Hybrid Cloud Environments

Nowadays application world is very dynamic. Changes in the infrastructures happens fast, requirements changes even faster.
Application components starts to be deployed in different locations based on various technical and business requirements.
It's nothing rare to deploy different layers of applications in physically different locations. Rate of use of Public Clouds vs on premise resources changes. Public Cloud become more and more considered for applications which can be hosted outside of own physicall capacity.

Rate of containeraized applications grow. Customers are deploying Kubernetes to orchestrate tenants, where they run their systems. Very often having dozens of Kubernetes deployments is nothing strange. However management of them become complicated.

Important is to have control at your overall environment. Cisco Container Platform (CCP) gives the possibility to deploy, orchestrate and provide a controll for all your Kubernetes tenants regardless of locations they are deployed.

## High Level Design of Lab scenario.

During this lab session you will be able to experience of deployment multi-cloud application run on Kubernetes tenants. Three tier application is running in two different locations:

* On-Prem
* AWS

Components of the application and their interconnection is presented on the figure below.

<img src="https://raw.githubusercontent.com/marcinduma/WILCLD-2611/master/images/Overal-HybridApp.png">

By using CCP, you will be able to deploy Kubernetes clusters in vSphere - on premise and AWS.
Once done, you will manage each of Kubernetes tenant from central terminal server running Kubernetes commands to deploy our App.
In the end of excercise you finally will see the results of Web-based interface showing you data processes by the app.

**<p style="text-align: center;">Enjoy!</p>**