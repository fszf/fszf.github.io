---
layout: post
title: Hurdles and Moving Forward
---

Who would've known it required quite a few changes to switch from Wordpress to a jekyll site hosted on github.  My domain registrar is Namecheap and I had to delete Digital Ocean's nameserver off the domain.  Create some A names to point to github's servers and a CNAME to the <user>.github.io.  Since the domain wasn't pointing to Digital Ocean, my DO created A name for the subdomain broke.  I had to go back to Namecheap to create an A name so that my subdomain pointed to another
droplet.

### TO DO
1. blog:
    * add search button
    * add tags or category, some way to organize all the posts
    * remove useless posts
    * fix .md formating in imported posts
    * better font?
    * better theme?
    * merge /wordpress to /images

2. migrating:
    * make sure to download all important files from buntu vps
    * delete buntu vps

3. arch vps:
    * mail server
    * other projects?
