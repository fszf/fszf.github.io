---
title: Installing Archlinux on Dell XPS 13 2016 Skylake 9350
date: 2015-11-11T20:58:25+00:00
author: Frank S
layout: post
---
<a href="http://frankshin.com/wp-content/uploads/2015/11/dell-xps-13-2015-product-photos-01.jpg"><img class="size-medium wp-image-547" src="http://frankshin.com/wp-content/uploads/2015/11/dell-xps-13-2015-product-photos-01-300x169.jpg" alt="dell-xps-13-2015-archlinux" width="300" height="169" /></a> 

<h3>Changelog</h3>
<ul>
	<li>
<h3><span style="color: #ff0000;">January 29 2015 - Please visit the archlinux page for updated information.  My xps 13 is <a style="color: #ff0000;" href="http://frankshin.com/dell-xps13-great-product-but-service-needs-serious-improvements/">no longer in my possession since December 9th 2015 </a>so I have been unable to update this page.</span></h3>
</li>
	<li><span style="color: #800080;">November 24 2015 - White noise fix patched.  Incoming to 4.4-rc3 or via my github</span></li>
	<li><span style="color: #800080;">November 19 2015 - Github updated with 4.4-rc1 kernel</span></li>
	<li><span style="color: #800080;">November 17 2015 - Added Archlinux Forum link for our device and a bugzilla bug report for white noise</span></li>
	<li><span style="color: #0000ff;"><span style="color: #800080;">November 14 2015 - Added troubleshooting section, references, and a link to my dell xps 13 9350 github</span>
</span></li>
</ul>
<h3></h3>
<h3>Installation of Archlinux on Dell XPS 13 late 2015 skylake 9350</h3>
<span style="color: #ff0000;">Disclaimer:  I just went through a day of installation as there were some unforeseen situations.  Therefore, the information here is written down from memory.  I will update as I remember more.</span>
<h4>1. USB installer</h4>
I've always carried an updated archlinux iso on my Drive Droid (android app) so this is what I used.  However, you can alternatively use <a href="https://wiki.archlinux.org/index.php/USB_flash_installation_media#In_Windows">rufus and usbwriter</a> from windows.
<h4>2. Bios Settings</h4>
Keyboard shortcuts:

F2 = Enter setup

F12 = Select boot device

Enter into setup and ensure these settings are in place:

General -&gt; Boot Sequence = UEFI (Choose Legacy just for booting off usb arch iso if you have problems, just remember to switch back to UEFI when done)

General -&gt; Advance Boot Options = Checked Enabled Legacy Options ROMs, uncheck Enable UEFI Network Stack

System Configuration -&gt; SATA Operation = Disabled

Secure Boot = Disabled

POST Behavior = Fastboot = Minimal (this is so that systemd-boot can show menu)
<h4>3. Partition</h4>
Depending on which SDD you selected you may or may not see the nvme partitions.  I have them and this is what I have.  I used cfdisk.

nvme0n1p1 vfat /boot

nvme0n1p3 ext4 rest of disc
<h4>4. Boot Loader (from <a href="https://wiki.archlinux.org/index.php/Beginners'_guide#Install_a_boot_loader">archwiki</a>)</h4>
<h3><span id="Install_a_boot_loader" class="mw-headline">Install a boot loader</span></h3>
See <a title="Boot loaders" href="https://wiki.archlinux.org/index.php/Boot_loaders">Boot loaders</a> for available choices and configurations. If you have an Intel CPU, install the <span class="plainlinks archwiki-template-pkg"><a class="external text" href="https://www.archlinux.org/packages/?name=intel-ucode" rel="nofollow">intel-ucode</a></span> package, and <a title="Microcode" href="https://wiki.archlinux.org/index.php/Microcode#Enabling_Intel_microcode_updates">enable microcode updates</a>.
<h4><span id="UEFI.2FGPT" class="mw-headline">UEFI/GPT</span></h4>
Here, the installation drive is assumed to be GPT-partioned, and have the <a title="Unified Extensible Firmware Interface" href="https://wiki.archlinux.org/index.php/Unified_Extensible_Firmware_Interface#EFI_System_Partition">EFI System Partition</a> (gdisk type <code>EF00</code>, formatted with FAT32) mounted at <code>/boot</code>.

<i>bootctl</i> is part of systemd, and as such part of the base installation.
<pre># bootctl install
</pre>
Create a boot entry in <code>/boot/loader/entries/arch.conf</code>, replacing <code>/dev/nvme0n1p3</code> with the <b>root</b> partition:
<pre>/boot/loader/entries/arch.conf</pre>
<pre>title          Arch Linux
linux          /vmlinuz-linux
initrd         /initramfs-linux.img
options        root=<b>/dev/nvme0n1p3</b> rw</pre>
Modify <code>/boot/loader/loader.conf</code> to select the default entry (without <code>.conf</code>) suffix:
<pre>/boot/loader/loader.conf</pre>
<pre>timeout 3
default arch</pre>
See <a title="Systemd-boot" href="https://wiki.archlinux.org/index.php/Systemd-boot">systemd-boot</a> for more information.
<h4>5. Follow the rest of the beginner's guide</h4>
<h4><del>6. Install <a href="https://aur.archlinux.org/packages/linux-bcm4350/">linux-bcm4350 from AUR</a></del></h4>
4.4-rc1 is out in testing so I wrote a new pkgbuild in my <a href="https://github.com/frank604/Dell-XPS-13-9350">github</a>.  We no longer need the broadcom patch/bin.

<del>Until kernel 4.4 rolls out we have an unsupported broadcom 4350 chip for wifi.  Fortunately, someone was able to extract the module and created an AUR package for this.  Just remember to add a boot entry for this new kernel.</del>

<del><strong><span style="color: #ff0000;"><a href="https://github.com/frank604/Dell-XPS-13-9350">Note: You can visit my github for a 4.3 testing kernel with patch and .bin</a></span></strong></del>

<del>In /boot/loader/entries:</del>
<pre><del>arch.conf
bcm4350.conf
dell.conf</del></pre>
<del>Cat dell.conf:</del>
<pre><del>title Arch Linux - DELL
linux /vmlinuz-linux-dell
initrd /intel-ucode.img
initrd /initramfs-linux-dell.img
options root=/dev/nvme0n1p3 rw i915.preliminary_hw_support=1 elevator=noop pcie_aspm=force i915.enable_rc6=7 i915.enable_execlists=0</del></pre>
<h4>7. Intel skylake support</h4>
<del>As you can see in my options above, I had to add in i915.preliminary_hw_support=1 to get into X.  Otherwise you'll get some error message saying [EE] can't open /dev/dri doesn't exist.
</del><span style="color: #ff0000;">No longer needed in latest kernels.
</span>
<h2>Troubleshooting</h2>
1. White hissing noise/sound when wearing headphones
<ul>
	<li><del>This was a strange issue for me.  I first had to enable powersaving via TLP to AC and Battery mode.  Then I had to run alsamixer and increase mic volume 1 step from 0.  If the mic volume is at 0, the hissing starts.  There are two sound issues.  This is one.  The second one is that you can hear the EMI interference.  I could not fix this latter issue.</del></li>
	<li>I've written a bug report on <a href="https://bugzilla.kernel.org/show_bug.cgi?id=108081">bugzilla</a>.  Please feel free to participate.</li>
	<li><span style="color: #ff0000;">SOLUTION: white noise patch fixed.  please refer to 0003 patch in my github or wait for 4.4-rc3</span></li>
</ul>
2. DW1820A wifi chip.  Broadcom 4350.  Please download the .bin file from <a href="https://wiki.archlinux.org/index.php/Dell_XPS_13_%282016%29">archwiki</a> and use the patch in bcrm4350 kernel in AUR.

3. Intel video skylake flickering.  Do not use the fbc kernel parameter.

4. Slow bios during reboot = turn off legacy rom in bios (doesn't help much though)  <a href="https://bbs.archlinux.org/viewtopic.php?pid=1579251#p1579251">[credit to SheepOnMeth]</a>

&nbsp;
<h2>References</h2>
I found some interesting reads that you may like:

<a href="https://bbs.archlinux.org/viewtopic.php?id=205147">Dell XPS 13 9350 Archlinux Forum</a>

<a href="https://github.com/frank604/Dell-XPS-13-9350">My dell xps 13 9350 github</a>

<a href="https://wiki.archlinux.org/index.php/Dell_XPS_13_%282016%29">https://wiki.archlinux.org/index.php/Dell_XPS_13_%282016%29</a>

<a href="http://oli.me.uk/2015/11/06/installing-arch-linux-on-a-dell-xps-13-9350/">http://oli.me.uk/2015/11/06/installing-arch-linux-on-a-dell-xps-13-9350/</a>

<a href="https://www.reddit.com/r/Dell/comments/3p4bx8/dell_xps_13_9350_15_9550_linux_support/">https://www.reddit.com/r/Dell/comments/3p4bx8/dell_xps_13_9350_15_9550_linux_support/</a>

<a href="http://nerdjusttyped.blogspot.ca/2015/11/linux-debian-testing-on-dell-xps-13.html">http://nerdjusttyped.blogspot.ca/2015/11/linux-debian-testing-on-dell-xps-13.html</a>

&nbsp;

&nbsp;

&nbsp;
