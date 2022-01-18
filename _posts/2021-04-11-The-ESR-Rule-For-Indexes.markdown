---
layout: post
title:  "The ESR Rule for creating the mongo indexes"
date:   2021-04-11 07:39:31 +0530
comments_id: 8
---

In my present company, we place a lot of emphasis on optimizing the database queries. We create and review indexes for every each and every query. In this blog I present what are the best practices we follow.

If your table/collection has millions of data, then you can use mongo indexes to optimize your queries. The mongo indexes are stored as a B+ tree. If you want to see how a query will work using a index, you can visualize the B+ tree where after the parent node you select the next node based on filter given in the query.

