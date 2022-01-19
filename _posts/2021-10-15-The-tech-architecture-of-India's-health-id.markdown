---
layout: post
title:  "The tech architecture of Indian Health Id"
date:   2021-10-15 15:39:31 +0530
comments_id: 12
---

On Sept 27, PM launched the Ayushman Bharat Digital Mission, which would facilitate the management of the patient's health data using a unique health Id. This mission has the potential of bringing a revolutionary change in the health care infrastructure in India.
In this blog, I will walk you through a brief overview of the Tech architecture.

<!--more-->

## User Flow
![User Flow]("/assets/images/health-id/flow.png")

## Common Use Cases

### For Health Care Providers

* Create a health Id for their patients if they don't have the health Id already

* Link the health Id in their internal system if the user already has the health Id.

* Access the patient's previous data (consent required)

* Save the patient's consultation and other medical data

### For Patients

* Create their own health Id
* See their health records
* Provide consent for accessing the health record.


## Tech Architecture

The main software systems involved are:
* HIU (Health information user): The system that requests the health data.
* HIP(Health Information Provider): The system that provides the health data.
* App for the user (PHR App/ADBM Health Records): An interface for the user to access and manage their health data.

So who would create the HIU and HIP? As per the current architecture, private companies or startups can create and sell the HIU and HIP systems. The patient's document will be stored with the HIP only and not the government, government will just maintain a registry ( a mapping between a health record to the HIP which stores that particular record).

The actual tech flows involve a lot of services in between like Gateway, Registry, Consent Manager etc. To keep the blog simple, I have removed some of those flows.

The below diagram depicts a top-level flow between the various services.
![Tech Arch]("/assets/images/health-id/tech.jpeg")


## Summary
This framework provides an easy and complete solution for the communication between the various stack holders involved in the tech stack. The next challenge ahead is to figure out how to make this facility accessible to everyone in India and how a private practitioner can use this service.
Hope you enjoyed reading the blog. Please provide your suggestions and feedback.

Reference : https://sandbox.ndhm.gov.in/docs/integration_and_exit_process