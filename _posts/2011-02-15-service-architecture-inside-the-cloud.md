---
layout: post
title: Service Architecture Inside The Cloud

tags: Amazon,Cloud,Programming,Service Oriented Architecture,Software,Technology
---
When I started doing some serious programming about ten years ago this new buzzword started to get passed around. When I was browsing the isles at Barnes and Noble every other new-age programming book would pop up describing how a service oriented architecture would be the future of software development. How it would bridge the gaps between platform dependent code and allow us to use cheap hardware when necessary to serve enterprise clients (and other services). It promised a more modular approach to programming, encapsulating functionality in a bundled executable called a "service" which had a schema that it responded to, but it via XML, SOAP or some other protocol. 

Whenever I dream up a project I tend to use it as a driver for learning a new software library or language. When reading first about the service oriented architecture paradigm the Java programming stack was usually the king of the hill when it came to discussions. Even today, after Oracle purchased Sun and basically started to put nails in the proverbial Java coffin, it still reminds a leader in enterprise service oriented design. I am a C/C++ programming, self taught and currently by trade, but I would be a fool to ignore the advantages that this platform offered. So as any good project manager I read up a lot on Java (at the time) and learned as much as I could about SOA practices. 

A few years ago I started attending college for the computer science discipline and Java was the primary language that was being taught everywhere. Although, until some of my later entrepreneurial projects, I heard not a word about SOA practices in any of my programming or software engineering courses. A few years ago the topic of the "Cloud" became all the rage; people were making money off writing books, companies such as Microsoft (and even Sun) were working on Cloud projects to help developers and Amazon started selling specialized hosting geared towards metered bandwidth, CPU and memory usage. I began asking myself: <em>what is different about software in the Cloud?</em>

Well, the truth is, software that is written to be able to take advantage of all the regularly toted features of the Cloud such as being able to elastically adjust your application's presence on demand, is just the service oriented architecture approach of designing software taken to the limit. The actual truth of the matter is that any piece of software that is designed to be fully "cloud compliant" is most likely some kind of service, be it a web application using the HTTP protocol or a Glassfish Java application stack using XML or SOAP as communication protocol. When designed properly a service oriented platform stack should be able to scale horizontally much more efficiently than it does vertically. 

What the is the difference between scaling out vertically and horizontally? When an application scales out vertically this means adding more memory, CPU power, hard-drive space, etc, to an existing system that is servicing clients. Scaling out vertically is merely adding additional computing nodes. This means everything to a distributed architecture; as soon as the node touches the grid it should be servicing clients. But as I said earlier in this essay the idea of SOA practices have existed long before the marketing engine of Salesforce and Amazon have trademarked the word cloud.

The principle of the cloud is the ability to scale out vertically on demand. If your application is about to get hit by a swarm of geeks from <a href="http://slashdot.org">Slashdot</a> any normal application running on cheap Linux metal in a data center would likely cripple under the additional CPU, bandwidth and memory requirements put in place by this surge of new clients. An application that is able to be scaled out can elastically grow and shrink on demand, servicing the needs of its client base at any single point in time.

But what does that mean for business? You only pay a metered rate for bandwidth and CPU cycles on the amount that you're using at any given point in time. Your traffic at 2AM in the morning on a Thursday likely is not anywhere near the traffic that you have at peak Internet browsing hours. Why should you be paying those massive hosting fees when you're really only using your hardware to the limit about three to four hours a day? 

This is the principle behind "the cloud," and if you couple this with a logical service oriented application design (see: distributed) your business will much more agile and cost effective in both the peak and downtime hours. 