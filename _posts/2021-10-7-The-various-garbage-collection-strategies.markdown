---
layout: post
title:  "The various garbage collection strategies"
date:   2021-10-07 06:39:31 +0530
comments_id: 11
---

We recently came across an issue where our services were restarting multiple times due to max CPU usage. It took us some time to figure out the root cause, but by changing the GC strategy we were able to reduce the frequency of the outage. In this blog I present to you the various garbage collection strategies.

<!--more-->

One of the most attractive feature of Java is the Garbage collections, unlike C++ we don't need to worry about the memory leakage, we don't have to explicitly call the free method.

JVM supports quite some garbage collector strategies and some of them are experimental too. Most garbage collectors work by splitting the heap into generations. These are called the old generation and the young generation. The young generation is further divided into sections known as eden and the survivor spaces.

The rational of diving the heap space into two generations is:

* The young generation is only a portion of the entire heap, processing it is faster than processing the entire heap. The application threads are stopped for a much shorter period of time than if the entire heap were processed at once. You probably see a trade-off there, since it also means that the application threads are stopped more frequently than they would be if the JVM waited to perform GC until the entire heap were full. It is almost always a big advantage to have the shorter pauses even though they will be more frequent.

* The second advantage arises from the way objects are allocated in the young generation. Objects are allocated in eden (which encompasses the vast majority of the young generation). When the young generation is cleared during a collection, all objects in eden are either moved or discarded: objects that are not in use can be discarded, and objects in use are moved either to one of the survivor spaces or to the old generation. Since all surviving objects are moved, the young generation is automatically
compacted when it is collected.

As you consider which garbage collector is appropriate for your situation, think about the overall performance goals that must be met. Trade-offs exist in every situation. In an application measuring the response time of individual requests, consider these points:

* The individual requests will be impacted by pause times—and more importantly by long pause times for full GCs. If minimizing the effect of pauses on response times is the goal, a concurrent collector may be more appropriate.
* If the average response time is more important than the outliers (i.e., the 90th%) response time), a nonconcurrent collector may yield better results.
* The benefit of avoiding long pause times with a concurrent collector comes at the expense of extra CPU usage. If your machine lacks the spare CPU cycles needed by a concurrent collector, a nonconcurrent collector may be the better choice.


The various GC Algorithms are:

*  The Serial Garbage Collector: 
It uses a single thread to process the heap. It will stop all application threads as the heap is processed (for either a minor or full GC). During a full GC, it will fully compact the old generation.

* The Throughput collector: 
It uses multiple threads to collect the young generation, which makes minor GCs much faster than when the serial collector is used. This uses multiple threads to process the old generation as well. Because it uses multiple threads, the throughput collector is often called the parallel collector. The throughput collector stops all application threads during both minor and full GCs, and it fully compacts the old generation during a full GC.

* The G1 GC collector:
The G1 GC (or garbage first garbage collector) uses a concurrent collection strategy to collect the heap with minimal pauses. In G1 GC, the old generation is processed by background threads that don’t need to stop the application threads to perform most of their work. Because the old generation is divided into regions, G1 GC can clean up objects from the old generation by copying from one region into another, which means that it (at least partially) compacts the heap during normal processing. The trade-off for avoiding the full GC cycles is CPU time: the (multiple) background threads G1 GC uses to process the old generation must have CPU cycles available at the same time the application threads are running.

These were the three main garbage collectors. In next blog I would like to cover what are the things we take care of during selecting a garbage collector.