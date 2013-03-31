---
layout: default
title: "APIs and Frameworks"
date: "2013-03-31"
categories: ""
tags: "API cassandra silvertunnel TOR"
---
<br/>
<p style="text-align:justify">A large combination of APIs and frameworks were used to build CassTor, in this blog I'll share my experience in dealing with each and why I decided to use them in the first place.
</p>

<h2>APIs</h2>
<h3>Astyanax</h3>
<p style="text-align:justify">A very light APIs that allows interfacing with Cassandra. Astyanax is difficult to pronounce and very easy to get started with! There was a huge choice in APIs to use as connectors to Cassandra and even more have come out since the beginning of this project with the latest being the ODBC driver for HIVE from Datastax. I feel that I've got plenty of experience of Cassandra APIs, some experiences were enjoyable, like using CQL for the first time, and some not so much (I didn't like hector but back in 2011 it seemed like a good choice). I chose Astyanax for three main reasons: It was something new, I quite enjoy learning new things and the API became very popular with the stackoverflow community when I was starting my project and the API supported CQL and RPC.<br/><br/>
Astyanax has been one of the simplest APIs I've ever gotten to use and I'd like to think that it is thanks to Netflix's amazing documentation. My struggle with hector was primarily because I didn't know how Cassandra worked at the time, but having to look through unit tests to find code snippets for creating keyspaces and such wasn't very helpful.
</p>

<br/>

<h3>Silvertunnel TOR</h3>
<p style="text-align:justify">This was a choice based on the lack of choice available. There are few libraries for connecting through TOR, netlib and the MIT torlib, one was C++ wrapped in java and the other was using out-dated socket implementations (that when tested failed to connect correctly). Silvertunnel is a highly threaded API that allows for redirecting network traffic of a Java application by overriding the <code>Socket</code> class and redirecting it through the <code>NetLayer</code> provided by the API. Sadly connecting to TOR is very slow (I really mean slow, it can take anything between 6-15 minutes) and doesn't work if a firewall is present but once a connection is established querying delays are small (a typical query that requires 8ms to execute will jump up-to 150ms, a big jump, but still not noticeable by a human unless executing hundreds of sequential queries).
</p>

<br/>

<h2>Frameworks</h2>
<h3>Java SWING</h3>
<p style="text-align:justify">SWING was the prime contender if CassTor was to be implemented as a desktop application. The decision for a desktop application was based on avoiding unnecessary connections to the internet.<br/><br/>
Why did I pick SWING? Again, something new, I've made a number of JSP/Spring MVC web applications but never a desktop application, and when researching the various frameworks out there, SWING seemed like a really good choice as it allowed for styling an application to look like it's running natively on OSX and Windows7 and building a cross-platform application was the ultimate goal.

<br/><br/>
<img src='/thumbnails/images/Screen-Shot-2013-01-22-at-23-08-29.png' alt='CassTor internal email frame' width="96%">
<br/><br/>

Swing is a great framework, but there was a number of issues faced while using it, most of which were because my lack of experience with Java GUI design. I struggled to build frames so that when they were resized, their sizes would change to look suitable. Also it's great when IDEs try to prevent you from breaking your application, but Netbean's approach of disabling me from altering GUI related code was very frustrating, to the point where I was considering switching to IntelliJ, but it was too late in the project and dealing with potential issues would be a loss of time I couldn't afford.
</p>

<br/>

<p>To sum it up, each library/framework used had it's challenges but overall not using them would make it much-much more challenging to build the project!</p>
