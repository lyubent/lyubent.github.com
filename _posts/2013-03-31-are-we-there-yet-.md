---
layout: default
title: "Are we there yet?"
date: "2013-03-31"
categories: ""
tags: "progress"
---
<br/>

<h2>Upgrading to the latest</h2>
<p style="text-align:justify">
There are too many new features in Cassandra 1.2.3, and at this stage I'm planning on upgrading from 1.2.0 to the latest version. There aren't too many changes that can affect the upgrade, the prime concern is the switch from Thrift to CQL, but when I was reading up on this its clear that Apache have kept interfacing with thrift as an option for backwards compatibility. An attempt of switching will be made on Tuesday and hopefully not too much has changed.
</p>

<h2>Joining the ring</h2>
<div style='float:left;margin-right:15px;'>
<img src='/thumbnails/images/fCJO2hQ.jpg' alt='Cassandra ring after a new user.' width="400px"></div>
<p style="text-align:justify;">The three seed nodes are <code>134.36.36.188, 134.36.36.189, 134.36.36.217</code> with each host running on Windows 8, Ubuntu and OSX respectively. The final machine, <code>134.36.36.116</code> is an OSX machine representing the first user to join the ring and is connected to the ring through a VPN connection. With each user that joins the ring will grow, the theory being that the more users there are, the higher the availability of the network.
</p>
<br/>
<div style="clear:both"></div>

<h2>Balance - it's key</h2>
<p style="text-align:justify;"> There are a number of potential issues with the current system, firstly keeping track of which hosts are up/down when a new user joins the system. This shouldn't be a big problem because the three seeds nodes should be up all the time and one node going down will hopefully still allow for new users to bootstrap successfully.<br/><br/> The next problem is balancing the data with the incrementing replication factor. From the above diagram it's clear that the ring isn't well balanced and with new users joining the ring, it will become even less balanced. Currently the argument for "don't worry, it'll be ok" is that each node holds 100% of the data, so balanced or not, it doesn't matter if a node goes down (its expected for nodes to go down as people using the system will switch their machines off) the data will still be available.
</p>

<br/>
