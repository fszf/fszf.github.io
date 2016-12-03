---
id: 63
title: 'Putty or Kitty &#8211; Changing Color Scheme'
date: 2014-01-18T19:31:39+00:00
author: Frank S
layout: post
guid: http://www.frankshin.com/?p=63
permalink: /putty-changing-color-scheme/
bwps_enable_ssl:
  - ""
dsq_thread_id:
  - "3460899279"
mashsb_shares:
  - "0"
mashsb_timestamp:
  - "1480734266"
mashsb_jsonshares:
  - '{"total":0}'
mashsb_shorturl:
  - ""
categories:
  - Linux
---
My work environment is on windows and often I need to ssh into my server with <a href="http://www.chiark.greenend.org.uk/~sgtatham/putty/">putty</a> (edit: I now use <a href="http://www.9bis.net/kitty/?page=Download">Kitty</a>).  The coloring is determined through the putty color settings and I quickly found that I couldn't look at my terminal without wincing in pain when weird color combinations plague my sight.

A quick google search found a <a href="http://putty.org.ru/themes/index.html">russian site</a> that had really nice color schemes.  You can browse through and find the one that resonates with you.  Personally, I am enjoying the <a href="http://putty.org.ru/themes/chalkboard.html">chalkboard theme</a>.  For fear of having this site go down, I've copied the theme settings below.

&nbsp;

[caption id="attachment_64" align="alignnone" width="667"]<a href="http://frankshin.com/wp-content/uploads/2014/01/chalkboard1.png"><img class="size-full wp-image-64" alt="chalkboard putty color theme" src="http://frankshin.com/wp-content/uploads/2014/01/chalkboard1.png" width="667" height="335" /></a> http://putty.org.ru/themes/index.html[/caption]

[caption id="attachment_65" align="alignnone" width="837"]<a href="http://frankshin.com/wp-content/uploads/2014/01/puttychalkboardcode1.png"><img class="size-full wp-image-65" alt="putty chalkboard code" src="http://frankshin.com/wp-content/uploads/2014/01/puttychalkboardcode1.png" width="837" height="333" /></a> http://putty.org.ru/themes/index.html[/caption]

&nbsp;

I've now switched to the <a href="http://dotshare.it/dots/659/">Kasugano </a>colour theme.  I've converted the hex colours to RGB below:
<pre>URxvt.background: #1b1b1b 27-27-27
URxvt.foreground: #FFFFFF 255-255-255
URxvt.colorBD: #CFCFCF 207-207-207
URxvt.colorUL: #969696 150-150-150
URxvt.colorIT: #686868 104-104-104
!Black
*color0: #3D3D3D 61-61-61
*color8: #4D4D4D 77-77-77
!Red
*color1: #6673BF 102-115-191
*color9: #899AFF 137-154-255
!Green
*color2: #3EA290 62-162-144
*color10: #52AD91 82-173-145
!Yellow
*color3: #B0EAD9 176-234-217
*color11: #98C9BB 152-201-187
!Blue
*color4: #31658C 49-101-140
*color12: #477AB3 71-122-179
!Magenta
*color5: #596196 89-97-150
*color13: #7882BF 120-130-191
!Cyan
*color6: #8292B2 130-146-178
*color14: #95A7CC 149-167-204
!White
*color7: #C8CACC 200-202-204
*color15: #EDEFF2 237-239-242</pre>