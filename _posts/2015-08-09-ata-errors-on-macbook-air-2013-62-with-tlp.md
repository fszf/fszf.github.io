---
id: 483
title: ATA errors on macbook air 2013 6,2 with TLP after suspend/resume
date: 2015-08-09T19:30:49+00:00
author: Frank S
layout: post
guid: http://frankshin.com/?p=483
permalink: /ata-errors-on-macbook-air-2013-62-with-tlp/
mashsb_timestamp:
  - "1480522080"
mashsb_shares:
  - "0"
mashsb_jsonshares:
  - '{"total":0}'
dsq_thread_id:
  - "4018440130"
categories:
  - Linux
  - Macbook Air
tags:
  - archlinux
  - ata error
  - macbook air
  - suspend
---
I haven't checked my dmesg in awhile and when I did, I was shocked to see it flood with ATA errors.  The errors look similar to:
<pre><code>[  +0.000001] ata1.00: status: { DRDY }
[  +0.000003] ata1: hard resetting link
[  +0.719684] ata1: SATA link up 3.0 Gbps (SStatus 123 SControl 320)
[  +0.000465] ata1.00: unexpected _GTF length (8)
[  +0.000546] ata1.00: unexpected _GTF length (8)
[  +0.000073] ata1.00: configured for UDMA/133
[  +0.000110] ata1: EH complete
[  +4.384538] ata1.00: exception Emask 0x10 SAct 0x80000 SErr 0x4040000 action 0xe frozen
[  +0.000004] ata1.00: irq_stat 0x80000040, connection status changed
</code></pre>
Keep in mind that I had turned off NCQ by putting libata.force=1:noncq in grub as per user <a href="https://bbs.archlinux.org/viewtopic.php?pid=1295212#p1295212">Yesbabyyes on the arch forums</a>.  Upon careful reading of the dmesg errors I saw that the SATA link was connecting at 6.0 Gbps to 3.0 Gbps to 1.5 Gbps.  So I tried manually setting the link speed to 1.5 Gbps by default with libata.force=1:1.5G,noncq but this didn't resolve the issue.  I googled around and read countless documents with search terms of "ata error after suspend" and likewise.  The links in the references were ones that shoved me toward a better understanding of the issue and finally a fix on TLP's github issue tracker.

The solution is quite simple.  You need to comment out 1 line in /usr/sbin/tlp.
<pre><code># set_sata_link_power $1</code></pre>
References:

https://github.com/linrunner/TLP/issues/59

https://help.ubuntu.com/community/MacBookAir6-2/Trusty

https://ata.wiki.kernel.org/index.php/Known_issues

https://bugzilla.redhat.com/show_bug.cgi?id=672723

http://forums.linuxmint.com/viewtopic.php?f=49&amp;t=165237

&nbsp;