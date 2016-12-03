---
title: Installing Archlinux on Macbook Air 2013
date: 2014-01-13T22:49:39+00:00
layout: post
---
<a href="http://frankshin.com/wp-content/uploads/2014/01/FreedomX-1301141.png"><img class="wp-image-32 " src="http://frankshin.com/wp-content/uploads/2014/01/FreedomX-1301141.png" alt="Macbook Air 6,2 Archlinux" width="424" height="265" /></a> 

> Macbook Air 6,2 Archlinux (config from Jason W Ryan @ https://bitbucket.org/jasonwryan)

This Christmas I decided to gift myself a new portable computer as my previous Asus 1005ha was on its deathbed.  When the new 13" mid 2013 Macbook Air arrived, I booted it up for the first time.  Upgraded any firmware needed and backed up the <a href="https://wiki.archlinux.org/index.php/MacBook#Installation_of_Mac_OS_X_and_firmware_update" target="_blank">Mac files as stated in the Arch Wiki</a>.  Also to be noted is to turn down the volume all the way and exit Mac OS X to avoid the chime at boot up.

At first I followed the wiki by installing rEFInd in Mac OS X into the ESP and shrinking the mac partition to make room for a dual boot Arch.  Being new to EFI and rEFInd, I had difficulty passing kernel parameters.  Also, I didn't make a swap partition.  After running this setup for a week, I decided to completely ditch Mac OS X and redo the installation as a pure Arch only installation.
<h2>Ryan Gehrig's Steps</h2>
I stumbled across a wonderful <a href="http://ryangehrig.com/index.php/arch-linux-on-macbook-air-2013/" target="_blank">blog by Ryan Gehrig</a> that described this process.  Thank you Ryan.  This is my first EFI device and to be honest, I was head over heels even after reading wiki after wiki.  For the sake of my own reference, I've copied his process here in this post.  Please note that all installation steps belong to Ryan Gehrig.
<blockquote>I found it very difficult to get Arch booting via EFI as all directions I found were inconsistent. You can also try REFind, as I was able to at least get that to boot up instead of my old broken grub prompt, but I got nowhere with Refind, so I went with reinstalling grub in this article. This is what my system currently uses. No MBR, grub is booted via EFI. For partitioning, you can use a 200MB HFS+ partition to store your EFI data, or you can use FAT32 (vfat). I went the VFAT route and it worked for me, so this guide assumes you have a VFAT partition for EFI, with the scheme like this:</blockquote>
<pre>[root@mac ~]# fdisk -l

Disk /dev/sda: 113 GiB, 121332826112 bytes, 236978176 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 4096 bytes
I/O size (minimum/optimal): 4096 bytes / 4096 bytes
Disklabel type: gpt
Disk identifier: xxxx

Device Start End Size Type
/dev/sda1 2048 411647 200M Microsoft basic data
/dev/sda2 411648 935935 256M Linux filesystem
/dev/sda3 935936 9324543 4G Linux swap
/dev/sda4 9324544 236978142 108.6G Linux filesystem</pre>
<blockquote>I used the following to setup the filesystems:</blockquote>
<pre>mkfs.vfat -F 32 /dev/sda1
mkfs.ext2 /dev/sda2
mkswap /dev/sda3
swapon /dev/sda3
mkfs.ext4 /dev/sda4

mount /dev/sda4 /mnt
mkdir /mnt/boot

mount /dev/sda2 /mnt/boot
mkdir /mnt/boot/efi

mount /dev/sda1 /mnt/boot/efi</pre>
<blockquote>Finish your installation according to the main guide (skipping anything after the bootloader), now chroot into your installation, and setup Grub:</blockquote>
<pre>arch-chroot /mnt

pacman -S grub efibootmgr

# The directory paths are everything here.
mount -t efivarfs efivarfs /sys/firmware/efi/efivars
grub-install --target=x86_64-efi --efi-directory=/boot/efi --bootloader-id=grub --recheck --debug
grub-mkconfig -o /boot/efi/EFI/grub/grub.cfg
cp /boot/efi/EFI/grub/grub.cfg /boot/grub/grub.cfg

# Not necessary but hey, helped me out
# (Frank Edit) I needed to do the below line to make it work
cp /boot/efi/EFI/grub/grubx64.efi /boot/efi/EFI/boot/bootx64.efi</pre>
<blockquote>Note that above, –efi-directory means that grub will append a directory named “EFI” (caps, yes) to whatever you specify. As for –bootloader-id, this gets a directory created in the –efi-directory you specified, so in this example, it’d create the directory /boot/efi/EFI/grub.

If you need to wipe out your MBR for some reason, see this page: https://bbs.archlinux.org/viewtopic.php?id=119702</blockquote>
<h2>Post Installation (Avoid bugs, get wifi, key functions, etc to work)</h2>
Please read the <a href="http://www.frankshin.com/macbook-air-62-2013-setting-it-up-with-archlinux/">next post located here on how to do your post installation setup</a>.

&nbsp;
<h2>Congratulations!</h2>
You just installed Arch Linux on a Macbook Air 6,2 (mid 2013).  As I mentioned above, there is one bug that really affects us and that is the inability to suspend/resume without the brightness bug.  However, if you are running on 100% brightness all the time, this should not affect you.  Although I wrote this mostly for myself in the case that I have to re-install, I hope that it helps the community as well.  Please feel free to share and give credit where due to <a href="http://ryangehrig.com/index.php/arch-linux-on-macbook-air-2013/">Ryan Gehrig</a>. Without his blog post I would have had a damn difficult time getting the EFI part setup.

&nbsp;

Reference:

<a href="https://wiki.archlinux.org/index.php/MacBook">https://wiki.archlinux.org/index.php/MacBook</a>

<a href="https://bbs.archlinux.org/viewtopic.php?id=165899&amp;p=1">https://bbs.archlinux.org/viewtopic.php?id=165899&amp;p=1</a>

<a href="http://ryangehrig.com/index.php/arch-linux-on-macbook-air-2013/">http://ryangehrig.com/index.php/arch-linux-on-macbook-air-2013/</a>
