---
title: Patching DWM (Dynamic Window Manager) with statuscolors
layout: post
---
After you have <a href="https://wiki.archlinux.org/index.php/Dwm">DWM installed </a>and running, the first step in customizing DWM is to patch it.  Today we are going to look at adding in a patch that will enable colours in the statusbar.

Getting the patch:
<ol>
	<li>Go to the suckless <a href="http://dwm.suckless.org/patches/">website</a> to view the available patches.</li>
	<li>Under <em><strong>patches/</strong></em><strong>  </strong><strong></strong>you will see <a href="http://dwm.suckless.org/patches/statuscolors">statuscolor</a></li>
	<li>At the bottom there is a link for <a href="http://dwm.suckless.org/patches/dwm-5.9-statuscolors.diff">dwm-5.9-statuscolors.diff</a></li>
</ol>
Patching format:
<pre><code>cd dwm-directory
git apply path/to/patch.diff</code></pre>
Patching:
<pre>cd ~/dwm/src/dwm6.0 
patch -p1 &lt; ~/dwmpatch/dwm-5.9-statuscolors.diff</pre>
Output:
<pre>patching file config.def.h
Hunk #1 FAILED at 1.
Hunk #2 succeeded at 46 (offset 1 line).
1 out of 2 hunks FAILED -- saving rejects to file config.def.h.rej
patching file dwm.c
Hunk #1 succeeded at 49 (offset 1 line).
Hunk #2 succeeded at 100 (offset 2 line).
Hunk #3 succeeded at 178 (offset 3 line).
Hunk #4 succeeded at 731 (offset -6 line).
Hunk #5 succeeded at 747 (offset -6 line).
Hunk #6 succeeded at 774 (offset -6 line).
Hunk #7 succeeded at 815 (offset -6 line).
Hunk #8 succeeded at 834 (offset -6 line).
Hunk #9 succeeded at 884 (offset -6 line).
Hunk #10 succeeded at 1173 with fuzz 2 (offset 7 line).
Hunk #11 succeeded at 1641 (offset 62 line).
Hunk #12 succeeded at 1804 (offset 60 line).</pre>
Resolved failed hunks:

Hunk #1 failed while patching config.def.h and patch saved the rejects to file config.def.h.rej

config.def.h.rej content:
<pre>--- config.def.h 2011-07-10 16:24:25.000000000 -0400
+++ config.def.h 2011-08-18 02:02:47.033830823 -0400
@@ -1,13 +1,16 @@
/* See LICENSE file for copyright and license details. */

/* appearance */
+#define NUMCOLORS 4 // need at least 3
+static const char colors[NUMCOLORS][ColLast][8] = {
+ // border foreground background
+ { "#cccccc", "#000000", "#cccccc" }, // 0 = normal
+ { "#0066ff", "#ffffff", "#0066ff" }, // 1 = selected
+ { "#0066ff", "#0066ff", "#ffffff" }, // 2 = urgent/warning
+ { "#ff0000", "#ffffff", "#ff0000" }, // 3 = error
+ // add more here
+};
static const char font[] = "-*-terminus-medium-r-*-*-16-*-*-*-*-*-*-*";
-static const char normbordercolor[] = "#cccccc";
-static const char normbgcolor[] = "#cccccc";
-static const char normfgcolor[] = "#000000";
-static const char selbordercolor[] = "#0066ff";
-static const char selbgcolor[] = "#0066ff";
-static const char selfgcolor[] = "#ffffff";
static const unsigned int borderpx = 1; /* border pixel of windows */
static const unsigned int snap = 32; /* snap pixel */
static const Bool showbar = True; /* False means no bar */</pre>
The lines that start with a minus (-) indicate which lines to remove.  The entire Hunk #1 failed because one or more lines weren't found.  This is most likely happening because the dwm version we have is 6.0 and this patch was diff'd against a 5.9 version (just my guess).  That means we need to edit the default config.def.h to match the (-) lines.

Snippet of default config.def.h:
<pre>static const char normbordercolor[] = "#444444";
static const char normbgcolor[] = "#222222";
static const char normfgcolor[] = "#bbbbbb";
static const char selbordercolor[] = "#005577";
static const char selbgcolor[] = "#005577";
static const char selfgcolor[] = "#eeeeee";</pre>
All we need to do is edit the values in the dwm-5.9-statuscolors.diff to match the default config.def.h so replace #cccccc with #444444 and so on and so forth.  Then save the patch as dwm-6.0-statuscolors.diff and then whenever you reinstall DWM and need to patch statuscolors, you can do so without all this hassle.

Keep in mind that some patches can't patch over a pre-patched source, so there is a general order of patches you must follow.  That will be covered at a later time.

Resources:

https://wiki.archlinux.org/index.php/Dwm

<a href="https://bbs.archlinux.org/viewtopic.php?id=92895">DWM Hackers Unite! Share (or request) dwm patches.</a>

&nbsp;
