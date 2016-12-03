---
title: 'DWM (Archlinux) &#8211; Patchset description'
layout: post
---
DWM is designed to be under 2000 SLOC (standard lines of code).  Due to this feature, DWM's flexibility is entrusted to its user, you.  This means, you are free to use it as is, or to patch in whatever features you wish.  The only requirement is that the patch is already written by a community member, or that you write it yourself.  Lately, I'm looking to try different patches together and see what feels "right" for me.  Since there isn't a single library for these patches, some digging around is required.

Resources:
<a style="line-height: 1.5em;" href="http://dwm.suckless.org/patches/">Suckless Patch Site
</a><a style="line-height: 1.5em;" href="https://bbs.archlinux.org/viewtopic.php?id=92895">Archlinux Forum's DWM Patch Thread
</a><a style="line-height: 1.5em;" href="http://www.google.com">Google-fu</a><span style="line-height: 1.5em;"> with search terms similar to "dwm patch" </span>

Current DWM Patchset:
<div>
<ul>
	<li><span style="line-height: 1.5em;">statuscolors</span>
<ul>
	<li>Adds colours to elements in the statusbar.  This will enable colouring of tag names, and text/icons that you pipe to the statusbar</li>
</ul>
</li>
	<li><span style="line-height: 1.5em;">statusallmons</span>
<ul>
	<li>This patch draws and updates the statusbar on all monitors.</li>
</ul>
</li>
	<li><span style="line-height: 1.5em;">centredfloating</span>
<ul>
	<li>Adds 'iscentered' to the DWM Rules.  Values are either True or False.  If True and window is floating, it will center them on vertical and horizontal axis of your screen.  I like this as I can force MPV to open on the center of my screen instead of floating in a corner.  For Gimp, you can set this to False.</li>
</ul>
</li>
	<li><span style="line-height: 1.5em;">savefloats</span>
<ul>
	<li>This patch saves size and position of every floating window before it is forced into tiled mode. If the window is made floating again, the old dimensions will be restored.</li>
	<li>I've always hated the fact when I tile a window and set it to float again and it stays in the same position as if it was tiled.  This can now save it!</li>
</ul>
</li>
	<li><span style="line-height: 1.5em;">notitle</span>
<ul>
	<li>Pretty self explanatory.  No window titles displayed in statusbar at top. Very useful if you have a small screen like I do on my 13" macbook air.</li>
</ul>
</li>
	<li><span style="line-height: 1.5em;">pertag2  </span>
<ul>
	<li><span style="line-height: 1.5em;">Each tag has its own layout, floating, tile, etc!  Some tags are in floating layout like my Media tag and some are tiled as bstack.  Great stuff.</span></li>
</ul>
</li>
	<li><span style="line-height: 1.5em;">systray</span>
<ul>
	<li>Adds a systray feature at the right end of your statusbar.  I have a dropbox, clipboard, and steam showing in the systray.  I may add a connman gui applet if it works soon for roaming networks.  Otherwise netctl-auto really does a good job for me.</li>
</ul>
</li>
	<li><span style="line-height: 1.5em;">occupiedcol</span>
<ul>
	<li>When a tag is occupied, as in a window exists in it, this patch can enable different tag colours.  For example, my unoccupied tags are white.  When they get occupied they turn grey.  The tag I am viewing regardless of being occupied or not is white with a blue underline.</li>
</ul>
</li>
	<li><span style="line-height: 1.5em;">uselessgaps </span>
<ul>
	<li><span style="line-height: 1.5em;">You can customize how big the gaps will be or set it to have zero gaps between windows/screenedge.</span></li>
</ul>
</li>
	<li><span style="line-height: 1.5em;">keysymfix</span>
<ul>
	<li>XKeycodeToKeysym deprecated patch to fix Keysym.</li>
</ul>
</li>
	<li><span style="line-height: 1.5em;">bstack (bottom stack)</span>
<ul>
	<li>Main on top and multiple stacks at bottom layout</li>
</ul>
</li>
	<li><span style="line-height: 1.5em;">runorraise </span>
<ul>
	<li><span style="line-height: 1.5em;">I bind my browser to Modkey + shiftmask + w and if I press the binding it will open my browser or if it is already open it will bring me to the browser!!! Simply amazing</span></li>
</ul>
</li>
	<li><span style="line-height: 1.5em;">Push </span>
<ul>
	<li>Push windows inside a tag up and down</li>
</ul>
</li>
	<li><span style="line-height: 1.5em;">Cycle </span>
<ul>
	<li>Cycle through tags.  I have it set to Modkey + {left,right arrow}</li>
</ul>
</li>
</ul>
</div>
