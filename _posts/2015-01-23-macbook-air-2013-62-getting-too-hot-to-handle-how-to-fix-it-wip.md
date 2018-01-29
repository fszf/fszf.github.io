---
title: 'Macbook Air 2013 (6,2) Getting too hot to handle &#8211; How to fix it (WIP)'
date: 2015-01-23T19:00:56+00:00
author: Frank S
layout: post
---
<span style="color: #ff0000;"><strong>Edit: Feb 27, 2015 - <a style="color: #ff0000;" href="http://frankshin.com/macbook-air-2013-62-better-battery-life-in-arch-linux/">Battery saving post is UP!</a></strong></span>

<span style="color: #ff0000;">EDIT: Feb 14, 2015 - The below is my journal of what appeared to be an issue created with the yosemite firmware.  The final solution was to suppress the gpeXX that were creating an ACPI shit storm.  I do not use thermald, pstate-frequency-git, and macfanctld.  There will be an updated post this week, which I will link here, on how to optimize your battery life in Archlinux.  Stay tuned!</span>

&nbsp;

A few weeks ago, I decided to reinstall Mac OSX Yosemite and instead of a standalone install of Arch, I dual booted.  That way, my wife won't flip out at me when she tries to use my laptop.  I find that Mac OSX had better battery life by a couple hours and ran under cooler temps.  So what do I do?  I start looking at my options.

First, I installed <a href="https://www.archlinux.org/packages/?name=cpupower">cpupower</a> which is "a set of userspace utilities designed to assist with CPU frequency scaling. The package is not required to use scaling, but is highly recommended because it provides useful command-line utilities and a <a title="Systemd" href="https://wiki.archlinux.org/index.php/Systemd">systemd</a> service to change the governor at boot." - <a href="https://wiki.archlinux.org/index.php/CPU_frequency_scaling#cpupower">Archwiki</a>  I tried setting the governor to powersave and setting the min max frequencies but for some reason, it had little effect on temp and frequency control.

Then I used <a href="https://aur.archlinux.org/packages/i7z-git/">i7z-git</a> from AUR which is a very detailed monitoring system.  This is what I have running in the background to check my tests.

So while browsing the archlinux forums, I came across a few <a href="https://bbs.archlinux.org/viewtopic.php?id=169525">discussions</a> about <a href="https://wiki.archlinux.org/index.php/CPU_frequency_scaling#thermald">thermald</a>, which is "a Linux daemon used to prevent the overheating of platforms. This daemon monitors temperature and applies compensation using available cooling methods." -Archwiki.  Although thermald has run nicely for others out of the box without any extra configurations, for our MBA it had little effect.  Temps still idled around 78-84 for normal web browsing.

I then read about <a href="https://aur.archlinux.org/packages/macfanctld-git/">macfanctld</a> (automatic fan control based on temp for intel macs).  As soon as I started the systemd service, the fans kicked in and tried to bring down the temps.  However, the root cause so far by looking at i7z was that the frequency was always hovering at max (2.6GHz in our case).

I then decided to do a blind look in AUR for our cpu frequency driver, intel pstate.  A quick search brought me to <a href="https://aur.archlinux.org/packages/pstate-frequency-git/">pstate-frequency-git</a> and I checked out the upstream link to the author's github which yielded some very nice <a href="https://github.com/pyamsoft/pstate-frequency">documentation</a>.  Finally, I found something that could control the cpu frequencies the way I want.  Albeit there is still some more tweaking left, my temps immediately dropped 20C and were now in the 50's-60's.  This post is a work in progress and I journey towards the nirvana of temp control and battery life without sacrificing performance.  Please feel free to share your own tips or tricks, perhaps one of them will be the key I am looking for.
<h3>Addendum #1 January 25 Sunday:</h3>
After going through and trying out all the possible solutions, the journey was tiresome.  I came across a dialogue on the <a href="https://bbs.archlinux.org/viewtopic.php?id=166623">Archforums</a> and learned more about pstate driver and the c0-&gt;c7 cpu state.  That took me right away to powertop.  In powertop I then realized something.  My cpu was in c0% from 99%-100% of the time!!  In powertop the acpi was producing over 10,000 events per second - yikes!  Kworker was going bat shit crazy due to acpi as well.  Oh no.  Googling around for acpi+events+macbook got me to find that this was due to acpi interrupts for macbooks that have upgraded their Mac OSX to yosemite.  No wonder I didn't remember this issue as I immediately removed Mavericks when I first got the MBA.

The <a href="https://wiki.archlinux.org/index.php/MacBook#kworker_using_high_CPU">macbook archwiki</a> then confirmed all of this research.

I ran:

<code>grep . -r /sys/firmware/acpi/interrupts/</code>

Then I scrolled up and saw that interrupt gpe66 had over 10,000 interrupts. This was the culprit! However, disabling it would prove to be challenging. I tried crontab commands to start at reboot, manually doing it, and everything in between. I was desperate at this point to disable this ill begotton son of interrupt.

Thankfully <a href="http://loicpefferkorn.net/2015/01/arch-linux-on-macbook-pro-retina-2014-with-dm-crypt-lvm-and-suspend-to-disk/">some dude, who blogged his own adventures in Archlinux with his Macbook Pro,</a> posted his solution, which was to create a service for systemd.  As an addition, I found that gpe4E also needed to be muted.  You can download both <a href="https://github.com/frank604/configs/tree/master/system">service files from my github</a>.

Also, <a href="https://bbs.archlinux.org/viewtopic.php?pid=1497798#p1497798">step-2 from the archforums </a>mentioned that Yosemite has an update to 10.10.2 which resolves this issue.  For dual booters, this is a good fix but for Arch only installs, the service method is the best bet.  Unless you want to reinstall mac osx.

One thing to note is, gpe4E was still creating a lot of interrupts, even with the 10.10.2 update but gpe66 was fixed.  So, keep in mind to monitor your system with the grep command above, and apply this bandaid as needed.

His service is:
<code># /etc/systemd/system/suppress-gpe66.service</code>

<code>[Unit]
Description=Disables GPE 66, an interrupt that is going crazy on Macs</code>

<code>[Service]
ExecStart=/usr/bin/bash -c 'echo "disable" &gt; /sys/firmware/acpi/interrupts/gpe66'</code>

<code>[Install]
WantedBy=multi-user.target</code>

&nbsp;
