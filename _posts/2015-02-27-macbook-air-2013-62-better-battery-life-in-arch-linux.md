---
title: 'Macbook Air 2013 6,2 &#8211; Better battery life in Arch Linux'
date: 2015-02-27T09:55:56+00:00
author: Frank S
layout: post
---
<a href="http://frankshin.com/wp-content/uploads/2015/02/battery.jpg"><img class=" size-medium wp-image-444 aligncenter" src="http://frankshin.com/wp-content/uploads/2015/02/battery-300x168.jpg" alt="battery life" width="300" height="168" /></a>

&nbsp;
<h3>Better Battery Life in Arch Linux (Macbook Air 2013 6,2)</h3>
For those that have spent some time using the Macbook Air in OSX, you probably were fond of the 11+ hours of battery life.  I for one enjoyed not having to be a battery-watcher.  As with all laptops and linux, this combination will never provide as much battery life as Apple's OSX.  However, fear not!  We can get as close to it as possible.

<strong>Battery life in linux during the writing of this post: 10% =~55min</strong>

<span style="color: #993300;">Disclaimer #1: I am fairly new at understanding all the little pieces that help save power so if you feel something I wrote about is incorrect or have a better way in doing it, please let me know!  This post is mostly for my understanding and recording my findings, but felt others could benefit from it.</span>

<span style="color: #993300;">Disclaimer #2: Do not blindly copy paste what I have written here.  Seek to understand it even if I don't.</span>
<h3>Step 1: Read The F***'n Manual</h3>
The <a href="https://wiki.archlinux.org/index.php/Power_saving">Power Saving Archwiki</a> is a perfect start, where it shows how to create udev scripts and modify kernel parameters via sysctl.d.  Due to Step 2 of this post, I've removed all of these suggestions from the wiki.  However, if you wish, I've saved them in <a href="https://github.com/frank604/configs">my github</a>.
<h3>Step 2: Powertop Service</h3>
I just enable this service.
<pre><code>
[Unit]
Description=Powertop tunings

[Service]
Type=oneshot
ExecStart=/usr/bin/powertop --auto-tune

[Install]
WantedBy=multi-user.target</code></pre>
<h3>Step 3: TLP</h3>
Read the <a href="https://wiki.archlinux.org/index.php/TLP">TLP archwiki</a> and get it installed.

Configure /etc/default/tlp to your preferred setting.  I don't control the cpu freqs as that will be done in step 4.  I also use linux-ck so instead of selecting an IO scheduler I leave it commented out.  CK patchset uses BFQ.  Go take a look at <a href="https://wiki.archlinux.org/index.php/repo-ck">graysky's repo</a> if you wish to use the CK patched kernel.

<a href="https://github.com/frank604/configs/blob/master/default/tlp">A TLP config I am working on is on my github</a>.

Note: I had to edit TLP which was causing an ATA error after suspend.  Read about it <a href="http://frankshin.com/ata-errors-on-macbook-air-2013-62-with-tlp/">here</a>.
<h3><del>Step 4: pstate-frequency-git (AUR)</del></h3>
<del><a href="https://aur.archlinux.org/packages/pstate-frequency-git">Install pstate-frequency-git from AUR</a>.  This is a handy tool to help control cpu governor, cpu frequency, and turbo boost.  For normal day to day stuff leaving it at powersave plan works best for me.  That is a min/max of 30% cpu frequency which is 800mhz and no turboboost.  When I do something heavier besides browsing, music, weechat, etc. like compiling, then I would bump it to the performance plan.  Optionally you can stay in powersave and just increase cpu max from 30% to 100% and enable turbo.  Create aliases in your shell for these manual changes.  Automatically via udev, this will go from powersave plan on batt and performance plan on ac.</del>

<del>To see how to use pstate-frequency, <a href="https://github.com/pyamsoft/pstate-frequency">visit the upstream github page with syntax and info here</a>.</del>
<h3>Step 4: Get thermald and macfanctld</h3>
Install both items from AUR.
<h3>Step 5: add 'acpi_osi=' to kernel boot option</h3>
Add to /etc/default/grub
<h3>Conclusion</h3>
That's it!  The battery life with this setup is not on par with mac osx but it brings enough life where I'm not constantly worrying about the battery life.  It also keeps my MBA cool like a pickle.  I used to use powerdown but realized development stopped awhile ago.  TLP was mentioned to me by Iamikon, so thanks brother for letting me check this out.  As always, if you guys feel like there is something better out there, please share!

&nbsp;

&nbsp;
