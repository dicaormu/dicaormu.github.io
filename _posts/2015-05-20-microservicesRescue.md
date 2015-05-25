---
layout: post
title: Microservices to the rescue
categories: [ methodology, microservices]
tags: [methodology, microservices]
description: How to continue developping in the modern way? microservices to the rescue.
---

Martin fowler defines a [Microservices](http://martinfowler.com/articles/microservices.html) architecture as

>”a particular way of designing software applications as suites of independently deployable services”

Nowadays, to design a highly available and scalable system, we have to change our traditional way of thinking. Tipically, we build monolitic applications, where one component contains all necessary elements. Those applications are usually deployed into application servers, that were created to host one or more applications together.

Cloud based development has made developers to face new challenges in scalability, availability and automatization. Now, our application is not only limited to one single machine. Besides, installing and monitoring this kind of software in an application server is difficult. Often it complexifies the application by making the relaese component bigger and dependent on configuration files or a particular directory structure. In other words, scaling out is not easy.

To solve those difficulties,  microservices arrived to the rescue.

## Why microservices are not just SOA?

SOA encourage the use of tools such as intelligent transport buses and complex business composition. In the begining it seemend to be a good idea, however, the same problems comming from the application server domain started to arise. In the end this prevented the proper scaling of the solution. 

In the other hand, microservices architectures promote dumb pipes and simple business composition, where each service is in charge of managing an unique domain. 


## Reactivity

There is another concept that I will deal with in future posts but makes a point to adopt a microservices vision: [reactive software](http://www.reactivemanifesto.org/). 

Users wait for applications to be available 100% of the time, even the not mission-critical ones, among other features.  Automatization (key-word for  cloud computing ) has become a must.

Distributed systems decompose a monolithic infrastructure into small scalable subsystems interconnected through a common transport.  The microservices architecture ease the implementation of a distributed software system  where each individual service is atomic, auto-deployable, stateless and most of the time, they are interconnected through http as the common transport. This facilitates automatization for the creation of new instances of a service in case of need. 

For each service there you use _”the right tool for the job”_, it means, for example, you can develop one service using python, because it is easier for the functionality and other one using scala for the same reason. That is what we call a _polyglot_ application. It is the same for the storage: you can create the services needed for reading-storing information in any database you need and you have your application with  polyglot persistence.

## Tools and Technologies

I want to point that when using gradle, sbt, mvn or your favorite build tool, you must assure that your service is auto-contained and deployed. You must include in your distribution component (e.g. jar) a lightweight http server such as jetty or embedded tomcat to enable your application to run by itself.

In this section I am going to mention some popular tools to develop and deploy microservices applications.

### [Springboot](http://projects.spring.io/spring-boot/)
Springboot is a micro-framework  that adds Boot built on the top of spring, with all its advantages but with some fixtures for developing microservices. it makes RESTful http and embedded web application easy to develop and use. 


### [Docker](https://www.docker.com/)
Even if docker is not a development tool but a deployment one, it is considered very important to the microservice architectures. [_Uncle Bob_](http://en.wikipedia.org/wiki/Robert_Cecil_Martin) says that microservices architectures are not architectures in the design as well but just a deployment view.  Docker and in general containers are highly used in cloud development, as a tool for devops and in general for distributed applications.

### [Dropwizard](http://www.dropwizard.io/)
It is something similar to _springboot_, they defined themselves as a library-framework to build restful applications. it uses jetty as the http server.

### [Wiremock](http://wiremock.org/)
Unit testing is really very important, and to test most of the rest functionality, wiremok gives a hand.

### [Hystrix](https://github.com/Netflix/Hystrix)
Netflix has become a big player of the opensource community and a reference point in development. Hystrix is a netflix project that acts as a circuit breaker tool, allowing to isolate failed componentes from the rest of the system.

## Final thoughts
Those are some tools just to start.  I hope this post helps you to start with your new distributed application.
