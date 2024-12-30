---
layout: post
title:  "Aggregating data by days or hours in MongoDB"
date:   2020-10-31 15:39:31 +0530
category: tech
comments_id: 3
---

I came across a very interesting problem of aggregating our data stored in mongodb by day. Though at the first look it seems like a very easy problem, but taking care of the time zones in the aggregation pipeline makes it a little interesting. In this blog I will walk you through how we can solve this problem and the various challenges involved in the path.
<!--more-->

### Problem Statement And Solutions

I had the data of status of a pipeline with the timestamp(epoch time). The status of a pipeline can be SUCCESS or FAILED. The task at hand was to group the documents based on success and failures in each day/hour. The input I got was startTime and endTime interval, and I had to group the data by either days or either by hours. This looks like a very easy problem and can be solved by just grouping by date, month and year. The mongodb query will look something like

```
aggregate([
    {
        '$project': {
            newFieldName: {'$dateToString': {format: '%Y-%m-%d', date: '$yourDateFieldName'}}
        }
    }, {
        '$group': {
            _id: {newFieldName: '$newFieldName'},
            viewCount: {'$sum': 1}
        }
    }, 
    {'$sort': {'_id.newFieldName': 1}}
], {})

```

But there is an issue with this approach, the above code gives correct result for the UTC time zone as we are converting the time to the UTC zone, but won't work for the other time zones. 

To solve this issue I used the [bucket](https://docs.mongodb.com/manual/reference/operator/aggregation/bucket/) concept from the mongodb. This stage categories the input documents into buckets and outputs a document for each bucket.

To solve the aggregation problem I asked the client to give the startTime and endTime according to their timezone. Once I get the start and endTime, I created buckets between this time, where each buckets represents a day. After using the bucket operation I got the documents belonging to that particular day.


To solve the aggregation problem for hours, we will create buckets of size 1 hours instead of one day.