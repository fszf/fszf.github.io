---
id: 367
title: Domain Expired And DNS Troubles/Optimization
date: 2015-02-02T19:03:56+00:00
author: Frank S
layout: post
guid: http://frankshin.com/?p=367
permalink: /domain-expired-dns-troublesoptimization/
dsq_thread_id:
  - "3480113841"
mashsb_shares:
  - "0"
mashsb_timestamp:
  - "1480521987"
mashsb_jsonshares:
  - '{"total":0}'
categories:
  - Linux
tags:
  - dns
  - domain
  - linux
  - server
---
<a href="http://frankshin.com/wp-content/uploads/2015/02/server-down-it-was-aliens.jpg"><img class=" size-medium wp-image-368 aligncenter" src="http://frankshin.com/wp-content/uploads/2015/02/server-down-it-was-aliens-300x263.jpg" alt="server-down-it-was-aliens" width="300" height="263" /></a>

Last night something dreadful happened.  My website was inaccessible! This was strange as my server was still pingable and I was able to ssh in and see that it was running fine.  A WHOIS showed that yesterday was the expiration date for my domain.  It's a long story but let's just say this was a very time consuming experience where I hope to rectify it so that I won't have to go through this again.  Apparently all the other DNS resolvers updated my domain but I was on my ISP's and it was not updated.

While the rest of the DNS resolvers propagate my domain information, let's talk about DNS!

&nbsp;

&nbsp;
<h3>DNS Resolvers</h3>
<a href="http://frankshin.com/wp-content/uploads/2015/02/demo.png"><img class=" size-medium wp-image-369 aligncenter" src="http://frankshin.com/wp-content/uploads/2015/02/demo-300x179.png" alt="demo" width="300" height="179" /></a>Have you heard of openDNS, openNIC, Google DNS, and Comodo?  They are alternative DNS resolvers that you can use.  In <a href="https://wiki.archlinux.org/index.php/Resolv.conf">Archlinux, we can simply modify /etc/resolv.conf </a>and add at the top of the list
<pre><code>nameserver 8.8.8.8
nameserver 8.8.4.4</code></pre>
<p style="text-align: left;">This would automatically connect you to Google's DNS resolver, which in fact is one of the best free alternatives.  I ran a tool called namebench.  <a href="https://code.google.com/p/namebench/">Google Link</a> and <a href="https://aur.archlinux.org/packages/namebench/">AUR Link</a>.</p>
<p style="text-align: left;">Using namebench showed that the promised faster host name lookup from openDNS was false, at least for me.  Use the tool and check out which nameserver you should use.</p>