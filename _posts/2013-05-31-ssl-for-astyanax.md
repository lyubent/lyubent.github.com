---
layout: default
title: "SSL for Astyanax"
published: false
---
<p>Security is important for any application that handles personal data and one of the most common ways of protecting the wire is through the use of SSL. Because of my struggle to setup client- server SSL I though I'd share what I learned in the form of a brief tutorial on the steps necessary to implement client-server security between Cassandra and the Astyanax client.
</p>
<h2>Firstly to clarify the terms used.</h2>
<p>Astyanax - A high-level, thrift based Java API for Cassandra.<br/>
Java Keystore (JKS) - A file that stores private keys, and the certificates with their corresponding public keys.<br/>
Java Truststore (JTS) - Another file that contains certificates from other parties that you expect to communicate with, or from Certificate Authorities that you trust to identify other parties.<br/>
Keytool - A key and certificate management utility allowing for creation and signing of certificate stores.<br/>
Secure Sockets Layer (SSL) - cryptographic protocol that provides communication security over the Internet.<br/>
</p>
<h2>Creating the Necessary Certificates</h2>
<p>
The simplest guide out there was Acunu's guide to Cassandra security. The section headed 'Cassandra client certificates' contains detailed information and explanation on the various keytool commands used to generate the necessary certificate stores and are the source of the below snippet of code outlining the process:
<br/>
<script src="https://gist.github.com/lyubent/5664185.js"></script>
</p>
<p>
<h2>Configuring Cassandra to use SSL</h2>
The configuration takes place in the cassandra.yaml file located in casandradir/conf/ 
We are after the following option client_encryption_options (typically located near the bottom of the file) which should be modified to the below snippet:
<br/><br/>
<script src="https://gist.github.com/lyubent/5664276.js"></script>
</p>
<p>
<h2>Enabling SSL in the Astyanax client</h2>
To allow Astyanax to communicate with Cassandra the password and path to the certificate store has to be supplied when creating the Astyanax context. 
<br/>
The file containing the certificate store, based on the above certificate generation example, is "cassandra_external_trust.jks".
<br/>
Within the creation of the Astyanax context, in the withConnectionPoolConfiguration method we call setSSLConnectionContext to enable SSL and pass a SSLConnectionContext object as a parameter. The object requires two parameters, the part to the certificate store and the store’s password:
<br/><br/>
<script src="https://gist.github.com/lyubent/5664395.js"></script>
<br/>
And now our communication channel is protected by encryption via SSL. The below two screen shots of Wireshark will hopefully demonstrate why it's a good idea to protect your communication channel.
</p>
<h3>Regular Thrift traffic</h3>
<img width="800" height="600" src="/images/noencryption.png" alt="Unencrypted thrift traffic with human-readable sensitive data">
<h3>Encrypted Thrift traffic</h3>
<img width="800" height="600" src="/images/encryption.png" alt="Encrypted thrift traffic with scrambled data that is uncreadable by anyone who doesn't hold the private key.">
