---
layout: post
title:  "Capsicumization of the base system"
description: Hello FreeBSD!
date:   2020-05-15 15:00:00 +0530
categories: FreeBSD Capsicum Casper 
---

Welcome to my introductory blog post for the Google Summer of Code 2020. I will be working on [Capsicumization of the Base System](https://wiki.freebsd.org/SummerOfCode2020Projects/CapsicumizationOfTheBaseSystem) with FreeBSD under the mentorship of **Mariusz Zaborski** and **Mark Johnston**

# My Introduction

I am a final year undergraduate at the Indian Institute of Technology, Kanpur. I have a minor in Computer Systems. I successfully completed a project with FreeBSD in the Google Summer of Code 2018 with FreeBSD under the mentorship of Prof. Jonathan Anderson. The project details can be found here: [Oblivious Sandboxing with Capsicum](https://wiki.freebsd.org/SummerOfCode2018Projects/ObliviousSandboxingwithCapsicum).

It was a great learning experience  for me and allowed me to understand the principles of sandboxing and utilising Capsicum for the same. The approach that we used to sandbox applications involved building a **capability shell** which can run applications in a sandbox without the need of modifying them. This made me curious and I wanted to look at the other approach of modifying the applications to use sandbox, which is the current and harder approach but it helps to understand the principles of capsicum better which is why I chose to work on this project this year :)

# Project Introduction

A sandbox is a protection framework in computer security for separating running programs, typically in an attempt to prevent system failures or spreading software vulnerabilities. Capsicum is a sandboxing framework for principled, coherent compartmentalization of FreeBSD applications.

Writing an application which makes use of capsicum’s principles is not difficult. But what poses a challenge is to modify the existing applications. Most of the applications’ code was not written with privilege separation in mind. So, in order to capsicumize an application, we need to study what all does an application interact with, what all resources does it require, which can be a good point to enter the capability mode.

The application might require a casper service, either out of the existing casper services or a new one. While working on a new casper service we need to focus on:

* what API we are willing to offer, mapping out the necessary functions
* what all limitations should be enforced on this service

We aim to capsicumize i.e sandbox all of the existing base applications. Many applications have been sandboxed but still a lot of applications need to be capsicumized. This project aims to sandbox some of them, namely **traceroute6**, **fsck_ffs**, **fsdb**, **fsck_msdosfs**, **syslogd/file(1)**.

## Generic Approach to sandbox any applciation

The generic approach that we will use to sandbox an application will involve:

### Read the code

The first phase involves getting to know the application, reading the code and understanding what the application does. This will help in identifying which part of the code is allowed in the capability mode and which is not.

### Reorganize the code

After we are well versed with the application, we are ready to sandbox it. After understanding what all descriptors does the application need before entering the sandbox, we can provide those descriptors before cap_enter()
We can further read the code to understand what all capabilities do the descriptors need. For example in D9303(capsicumizing traceroute) it can be clearly seen that the connect() call was made before the call to cap_enter()

### See if any casper service is required

The application might need a service such as a DNS lookup or opening multiple files, which won't be allowed in the sandbox. Casper makes it possible to utilise these services from inside the sandbox. If writing a new casper service, we need to figure out what API are we trying to provide and what limitations it enforces.

### Enter the sandbox

Finally, we select the most suitable point of calling cap_enter() and enter inside the sandbox. Now, our application runs inside a sandbox making use of Capsicum and Casper.


I am greatly excited to be a part of this program once again, for all the learning experience and the interaction with the FreeBSD communtiy :)

