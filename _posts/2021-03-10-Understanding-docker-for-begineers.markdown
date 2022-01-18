---
layout: post
title:  "Why do we need docker ?"
date:   2021-03-10 17:39:31 +0530
comments_id: 7
---

There are a lot of blogs on what and how of docker but there are quite few blogs on why to use docker. As a beginner I struggled with why exactly we want to use it. In this blog I will be answering this question.

In 2018, I was working on the OpenPrinting project. The OpenPrinting handles all the code which is required for handling printers and printing using a linux machine. I was using the c code and sometimes I faced issues in running the code as either some required library was missing in my OS or the version of the required library was different in my system. Every developer who is using this application will have to go through the same process.

What happens if we try to deploy this application on a server ? Then we will have to ensure that all the libraries should be correctly installed on the server.

Oh that's a lot of work!. What if we can create a container and keep all the required libraries and our application in that container and simply run the container. This way the developers can run the code on any OS and need not worry about the OS.

This is just one use case that is solved by docker, there are other use cases too like

* In my current role, I am using Redis(for cache), MongoDB (for database) and my frontend code. If I was manually running this applications then I will have to install all their required libraries. What is MongoDB requires a different version of a library and Redis requires a different version of the same library? The how will I run both this services together ? To solve this issue we can run the application in a docker container. For my local development, I use three docker containers, one for 
Redis, one for MongoDB and one for Frontend code.

* If a new person joins the organization, instead of running tons of command to setup the environment, he/she can use the docker containers for the libraries or dependencies.

* All the new DevOps tools have robust support for docker containers which makes it easy to deploy the services using it.

One of my startup friend was asking that whether he should use docker tool for his startup. When you are just starting a new startup you might not face the problems mentioned above and might not need to use docker. Anyways for a very early stage startup AWS provides quite some good DevOps tool.

Hope you find this blog useful.

Reference: https://stackoverflow.com/questions/28089344/docker-what-is-it-and-what-is-the-purpose