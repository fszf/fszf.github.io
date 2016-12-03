---
id: 38
title: 'Archlinux &#8211; Exploring Into Tiling Window Managers'
date: 2014-01-16T23:45:11+00:00
author: Frank S
layout: post
guid: http://www.frankshin.com/?p=38
permalink: /archlinux-exploring-into-tiling-window-manager/
bwps_enable_ssl:
  - ""
dsq_thread_id:
  - "3459483643"
mashsb_shares:
  - "0"
mashsb_timestamp:
  - "1480739538"
mashsb_jsonshares:
  - '{"total":0}'
categories:
  - Linux
---
Mainstream linux news is filled with updates to <a href="https://wiki.archlinux.org/index.php/Desktop_Environarchlinux-moving-into-a-tiling-window-managerment">desktop environments(DE)</a> like Gnome, KDE, Cinnamon, Unity, XFCE, LXDE, etc.  As a newcomer to the linux world, these DEs are the only choices I had to try.  Each one has its advantages and disadvantages such as ram overhead of simply running the DE to the choice of preferred apps they utilize GTK vs QT.  But that is not the point of discussion for this post!

This all changed when I began to lurk more in the Contributions &amp; Discussion area of the <a href="https://bbs.archlinux.org/index.php">Archlinux Forums</a>.  This is an area where Arch users share their desktop configurations, what apps they use for browsing, editing, file management, etc.  In addition to all that, this is where they freely share a screenshot of their desktop and how they configured it.  Obviously, many of the screenshots posted looked amazing and then I started noticing a trend emerging.  There is a great number of Arch users who are running with only a windows manager.
<p style="text-align: center;"><a style="color: #007ea6;" href="http://frankshin.com/wp-content/uploads/2014/01/same_old_same_old_by_earspl1t-d6w3s131.png"><img class="wp-image-52 aligncenter" style="margin-top: 25.3125px; margin-bottom: 25.3125px; border: 1px solid black;" title="Screenshot by Earsplit on Archlinux Forum" alt="Screenshot by Earsplit on Archlinux Forum" src="http://frankshin.com/wp-content/uploads/2014/01/same_old_same_old_by_earspl1t-d6w3s131.png" width="236" height="133" /></a></p>
The above screenshot is from Earsplit running BSPWM.  There are many screenshots from different tiling WMs such as i3, awesome, xmonad, dwm, etc etc the list literally goes on and on.  At that time I was deciding which one to install and learn from so I digged around asking various members of the forum why they use the tiling WM that they use.

The bottom line is that all of them are great and people move around between different tiling window managers.  Well, that didn't really help in choosing a tiling WM.  The best solution possible was to download them all and fire it up, which highlights Archlinux's flexibility in changing the userland to whatever you want.

The first of these that I tried and mostly stuck with is DWM. Here is a quote from the <a href="http://dwm.suckless.org/">suckless website</a>:
<ul>
	<li>dwm is only a single binary, and its source code is intended to never exceed 2000 SLOC.</li>
</ul>
<ul>
	<li>dwm is customized through editing its source code, which makes it extremely fast and secure - it does not process any input data which isn’t known at compile time, except window titles and status text read from the root window’s name. You don’t have to learn Lua/sh/ruby or some weird configuration file format (like X resource files), beside C, to customize it for your needs: you only have to learn C (at least in order to edit the header file).</li>
</ul>
These two bullet points really struck my interest.  As a linux hobbyist and enthusiast, this provided a playground to potentially create/modify some patches in C language.  The additional benefit of being fast and secure was the cream topping.  I have been using DWM casually for half a year and as my main WM for a few months now.

I also watched JasonWRyan's introduction video to DWM, where he did an excellent job in showcasing DWM's basic functionality as well as some great patches that add extra functions.

&nbsp;
<iframe src="//www.youtube.com/embed/GQ5s6T25jCc" height="315" width="420" allowfullscreen="" frameborder="0"></iframe>