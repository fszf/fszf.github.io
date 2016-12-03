---
title: Macbook Air 6,2 (2013) Setting it up with Archlinux
date: 2014-01-18T19:09:36+00:00
layout: post
---
<h2>Changelog</h2>
September 6 2015
<ul>
	<li>added acpi_osi= to kernel command</li>
</ul>
January 29 2015
<ul>
	<li>Updated synaptics</li>
</ul>
<strong>January 24 2014</strong>
<ul>
	<li>Fixed a few errors</li>
</ul>
<strong>March 9 2014</strong>
<ul>
	<li>Added ICC profiles back from the macos</li>
</ul>
<strong>February 11 2014</strong>
<ul>
	<li>Added 20-intel.conf to /etc/X11/xorg.conf.d</li>
</ul>
<strong>January 22 2014</strong>
<ul>
	<li>Added /etc/modprobe.d/hid_apple.conf to fix the tilde and set right keyboard</li>
	<li>Removed tilde xmodmap</li>
</ul>
<strong>January 19 2014</strong>
<ul>
	<li>Suspend/Resume fixed by <a href="https://github.com/patjak/mba6x_bl">patjak</a>.  Please report bugs issues to his git hub and give him thanks!  This is experimental so please do not install unless you are willing to take a risk.</li>
	<li>Updated .xbindkeysrc - bind F3 and F4</li>
</ul>
<strong>January 18 2014</strong>
<ul>
	<li>Originally, this post's content was in my <a href="http://www.frankshin.com/installing-archlinux-on-macbook-air-2013/">previous post here</a>.  However, the length grew as more items were added to the list.  Below you will find my most current setup/tips.</li>
</ul>
<h3>Credit:</h3>
Written below is a grouping of information spread out across the forums, wiki, and personal experience in implementing them.  I provided a step by step instruction for the lazy.  However, please be aware of what each implementation does prior by reading the wiki or google-fu.
<h3>Wifi</h3>
I have used both <a href="https://aur.archlinux.org/packages/broadcom-wl/">broadcom-wl</a> and <a href="https://aur.archlinux.org/packages/broadcom-wl-no-dkms/">broadcom-wl-no-dkms</a>.  They both worked for me.  However, I am currently on broadcom-wl as broadcom-wl-no-dkms has no maintainer.  For initial wifi, I tethered my android device (note 2) via usb and internet worked out of box for me.  Then I manually installed the broadcom-wl.  Please note, the version of the .pkg.tar.xz may differ as new versions are pushed.
<pre>wget broadcom-wl.tar.gz https://aur.archlinux.org/packages/br/broadcom-wl/broadcom-wl.tar.gz
tar -xvf broadcom-wl.tar.gz
cd broadcom-wl
makepkg -s
pacman -U broadcom-wl-6.30.223.141-4-x86_64.pkg.tar.xz</pre>
<h3>Audio</h3>
Legogris from the Arch Forums posted his /etc/asound.conf and on a base system with only alsa (no pulse), I was able to get sound working perfectly out of box with this config:
<pre>defaults.pcm.card 1
defaults.pcm.device 0
defaults.ctl.card 1

Edit: I realized that many steam games needed pulse, so I removed the asound.conf I wrote above</pre>
<h3>Trackpad</h3>
Use <a href="https://github.com/frank604/configs/tree/master/xorg">two synaptic files from my github</a>.  The setup makes it so that you must click the bottom buttons with two fingers to do a right click.  I found that without this, just two finger presses on the trackpad was triggering a right click - quite annoying~!

<del>The trackpad works out of box with the regular synaptics package.  I modified the default /etc/X11/xorg.conf.d/50-synaptics.conf to have natural scrolling and some palm detection.  3+ finger motions do not work out of box but I read that with some tweaking you can get the same gestures like mac osx.</del>
<pre><del>Section "InputClass"
Identifier "touchpad catchall"
Driver "synaptics"
...
Option "VertScrollDelta" "-111"
Option "HorizScrollDelta" "-111"
Option "PalmDetect" "1"
Option "PalmMinWidth" "20"
Option "PalmMinZ" "200"
EndSection</del></pre>
<h3>Kernel Parameters</h3>
<blockquote>Note: The below steps are valid if your <a href="http://www.frankshin.com/installing-archlinux-on-macbook-air-2013/">installation process is same as mine</a>.</blockquote>
I edited the /etc/default/grub line 4 to show the following
<pre>GRUB_CMDLINE_LINUX_DEFAULT="quiet acpi_osi= libata.force=1:noncq i195.i195_enable_rc6=1 resume=/dev/sda3</pre>
You can take out the 'quiet' parameter for debugging.  The only must haves from above for my setup are the libata.force=1:noncq and resume=/dev/sda3.

I added in the 'acpi_osi=' due to a kernel issue with darwin.  This is supposed to help battery life.

I regenerate grub.cfg by running a script but you can just run it yourself <strong>(this is for the Archonly configuration!!)</strong>
<pre>sudo grub-mkconfig -o /boot/efi/EFI/grub/grub.cfg
sudo cp /boot/efi/EFI/grub/grub.cfg /boot/grub/grub.cfg</pre>
I regenerate grub.cfg by running a script but you can just run it yourself <strong>(this is for the dual-boot configuration!!)</strong>
<pre>sudo grub-mkconfig -o /boot//grub/grub.cfg
</pre>
<h3>Suspend/Resume Bug</h3>
<pre><strong>Note: The suspend bug has been fixed unofficially by <a href="https://github.com/patjak/mba6x_bl">Patjak</a>.  This is experimental and risks are involved.</strong></pre>
<del>Currently as of 1-13-2014, the <a href="https://bugzilla.kernel.org/show_bug.cgi?id=62891">bug</a> still exists where if you suspend and resume, the screen backlight will either be at 0% brightness or 100% brightness depending on value.</del>
<h3>Hibernate Enabling</h3>
To enable hibernate:

Edit /etc/mkinitcpio.conf to add 'resume' hook
<pre>HOOKS="base udev autodetect modconf block resume filesystems keyboard fsck"</pre>
Regenerate initramfs with:
<pre>mkinitcpio -p linux</pre>
<h3><del>Enable hibernate on laptop lid close:</del></h3>
Note: I no longer need this as the suspend bug is fixed.

<del>Edit /etc/systemd/logind.conf</del>
<pre><del>HandleLidSwitch=hibernate</del></pre>
<h3>Multimedia Keys</h3>
In some DEs like gnome/kde/cinnamon, I think the multimedia keys mostly work out of box.  However, if you are only running a WM like DWM you will have to bind them yourself. Make sure to add "xbindkeys" to your .xinitrc or whichever binding program you like.

In your home folder you should create your .xbindkeysrc which should look like this or whatever you want to map it to:
<pre># Decrease monitor backlight by 5%.  Change to value you wish
"xbacklight -dec 5"
m:0x0 + c:232

# Increase monitor backlight by 5%
"xbacklight -inc 5"
m:0x0 + c:233

# requires kbdlight from aur
# keyboard backlight increase
"kbdlight up"
m:0x0 + c:238

# keyboard backlight decrease
"kbdlight down"
m:0x0 + c:237

# Increase volume by 5%
# change to any value you wish
"amixer -c 1 set Master 5%+"
m:0x0 + c:123

# Decrease volume by 5%
"amixer -c 1 set Master 5%-"
m:0x0 + c:122

# Toggle mute/unmute audio
"amixer -c 1 set Master toggle"
m:0x0 + c:121

# Play/pause for ncmpcpp
"ncmpcpp toggle"
m:0x0 + c:172

# play next for ncmpcpp
"ncmpcpp next"
m:0x0 + c:171

# play prev for ncmpcpp
"ncmpcpp prev"
m:0x0 + c:173

You can download <a href="https://aur.archlinux.org/packages/kbdlight/">kbdlight</a> from the AUR and special thanks to hobarrera for making this!  To find out the "m:0x0 + c:122" you can run "xbindkeys -k" and press the key.  Or visit the <a href="https://wiki.archlinux.org/index.php/Xbindkeys">Arch Wiki</a> on this.
</pre>
<h3>~ (missing Tilde key)</h3>
Add /etc/modprobe.d/hid_apple.conf
<pre>options hid_apple iso_layout=0</pre>
&nbsp;

<del>Right now if you press ` or shift+` (~) the output will be &lt; or &gt;.  I just added a simple xmodmap line into my .xinitrc:</del>
<pre><del>xmodmap -e 'keycode 94 = acsiitilde' &amp;</del></pre>
<del>There are other ways around this but I don't need the ` and being able to output ~ without using shift was a two-birds-with-one-stone type of thing for me.</del>

&nbsp;
<h3>Intel Driver issues (Looks like I don't need this anymore)</h3>
<del>On 2/11/2014 I noticed an issue with my intel drivers.  Specifically, if I fullscreen and minimize a youtube video, my screen would go black and unrecoverable.  A hard reboot would be required.  I cannot get into TTY2.</del>

<del>In my Xorg.0.log I would see things like:</del>

<del>(EE) intel(0): sna_mode_redisplay: page flipping failed, disabling CRTC:3 (pipe=0)</del>

<del>So I read the <a href="https://wiki.archlinux.org/index.php/Intel#Choose_acceleration_method">intel driver archwiki</a>, about acceleration modes.  The default is "SNA - (Sandybridge's New Acceleration) is the faster successor for hardware supporting it."  What I needed to set is "UXA - (Unified Acceleration Architecture) is the mature backend that was introduced to support the GEM driver model."</del>

<del>You can read more on the differences at the wiki.</del>

<del>To do the switch I needed to add an Options line in my /etc/X11/xorg.conf.d/20-intel.conf</del>

<del>Section "Device"</del>

<del>Identifier "Intel Graphics"</del>

<del>Driver "intel"</del>

<del>Option "AccelMethod" "uxa"</del>

<del>Option "TearFree" "true"</del>

<del>EndSection</del>

<del> </del>

<del>Please note that I also have an Option for tearfree.  I added that in as some music videos were tearing on youtube.  It resolved it but if you don't need it, you should exclude that in your 20-intel.conf</del>

&nbsp;
<h3>ICC Profiles for Monitor</h3>
Lately I've been staring at my screen and realized the white is REALLY white.  Then I remember'd I made a backup of ICC profiles on Mac OSx before I installed arch.  So, I installed xcalib from AUR and downloaded my backup ICC profiles.  In case you didn't make a backup, you can find them <a href="http://frankshin.com/files/macos/profile.tar">here</a>.

Un tar the file and read the README I wrote in there.  It will provide examples of how to use xcalib and ICC as well as autostart your settings.

&nbsp;
<h3>Cpu Freq / Overheating / Battery Drain</h3>
Continue reading onto my next post about <a href="http://frankshin.com/macbook-air-2013-62-getting-too-hot-to-handle-how-to-fix-it-wip/">cpu frequency control, overheating laptop, and battery drain.</a>
