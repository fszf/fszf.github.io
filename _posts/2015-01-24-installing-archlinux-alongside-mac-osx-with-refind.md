---
id: 179
title: Installing Archlinux alongside Mac OSX with Refind
date: 2015-01-24T15:21:40+00:00
author: Frank S
layout: post
guid: http://frankshin.com/?p=179
permalink: /installing-archlinux-alongside-mac-osx-with-refind/
dsq_thread_id:
  - "3458628486"
mashsb_shares:
  - "0"
mashsb_timestamp:
  - "1480699046"
mashsb_jsonshares:
  - '{"total":0}'
mashsb_shorturl:
  - ""
image: /wp-content/uploads/2015/01/2015-01-25-000215_1440x900_scrot.png
categories:
  - Macbook Air
tags:
  - archlinux
  - install
  - linux
  - macbook
  - macbook air
---
Last year when I first got my Macbook Air 2013 (6,2) I immediately set off to delete Mac OSX and install a standalone Arch.  I even wrote a post about it <a href="http://frankshin.com/installing-archlinux-on-macbook-air-2013/">here</a>. At that point in time I've never used Mac OSX and wasn't interested in it.  The problem with running an Arch only setup was that my wife would get annoyed because she couldn't use my laptop.  So this winter break I reinstalled Mavericks and upgraded it to Yosemite and set off to do a dual boot setup with Arch.  My first worry was disk space.  I have a 128gb ssd drive on my MBA and splitting it in half would divide my precious data space for music and movies.

This is where the <a href="http://nl.transcend-info.com/apple/jetdrivelite/">Jetdrive</a> comes into play.  It fits snugly in the sdcard port and instantly gives me a share-able drive for data that can be accessed by both OSes.  Watch the video below for more info.

Video: [youtube=https://www.youtube.com/watch?v=j35ydHqCK-4]

So I split the mac partition to be approximately 60g with 60g of free space.  Then <a href="http://sourceforge.net/projects/refind/files/0.8.4/refind-bin-0.8.4.zip/download">download refind-bin-0.8.4.zip</a> from the <a href="http://www.rodsbooks.com/refind/">refind website</a>.  Please note for Mac users on Yosemite that 0.8.4 is the lowest version you can use for this.  Mavericks and below can go ahead and use 0.8.3 if you wish.  Proceed to install refind by unzipping the content and running the install.sh.  I used the default settings and it worked fine.

Reboot with your archlinux usb bootable inserted and the refind menu should pop up with mac osx and the usb bootable.  Boot into the arch installer.

With cgdisk I created three partitions (you can customize this to your preference):
<pre><code>/dev/sda4 = 128M space between mac and arch
/dev/sda5 = 256M for /boot as Linux Filesystem
/dev/sda6 = Rest of drive as Linux Filesystem</code></pre>
Then I formated and mounted:
<pre><code>mkfs.ext2 /dev/sda5
mkfs.ext4 /dev/sda6 </code>

<code>mount /dev/sda6 /mnt
mkdir /mnt/boot</code>

<code>mount /dev/sda5 /mnt/boot
mkdir /mnt/boot/efi</code>

<code>mount /dev/sda1 /mnt/boot/efi</code></pre>
As you can see, I mounted the ESP where refind is installed when we were in mac osx.  I proceeded as normal following the <a href="https://wiki.archlinux.org/index.php/beginners%27_guide">beginner's guide in the archwiki</a> up until the chroot portion.
<pre><code>arch-chroot /mnt
grub-install --target=x86_64-efi --efi-directory=/boot/efi --bootloader-id=arch_grub --recheck --debug
grub-mkconfig -o /boot/grub/grub.cfg </code></pre>
<h3>Changelog:</h3>
March 2, 2015 - Realized there was some text pasted here and there causing confusion.  I've removed them.