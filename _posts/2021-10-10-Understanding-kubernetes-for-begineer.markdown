---
layout: post
title:  "Understanding the Kubernetes for beginner"
date:   2021-10-10 16:39:31 +0530
category: tech
comments_id: 11
---

Kubernetes in one of the important tech Buzzword in the market. All the documents out are explaining the features and advantages of it but for a new developer it is quite difficult to relate to it. This blog covers why do we need kubernetes.

<!--more-->

The current blog requires an understanding of why do we need containerization. Please refer my blog on containerization [here]().

The containerization of the application solved the issue of setting up the environment. Our next challenges are:

* How can we run this containers on the cloud ? We can run this containers on a VM, but what if we get more traffic and we need to scale up our infrastructure? 
* How can we make sure that we aren't underutilized our VMs ?
* If I am using multiple services, how can I easily manage the communication between them ?
* To deploy the service, one way is to manually ssh into the VM and run our containers. But as the number of services grows then managing this manual process looks like a lot of task.

The solution to all the above issues is Kubernetes. It is used to deploy the container images on your cloud infrastructure. It is a very powerful tool with a lot of capabilities. It also allows us to scale up/scale down the resources as per the traffic, do deployments easily and safely and also utilize our resources properly.

So if you are an enterprise which is growing quite fast and want your tech to keep us the pace, then you can try out Kubernetes. Hope you find this blog useful.