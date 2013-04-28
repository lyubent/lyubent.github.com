---
layout: default
title: "Setting up C* - OSX vs Windows"
date: "2013-04-28"
categories: ""
tags: ""
---
<br/><h1>TL;DR;</h1>
This post is a quick overview of my experience of trying to build a platform independent application that uses Cassandra (I say platform independent, but what I mean is that Ubuntu, OSX and Win7/8 are supported).
<br/>
<h2>Issues</h2>
<p><ul>
<li><b>Permission</b> - Unix based systems enforce permissions tightly and prevent usage of the <code>/var/log</code> and <code>/var/lib</code> directories without <strong>root</strong> access.</li>
<li><b>System configurations</b> - Windows requires the <code>CASSANDRA_HOME</code> environment variable to be configured.</li>
<li><b>Dependencies</b> - JDK is required for Cassandra so the fact that OSX ships with the developer tools is very handy, however if a specific JDK is required, replacing OSX's default can be problematic.</li>
</ul></p>
<br/><br/>
<h2><strike>Epic Workarounds</strike> Solutions!</h2>
<h3>Permissions</h3>
<p>Since each Casstor uses has a Cassandra node running on their local account it couldn't be expected that users would have root / administrator access so the data directories were placed on the user's desktop.</p><br/>
<h3>System configurations</h3>
<p>Because no environment variables are required by UNIX based systems, there wasn't much of a problem, and for windows the <code>CASSANDRA_HOME</code> variable will be added by a batch file (dos script) using the <code>setx</code> command in two ways, first an attempt is made to set a system level environment variable, if that fails than a user level environment variable is added:<br/>
C:> <code>setx -m CASSANDRA_HOME "C:\Users\%username%\Desktop\cassandra"</code><br/>
C:> <code>setx CASSANDRA_HOME "C:\Users\%username%\Desktop\cassandra</code>
</p><br/>
<h3>Dependencies</h3>
<p>In the windows branch of the application a warning message is displayed that Cassandra will not start if a runtime is unavailable. Also <code>launch4j</code> was used to allow simple JDK downloading if required.</p>
