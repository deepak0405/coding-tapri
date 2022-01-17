---
layout: post
title:  "Why is it called relational database?"
date:   2020-10-14 12:39:31 +0530
comments_id: 6
---

When we refer to a database as relational, what relation are we talking about ? What is its domain and Range ?

If we remember from our high school a relation is defined as 

A relation between two sets is a collection of ordered pairs containing one object from each set. If the object x is from the first set and the object y is from the second set, then the objects are said to be related if the ordered pair (x,y) is in the relation.

The above definiton defines a binary relationship. We can define a n-ary relationship as a set of n sized tuples. 

The relational database concept was developed by the mathematical concept of relation. The table in our database is also a set of n sized tuples and such database models are called as Reltional databases.

The question which really troubled me is that if this is a relation then what is its domain and range ?
We can represent an n ary relation as a binary relation between a set of size (n-1) and a set of size 1. Hence we can define the domain and range for the relation. But this solution looks like we are just trying to fit in something, actually the concept of domain and range doesn't make much sense for a n ary relation.


Reference: 
* https://stackoverflow.com/questions/4045744/what-is-a-relation-in-database-terminology/11619123#11619123
* https://math.stackexchange.com/questions/3792270/domain-and-range-of-n-ary-relations