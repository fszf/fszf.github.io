---
title: Installing MPD with NCMPCPP on Archlinux
date: 2015-01-26T19:14:43+00:00
author: Frank S
layout: post
---
<h3><a href="http://frankshin.com/wp-content/uploads/2015/01/2015-01-26-191341_1440x900_scrot.png"><img class=" size-medium wp-image-217 aligncenter" src="http://frankshin.com/wp-content/uploads/2015/01/2015-01-26-191341_1440x900_scrot-300x188.png" alt="2015-01-26-191341_1440x900_scrot" width="300" height="188" /></a></h3>
<h3>Installing MPD with NCMPCPP on Archlinux</h3>
"<b><a class="external text" href="http://www.musicpd.org/" rel="nofollow">MPD</a></b> (<b>m</b>usic <b>p</b>layer <b>d</b>aemon) is an audio player that has a server-client architecture. It plays audio files, organizes playlists and maintains a music database all while using very few resources. In order to interface with it, a separate <a href="https://wiki.archlinux.org/index.php/Music_Player_Daemon#Clients">client</a> is needed." - <a href="https://wiki.archlinux.org/index.php/Music_Player_Daemon">Archwiki</a>
<h3>Install MPD-GIT from AUR</h3>
<pre><code> wget https://aur.archlinux.org/packages/mp/mpd-git/mpd-git.tar.gz
tar -xvf mpd-git.tar.gz
cd mpd-git
makepkg -s
sudo pacman -U mpd-git************.pkg.tar.xz</code></pre>
Once that is complete, we have to set it up.  The easiest way to setup mpd is to download <a href="https://wiki.archlinux.org/index.php/Music_Player_Daemon#Scripted_configuration">Rasi's MPD Install Script</a>.  Please remember to enable mpd through systemctl.
<h3>Install NCMPCPP-GIT from AUR</h3>
<pre><code>wget https://aur.archlinux.org/packages/nc/ncmpcpp-git/ncmpcpp-git.tar.gz
tar -xvf ncmpcpp-git.tar.gz
cd ncmpcpp-git
makepkg -s
sudo pacman -U ncmpcpp-git****************.pkg.tar.xz</code></pre>
Modify the config located in ~/.ncmpcpp/config
A good starting config is <a href="https://bbs.archlinux.org/viewtopic.php?pid=1113439#p1113439">MadCatMk2's config on Archlinux Forums.</a>

&nbsp;
<pre>mpd_music_dir = "~/location/to/your/music/directory/"
visualizer_in_stereo = "yes"
visualizer_fifo_path = "/tmp/mpd.fifo"
visualizer_output_name = "FIFO"
visualizer_sync_interval = "30"
visualizer_type = "wave"
visualizer_look = "◆▋"
message_delay_time = "3"
playlist_shorten_total_times = "yes"
playlist_display_mode = "columns"
browser_display_mode = "columns"
search_engine_display_mode = "columns"
playlist_editor_display_mode = "columns"
autocenter_mode = "yes"
centered_cursor = "yes"
user_interface = "alternative"
follow_now_playing_lyrics = "yes"
locked_screen_width_part = "60"
display_bitrate = "yes"
external_editor = "vim"
use_console_editor = "yes"
header_window_color = "cyan"
volume_color = "red"
state_line_color = "yellow"
state_flags_color = "red"
progressbar_color = "yellow"
statusbar_color = "cyan"
visualizer_color = "red"</pre>
&nbsp;

&nbsp;
