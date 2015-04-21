---
layout: post
title: Starting with bigData and hadoop!
categories: [general, bigdata, hadoop]
tags: [bigdata, hadoop]
fullview: false
---
When one starts working in bigdata, the first thing people ask is : « am i going to use hadoop ? »
Before we make a decision, one should know what hadoop is for and why is used for bigdata.

Gartner(http://www.gartner.com/) defines bigdata as V3 : Volume, Velocity, Variety . 
Specialists in bigdata sometimes encourage thinking about 2 additional Vs: Value (value of data) and Validity (quality of data).  The most important thing is that we cannot say for example “Big data is over 100 GB of data”. When we talk about those new technologies, we talk about a breakdown in the architecture, not just the size.

Data has become the new patrol, and there is a lot!!!!
But when we need to distribute data processing and data saving, we need something different and specialized for taking the job, and that is where hadoop arrives. 

Hadoop is a framework allowing to save and to distribute data in a cluster; thanks to his distributed file system (hdfs) and to process information fast, thanks to map-reduce and the multiple tools hadoop provides to facilitate this job. 

It is not the objective on this post to talk about history of hadoop, but I would like to say that it has been widely used by yahoo. Jeffrey Dean and Sanjay Ghemawat  from google, wrote the paper  that describes map-reduce for first time. (http://research.google.com/archive/mapreduce.html).

I know 3 distributions of hadoop.
1.	Direct from apache. It means that we have to install hadoop and its tools for managing and monitoring by hand.
2.	Distribution from hortonworks (hdp): once one have the machines, it facilities installation and monitoring of each node. Opensource.
3.	Distribution from cloudera: once one have the machines, it facilities installation and monitoring of each node. Not free.

As always, we can have a cluster of 1 node. Hortonworks has a sandbox for using and learning hadoop. But in a production environment, we need at least datanodes and namenodes.

![hadoop cluster]({{ site.url }}/assets/images/2.png)
