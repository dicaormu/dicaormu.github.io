---
layout: post
title: Starting with bigdata and hadoop!
categories: [general, bigdata, hadoop]
tags: [bigdata, hadoop]
fullview: false
---
When one starts working in bigdata, the first thing people ask is : « am i going to use hadoop ? »
Before we make a decision, one should know what hadoop is for and why is it used for bigdata.

The most important thing to remember is that we cannot say: “Big data is over 100 GB of data”. Bigdata is not just about volume, it is about an architecture breakdown.

[Gartner](http://www.gartner.com/) defines bigdata as V3:

 * Volume 
 * Velocity
 * Variety

Specialists in bigdata sometimes encourage thinking about 2 additional Vs: 

* Value (value of data)
* Validity (quality of data).  

Data has become the new petroleum, and there is a lot of it!!!! But when we need to distribute data processing and data saving, we need something different and specialized for taking the job, and that is where _hadoop_ arrives. 

_Hadoop_ is a framework that lets you to save and to distribute data in a cluster; thanks to its distributed file system: __HDFS__. It also allows a fast information processing, thanks to _map-reduce_.

It is not the objective on this post to talk about the history of _hadoop_, but I would like to say that it has been widely used by [_yahoo_](https://developer.yahoo.com/hadoop/). _Jeffrey Dean_ and _Sanjay Ghemawat_ from google, wrote the original paper that describes [map-reduce for the first time](http://research.google.com/archive/mapreduce.html).


I know 3 distributions of _hadoop_ :

* Directly from _Apache_. It means that we have to install hadoop and its tools for managing and monitoring by hand.

Distributions from system integrators as:

* _Hortonworks_ (hdp): once one have the machines, it facilitates installation and monitoring of each node. Opensource.
* _Cloudera_: once one have the machines, it facilities installation and monitoring of each node.


In order to learn the basics, we can have a cluster of only 1 node. _Hortonworks_ even has a [sandbox](http://hortonworks.com/products/hortonworks-sandbox/) for using and learning _hadoop_. 


The general _hadoop_ architecture is as follows:

![hadoop architecture]({{ site.url }}/assets/images/architecture.png)

At the date, hadoop just anounced version __2.7__. In general, all _hadoop_ 2.x work with _YARN_ as base of _map-reduce_.

A _hadoop_ cluster has at least 2 elements: datanodes and namenodes.


![hadoop cluster]({{ site.url }}/assets/images/2.png)

_Namenodes_ and _datanodes_ work in a _master/slave_ mode where the namenode manages _hdfs_ information and _datanodes_ store and distribute blocks. One can add nodes because hadoop has been built to scale. 

In the next post I am going to make a little introduction to _map-reduce_.


