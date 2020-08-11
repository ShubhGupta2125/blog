---
layout: post
title:  "Introduction to Reactive Systems"
description: Getting started with reactive sytems
date:   2020-08-10 12:00:00 +0530
categories: Reactive Akka 
---
Hi! Welcome to my blog post on Reactive systems. I am writing this while learning the principles of Reative architecture.

## Why Reactive?

Responsiveness, is what makes the experience satisfying. Dealing with this much of data which is changing. The primary goal of reactive architecture is to provide an experience which is responsive under all conditions.

## Reactive Principles

**Reactive Manifesto** brings independantly developed patterns for solving similar problems. Hence the common ideas are brough together in a unified place.

* **Responsive** - A reactive system consistetly responds in a timely fashion
* **Resilient** - A reactive system is resposnive, even if failures occur
* **Elastic** - A reactive system is responsive, despite changes to load(upscale and downscale)
* **Message Driven** - A reactive system is built on the foundation of async, non blocking messages

### Responsive

* Cornerstone of usability
* Systems must respond in a fast and consisten fashion
* Responsiveness builds user confidence

### Resilient

* Provides responsiveness, despite failures
* Achieved through replication, isolation, containment, delegation
* Failures are isolated to a single component
* Recovery is delegated to an external component

## Elasticity

* Elasticity provides responsiveness, despite increases (or decreases) in load
* Implies zero contention and no central bottlenecks
* Predicitve auto scaling techniqus can be used to support elasticity
* Scaling up provides responsiveness during peakm while scaling down improves cost effectiveness

### Message Driven

* Responsivess, Resillience, Elasicity are supported by a message driven architecture
* Messages are asynchronus and non-blocking
* Provides loose coupling, isolation, location transparency
* Resources are consumed only while active

## Reactive Programming

### Reactive systems vs Reactive Programming

* Reactive systems and Reactive programming are often misunderstood
* They are not equivalent
* Reactive systems apply Reactive principles at the architecture level
* Reactive Programming can be used to build reactive systems(or not)

### Reactive Systems

* The reactive manifesto principles are intrinsic to the design and architeture of reactive systems
* All major architecture components interact in a reactive way
* Reactive Systems are seperated along asynchronous boundaries
* Eg. Reactive Microservices

### Reactive Programming

* Reactive PRogramming can be used to support the construction of reactive systems
* support sbreaking problems into small discrete steps
* Steps are executed in async/non blocking fashion, usually via a callback mechanism
* Eg. Futures/Promises, Streams, RxJava/RxScala
* A system that uses Reactive Programming is not necessarily a Reactive System

## Reactve Systems and Actor Model

### Actor Model

* The *Actor Model* is a programming paradigm that supports construction of Reactive systems
* It is message driven
* Abstractions provide *Elasticity* and *Resilience*
* It can be used to build *Responsive* software
* On the JVM:
    - Akka implemets the *Actor Model*
    - Akka is the foundation of Reactive tools like Lagom and Akka streams

### Fundamental Concepts of the Actor Model

* All computations occur inside of the Actors
* Each actor has an address
* Actors communicate only through asynchronous messages

### Location Transparency

* The *Message Driven* nature of actors supports *Locaction Transparency*
* Actors communciate using the same technique regardless of location
* Local vs Remote is mostly configuration
* Location Transparency enables actors to be both *Resilient* and *Elastic*
* The essence of Location Transparency is, it dosn't matter if the actor is local or remote, the Router between the actors know how to route between the actors

### Location Transparency vs Transparent Remoting

* Location Transparency should not be confused with Transparent Remoting
* Transparent Remoting:
    - Remote calls look like local calls
    - Hides the fact that you are making remote calls
    - Hides potential failure scenarios (Eg. network failures)
* Location Transparency:
    - Local calls look like remote calls
    - Assues you are always making remote calls
    - You have to assume remote failure scenarios can occur (Eg. network failures)

### Importance of the Actor Model

* There are many Reactive Programming tools
* Most of them only support some of the reactive principles
* You often have to combine different technologies to build a Reactive System
* The *Actor Model* provides facilities to support all of the Reactive Principles
    - Message driven by default
    - Location transparency to support *Elasticity* and *Resilience* through distribution
    - *Elasticity* and *Resilience* provide responsiveness

### Reactive System without Actors

* Reactive Systems are possible without actors
* Components are added rather than being built in
* Requires additional infrasructure like:
    - Service Registry
    - Load Balancer
    - Message Bus
* Result will be reactive at the large scale, not necessarily the small

**Thanks! Happy coding :)**
