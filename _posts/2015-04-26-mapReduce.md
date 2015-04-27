---
layout: post
title: Map Reduce
categories: [general, mapReduce]
tags: [mapReduce]
fullview: false
---


[Wikipedia](http://en.wikipedia.org/wiki/MapReduce) states: 

> MapReduce is useful in a wide range of applications, including distributed pattern-based searching, distributed sorting, web link-graph reversal, Singular Value Decomposition, web access log stats, inverted index construction, document clustering, machine learning,and statistical machine translation. Moreover, the MapReduce model has been adapted to several computing environments like multi-core and many-core systems, desktop grids, volunteer computing environments, dynamic cloud environments, and mobile environments.

In simple words, _mapReduce_ is a distributed programing framework. It uses the known technique: _"Divide and conquer"_ for treating big amounts of data in a distributed environment. It does it by dividing the main problem in many others of small size and executing them across a cluster of servers [1] . It was used by google for a while. Hadoop is an open-source MapReduce engine.

There are 2 main tasks in a _mapReduce_ operation: 1 map operation and 1 reduce operation (duh!)

* __Map__: Transformation of data in a group of pairs key/value to further processing. this operation must be parallelizable.

* __Reduce__: Handles each value of each key of the map operation. It is a paralelizable operation.

For doing that, there are 4 steps:

* __split__: data is splitted in fragments.

* __Mapper__: Mapper is applied to data to get the couples key/value.

* __Shuffle__: Couples are grouped by key.

* __Reduce__: Reduce operation is applied.

_MapReduce_ is not only used by _hadoop_, but by some of nosql databases and big-data processing tools. The main idea behind this concept is not only to distribute data processing but enabling new data models to make data agroupations and clustering.

Lets take an example:

Imagine we have 4 documents in a mongodb database:
{% highlight json %}

[
{
	"REF": "1234",
	"price": 500,
	"enabled": "true"
	"store":"BBB"
},
{
	"REF": "0987",
	"price": 250,
	"enabled": "true"
	"store":"BBB"
},
{
	"REF": "1234",
	"price": 100,
	"enabled": "true"
	"store":"AAA"
},
{
	"REF": "0987",
	"price": 50,
	"enabled": "true"
	"store":"AAA"
}
]

{% endhighlight %}

And now lets imagine that we need to get the average price by reference. The first thing we do is a _map_ operation, where we get 2 references as follows:

{% highlight json %}
{"1234" : {500,100}}
{% endhighlight %}

 and 

{% highlight json %}
 {"0987" : {250,50}}
{% endhighlight %}

Finally, after a _reduce_ operation, we get 
{% highlight json %}
{"_id": "1234",
"value": 300}
{% endhighlight %}

and

{% highlight json %}
{"_id": "0987",
"value": 150}
{% endhighlight %}

We can do _MapReduce_ without hadoop. It is available by several languages and even in the base libraries of some funcional languages.

In _hadoop_, hive is frequently used as a way to do _MapReduce_ in a sql-like way.




[1]: "See Programming Hive. Jason Rutherglen. Dean Wampler. Edward Capriolo."


