---
title: Suppressing CFG80211 Errors In Broadcom-wl
date: 2015-01-31T15:09:49+00:00
author: Frank S
layout: post
---
<a href="http://frankshin.com/wp-content/uploads/2015/01/2015-01-31-144257_1440x900_scrot-e1422744216907.png"><img class=" size-medium wp-image-351 aligncenter" src="http://frankshin.com/wp-content/uploads/2015/01/2015-01-31-144257_1440x900_scrot-e1422744216907-300x208.png" alt="cfg80211" width="300" height="208" /></a>
<h3>Annoying cfg80211 Errors In Dmesg/Journalctl</h3>
<pre><code>[ +0.000005] ERROR @wl_cfg80211_get_tx_power : error (-1) [ +1.194918] ERROR @wl_dev_intvar_get : error (-1)
[ +0.000005] ERROR @wl_cfg80211_get_tx_power : error (-1) [ +1.194918] ERROR @wl_dev_intvar_get : error (-1)</code></pre>
For anyone using the proprietary driver, broadcom-wl, you may be spammed by the cfg80211 API error message when it is collecting tx power info, or that's how I read it.  Anyways, this has plagued me for over a year and recently I've finally figured out why this is happening for me but not for many others.

For my dwm statusbar I called iwconfig to grep its ESSID:
<pre><code>
print_wifiqual() {
wifiessid="$(/sbin/iwconfig 2&gt;/dev/null | grep ESSID | cut -d: -f2)"
wifiawk="$(echo $wifiessid | awk -F',' '{gsub(/"/, "", $1); print $1}')"
wificut="$(echo $wifiawk | cut -d' ' -f1)"
echo -ne "${color6}¤${color0}${wificut}"
}</code></pre>
Calling upon iwconfig will always result in the error message and with my statusbar calling upon it every second, you can imagine the flood of errors in my logs which I am now happy to say no longer shows up.

&nbsp;
