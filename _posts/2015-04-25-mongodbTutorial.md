---
layout: post
title: Introduction to Mongodb, a tutorial!
categories: [general, tutorial, mongodb]
tags: [database, mongodb]
fullview: false
---


[MongoDB](https://www.mongodb.org/) (from "humongous") is an open-source document database, and the leading NoSQL database[...] written in C++”

## Getting Started

To follow this tutorial, you can use either your own instance of mongodb or use the docker image I have created for this purpose.

If you are interested in using the docker image, you must do:

{% highlight ruby %}
sudo docker pull dicaormu/mongodbtest
{% endhighlight %}

and then 

{% highlight ruby %}
docker run -p 27017:27017 dicaormu/mongodbtest
{% endhighlight %}

This toy image starts an instance of mongodb 3.0.3 with an example dataset.

For further information about installing docker for your operative system, you can check [here](https://docs.docker.com/installation/), or read my post about containers.

In case you are interested in installing your own instance of mongodb you should continue reading the next item, otherwise, you should continue in section __First steps__

### Installation 
If you have mongodb installed or if you are using my docker image, you can skip this section.

For installing mongodb, take a look to the [installation manual](http://docs.mongodb.org/manual/administration/install-on-linux/) of mongodb for your O.S. In general, if you are in linux, you have to execute something like this: 
{% highlight ruby %}
pkg install mongodb
{% endhighlight %}

{% highlight ruby %}
apt-get install mongodb-10gen
{% endhighlight %}

{% highlight ruby %}
yum install mongo-10gen mongo-10gen-server
{% endhighlight %}

Config is expressed on the command line or in a config file. Mongo comes with sensible defaults (db port is 27017).

__How do I start working?__

start the service using mongod

```
> sudo service mongod start
```


Enjoy!!

## First steps 

*  Open the mongo shell: If you are using the docker image, you should [open a connection to the docker container](http://webiphany.com/technology/2014/06/12/what-ip-do-i-access-when-using-docker-and-boot2docker.html). From shell su can use:

```
> mongo <ip> (or mmongo.exe in windows)
```

* Explore the default database, how is it called?

```
> use test
```

```
> show collections
```

* Note: show tables works too!!!

* What are the collections in the database?

## Let's work with our db

* let's create a collection db named _books_

```
> use booksDb
```

```
> db.books
```

* Now let's create the books:

|ISBN	|Title	|Author	|Year|	Awards|
|---------------|-----------|-------------------|-------|-----------------------|
|9780061474095	|Anathem	|Neal Stephenson	|2008	|Locus award, Hugo award|
|9780007149827	|The yiddish policemen's union	|Michael Chabon	|2007	|Hugo award, Hammet prize, Ictineu prize|
|9780812536362	|Rainbow ends	|Vernor Vinge	|2006	|Locus award, Hugo award|
|9780441014156	|Accelerando	|Charles Stross	|2005	|Locus award|
|9780060750862	|The system of the World	|Neal Stephenson	|2004	|Locus award, Prometheus award|

<p/><br/>
I propose the first book, you can enhance this by creating the other books:


```
> db.books.insert({"ISBN":"9780061474095","Title":"Anathem","year":"2008", "Author":"Neal Stephenson" ,
   "awards":[{"prize":"Locus award", "year":"2009"},{"prize":"Hugo award", "year":"2010"}]})
```

* The command __insert__ inserts a document into a collection.
you can explore the database [documentation](http://docs.mongodb.org/manual/reference/method/js-collection/) to know a little more about aditional methods. There is in particular an interesting method: __save__. What is the difference between __insert__ and __save__?

* Now, let's take a look to the documents we have added to the collection.

```
> db.books.find()
```

* Have you noticed the _id field in the collection? Mongodb requires an unique identifier (_id) that acts as primary key. if you do not provide it, [mongo uses](http://docs.mongodb.org/manual/reference/object-id/) an __ObjectId__ to create one.

* You can add criteria to the search. Let's search books writen after 2005

```
> db.books.find({ year : { $gt : "2005" } })
```

* You can sort the answer by year:

```
> db.books.find({ year : { $gt : "2005" } }).sort( {year : 1} )
```

*  What does the 1 [means](http://docs.mongodb.org/manual/reference/method/cursor.sort/)? 

* A Mongodb query works as follows:

> Collection   +     Query Criteria   +    Modifier

* Take a look to the [query operators](http://docs.mongodb.org/manual/reference/operator/query/#query-selectors
) and the [logical operators](http://docs.mongodb.org/manual/reference/operator/query/#query-selectors
)

* Let's select books either by _Neal Stephenson_ or _ISBN_ 9780007149827

```
> db.books.find( { $or : [{Author : "Neal Stephenson"} , {ISBN : "9780007149827"}] })
```

* ... neither ... nor ...

```
> db.books.find( { $nor : [{Author : "Neal Stephenson"} , {ISBN : "9780007149827"}] })
```

* Books with _ISBN_ different from 9780441014156

```
> db.books.find( { ISBN: { $ne :   "9780007149827" }})
```

* Mongodb embeds a JavaScript runtime. Queries can use JavaScript to match. Using that you can find books with even ISBNs

```
> db.books.find({$where: function(){
	return parseInt(this.ISBN) % 2 == 1
}})
```

### Advanced queries

####Joins

Mongodb does not support joins, but as a schemaless DB it enables us to add subdocuments. Let's consider some more examples:

* Find the books that got a Nebula award

```
> db.books.find({ "awards.prize" : { $eq : "Locus award" } })
```

* Find the book that got the Prometheus award of year 2010

```
> db.books.find({ awards: { $elemMatch: { prize : "Prometheus award", "year": "2010" } }})
```

####Aggregations

Mongodb supports different ways to perform aggregations, such as [single purpose aggregations](http://docs.mongodb.org/manual/core/single-purpose-aggregation/
), [aggregation pipelines](http://docs.mongodb.org/manual/core/aggregation-pipeline/
) and [_map reduce_ jobs](http://docs.mongodb.org/manual/core/map-reduce/
).

Let's do some single purpose aggregations:

* Count the books

```
> db.books.find().count()
```

* Count the books by Stephenson

```
> db.books.find( {Author:"Neal Stephenson"}).count()
```

_Map reduce_ jobs are general pupsose aggregations and are written in _javaScript_.

Now you are ready to do something like:

* Count the number of awards for each author


* Count the number of awards per year


I hope this introduction helps you to take hands on mongodb.

Good luck!











