---
layout: post
title:  "The benefits of using a graphql api"
date:   2020-05-20 16:39:31 +0530
comments_id: 4
---

After working on REST APIs for some years, I shifted to the graphql APIs. Though there were some conceptual difference, both the APIs conventions are quite similar. In this blog I would walk you through how graphql apis differs from the REST APIs.

### Why graphql was created ?
As per the rest API convention, we create CRUD and other apis for a resource. Lets say we are designing a study portal for a school. And we want to return the results of all the students of a course. By Rest APIs, we might design it as

1. We will call one api which takes course id and gives us the result of each student. Here in most of the cases we store only the userId and won't store other metadata like his name etc.
2. Now for displaying the result on the UI, we will need to call one more API to get the user name.

The above example shows that we might end up doing a lot of API calls to fetch the data. The same issue was faced by Facebook in 2022. For fetching the NEWS Feed the facebook UI was ending up calling a lot of APIs and it was resulting in high network usage. That's when Facebook developed the graphql APIs to solve to get all the result in one API itself.


### What is GraphQL? 
The graphQL apis allows fetching the interconnected data too in the same call, what it means that we can get the user name also if we were fetching the course details. Also graphql returns only those data which the client requested for.

> “GraphQL is a query language for your API that shifts the contract between clients and servers that allows the server to say ‘these are the capabilities that I exposed’ and allows the clients to describe their requirements in a way that ultimately > > empowers product developers to build the products they want to create.”
>
> -- <cite>Dan Schafer, GraphQL Co-Creator</cite>

### What are the benefits of the GraphQL ?

* Is a query language for APIs and a runtime for fulfilling those queries with your existing data. 

* Provides a complete and understandable description of the data in your API

* Gives clients the power to ask for exactly what they need and nothing more, makes it easier to evolve APIs over time, and enables powerful developer tools.

* First built and used inside Facebook in 2012, open sourced and released as a specification in 2015.

* Uses http as transport layer.

* Very helpful in fetching data which is highly interconnected




### Limitations

* Powerful query language but mutation support lag behinds. The mutation type system is weak and inflexible.
* Http middleware created for rest are not useful.
* Http error codes are not relevant. All the information is contained in payload.

Reference https://graphql.org/