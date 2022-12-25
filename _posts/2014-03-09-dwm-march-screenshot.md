---
title: 'DWM (Archlinux) &#8211; March Screenshot'
layout: post
---
DWM (Archlinux) - March Screenshot

<strong><span style="color: #ff0000;">Edit: Sept 6 2015 - Check out my latest screenshot<a style="color: #ff0000;" href="http://frankshin.com/dwm-screenshot-update/"> here.</a></span></strong>

DWM has been my WM of choice due to its simplicity, written in C, and a good knowledgable group of enthusiast at the Arch Forums.  Through my learning of DWM, an attempt at screenshotting each month will be made to journal my progress.

Below is my clean desktop.  I went with a blue grey color scheme which would be easy on the eyes and easy to find the information at a glance.

<a href="https://blog.f604.xyz/wp-content/uploads/2014/03/ss41.png"><img class="alignnone size-full wp-image-119" src="https://blog.f604.xyz/wp-content/uploads/2014/03/ss41.png" alt="ss4" width="400" height="250" /></a>

Below is my workspace.  I have part of my config.h displaying, rtorrent, weechat, and ranger.

<a href="https://blog.f604.xyz/wp-content/uploads/2014/03/ss51.png"><img class="alignnone size-full wp-image-120" style="margin-top: 22.09375px; margin-bottom: 22.09375px;" src="https://blog.f604.xyz/wp-content/uploads/2014/03/ss51.png" alt="ss5" width="400" height="250" /></a>

Hrm, on another thought, I'll have to add in my script and config even if you can find it on github.com/frank604 so that I can 'freeze' the settings here on my blog.

---------------------------------------------------------------------------------

Edit:  NEW SCREENSHOTS!!  March 10 2014 update!!

<a href="https://blog.f604.xyz/wp-content/uploads/2014/03/screenshot1.png"><img class="alignnone size-full wp-image-130" src="https://blog.f604.xyz/wp-content/uploads/2014/03/screenshot1.png" alt="screenshot" width="400" height="250" /></a> <a href="http://frankshin.com/wp-content/uploads/2014/03/screenbusy1.png"><img class="alignnone size-medium wp-image-132" src="http://frankshin.com/wp-content/uploads/2014/03/screenbusy1.png" alt="screenbusy" width="400" height="250" /></a>

So the strangest thing happened.  Last night I couldn't sleep so I found a different patchset that was close to what I wanted and then patched in cycle and push.  Now this change makes my DWM complete.  However, I did have to rewrite my config.h and I also took some time out to touch up my statusbar.

The new patchset is in my <a href="https://github.com/fszf/dwm">github</a>.  This is based off of <a href="https://github.com/KieranQuinn/dwm.git">Kieran Quinn's dwm</a>.  I modified JasonWRyan's copy of Push and Cycle patches from his <a href="https://bitbucket.org/jasonwryan/dwm-patchset/src">bitbucket</a> to work with Kieran's patchset
<h3><a href="https://blog.f604.xyz/dwm-archlinux-patchset-description/">Read about Patches and Description on next post</a></h3>
config.h
<pre>#define NUMCOLORS       13
#define MODKEY          Mod4Mask
#define TAGKEYS(KEY,TAG) 
    { MODKEY,                       KEY,      view,           {.ui = 1 &lt;&lt; TAG} }, 
    { MODKEY|ControlMask,           KEY,      toggleview,     {.ui = 1 &lt;&lt; TAG} }, 
    { MODKEY|ShiftMask,             KEY,      tag,            {.ui = 1 &lt;&lt; TAG} }, 
    { MODKEY|ControlMask|ShiftMask, KEY,      toggletag,      {.ui = 1 &lt;&lt; TAG} },

static const unsigned int tagspacing = 1;       /* space between tags */
static const unsigned int tagpadding = 5;      /* inner padding of tags */
static const unsigned int taglinepx = 2;        /* height of tag underline */
static const unsigned int systrayspacing = 1;   /* systray spacing */
static const Bool showsystray = True;           /* false means no systray */
static const unsigned int gappx = 8;            /* gaps between windows */
static const unsigned int borderpx = 1;         /* border pixel of windows */
static const unsigned int snap = 32;            /* snap pixel */
static const Bool showbar = True;               /* false means no bar */
static const Bool topbar = True;                /* false means bottom bar */
static const float mfact = 0.50;                /* factor of master area size [0.05..0.95] */
static const int nmaster = 1;                   /* number of clients in master area */
static const Bool resizehints = False;          /* true means respect size hints in tiled resizals */
static const char font[] = "-*-tamsynmod-medium-r-*-*-18-*-*-*-*-*-*-*";

static const char colors[NUMCOLORS][ColLast][13] = {
    /* border    fg         bg */
    { "#2D2D2D", "#FFFFFF", "#2D2D2D" },        /* 01 - regular */
    { "#4d79ff", "#FFFFFF", "#2D2D2D" },        /* 02 - selected */
    { "#2D2D2D", "#FF0000", "#2D2D2D" },        /* 03 - urgent */
    { "#2D2D2D", "#666666", "#2D2D2D" },        /* 04 - occupied */
    { "#2D2D2D", "#A82222", "#2D2D2D" },        /* 05 - red */
    { "#2D2D2D", "#4779b3", "#2D2D2D" },        /* 06 - blue */
    { "#2D2D2D", "#349147", "#2D2D2D" },        /* 07 - green */
    { "#2D2D2D", "#666666", "#2D2D2D" },        /* 08 - dark grey */
    { "#2D2D2D", "#DCDCDC", "#2D2D2D" },        /* 09 - light grey */
    { "#2D2D2D", "#4779b3", "#2D2D2D" },        /* 0A - orange */
    { "#2D2D2D", "#B86A6A", "#2D2D2D" },        /* 0B - pink */
    { "#2D2D2D", "#FFFFFF", "#2D2D2D" },        /* 0C - white */
    { "#2D2D2D", "#000000", "#2D2D2D" },        /* 0D - black */
};

static const Layout layouts[] = {
    /* symbol   gaps    arrange */
    { "þ",      True,   tile },
    { "ü",      True,   bstack },
    { "ÿ",      False,  monocle },
    { "ý",      False,  NULL },
};

static const Tag tags[] = {
    /* name     layout          mfact   nmaster */
    { "web",    &amp;layouts[0],    -1,     -1 },
    { "term",   &amp;layouts[0],    -1,     -1 },
    { "media",  &amp;layouts[3],    -1,     -1 },
    { "steam",  &amp;layouts[0],    -1,     -1 },
    { "mail",   &amp;layouts[0],    -1,     -1 },
    { "misc",   &amp;layouts[0],    -1,     -1 },
};

static const Rule rules[] = {
    /* class        instance    title       tags mask     isfloating      iscentred       monitor */
   { "Chromium",    NULL,       NULL,       1 &lt;&lt; 0,       False, True,       -1 },
   { "Filezilla",   NULL,       NULL,       1 &lt;&lt; 0,       True,  True,       -1 },
   { "Spacefm",     NULL,       NULL,       0,            True,  True,       -1 },
   { "Truecrypt",   NULL,       NULL,       0,            True,  True,       -1 },
   { "Dwb",         NULL,       NULL,       1 &lt;&lt; 0,       False, False,      -1 },
   { "Steam",       NULL,       NULL,       1 &lt;&lt; 3,       False, True,       -1 },
   { "Gimp",        NULL,       NULL,       0,            True,  True,       -1 },
   {  NULL,         "mutt",     NULL,       1 &lt;&lt; 4,       False, False,       -1 },
   {  NULL,         "tmux",     NULL,       1 &lt;&lt; 1,       False, False,       -1 },
   {  NULL,         "YouTube",  NULL,       1 &lt;&lt; 2,       True, True,       -1 },
   { "mpv",         NULL,       NULL,       0,            True,  True,       -1 },
};

/* helper for spawning shell commands in the pre dwm-5.0 fashion */
#define SHCMD(cmd) { .v = (const char*[]){ "/bin/sh", "-c", cmd, NULL } }

static const char *menu[] = { "dmenu_run", "-i", "-fn", font, "-nb", colors[0][ColBG], "-nf", colors[0][ColFG], "-sb", colors[1][ColBG], "-sf", colors[9][ColFG], NULL };
static const char *webb[] = { "dwb", NULL, "Dwb" };
static const char *file[] = { "pcmanfm", NULL, "Pcmanfm" };
static const char *term[] = { "termite", NULL,  };
static const char   *mailcmd[] = { "termite", "--name=mutt", "-e", "mutt", NULL };
static const char   *tmuxcmd[] = { "termite", "--name=tmux", "-e", "tmux", NULL };
static const char   *yt[] = { "termite", "--name=YouTube", "-e", "youtube-viewer", NULL };
static const char *fz[] = { "filezilla", NULL,  };

static Key keys[] = {
    { MODKEY,           XK_p,       spawn,          {.v = menu } },
    { MODKEY|ShiftMask, XK_w,       runorraise,          {.v = webb } },
    { MODKEY|ShiftMask, XK_Return,  spawn,     {.v = term } },
    { MODKEY|ShiftMask, XK_f,       runorraise,     {.v = file } },
    { MODKEY|ShiftMask, XK_t,       runorraise,     {.v = tmuxcmd } },
    { MODKEY|ShiftMask, XK_m,       runorraise,     {.v = mailcmd } },
    { MODKEY|ShiftMask, XK_y,       runorraise,     {.v = yt } },
    { MODKEY|ShiftMask, XK_z,       runorraise,     {.v = fz } },
    { MODKEY|ShiftMask, XK_q,       quit,           {0} },
    { MODKEY|ShiftMask, XK_b,       togglebar,      {0} },
    { MODKEY|ShiftMask, XK_c,       killclient,     {0} },
    { MODKEY,           XK_Return,  zoom,           {0} },
    { MODKEY,           XK_Tab,     view,           {0} },
    { MODKEY|ControlMask,           XK_f, togglefloating, {0} },
    { MODKEY,           XK_space,   setlayout,      {0} },
    { MODKEY,           XK_t,       setlayout,      {.v = &amp;layouts[0] } },
    { MODKEY,           XK_b,       setlayout,      {.v = &amp;layouts[1] } },
    { MODKEY,           XK_m,       setlayout,      {.v = &amp;layouts[2] } },
    { MODKEY,           XK_f,       setlayout,      {.v = &amp;layouts[3] } },
    { MODKEY,           XK_j,       focusstack,     {.i = +1 } },
    { MODKEY,           XK_k,       focusstack,     {.i = -1 } },
    { MODKEY,           XK_h,       setmfact,       {.f = -0.05 } },
    { MODKEY,           XK_l,       setmfact,       {.f = +0.05 } },
    { MODKEY,           XK_equal,   incnmaster,     {.i = +1 } },
    { MODKEY,           XK_minus,   incnmaster,     {.i = -1 } },
    { MODKEY,           XK_Down,    focusstack,     {.i = +1 } },
    { MODKEY,           XK_Up,      focusstack,     {.i = -1 } },
    { MODKEY,           XK_0,       view,           {.ui = ~0 } },
    { MODKEY|ShiftMask, XK_0,       tag,            {.ui = ~0 } },
    { MODKEY,           XK_comma,   focusmon,       {.i = -1 } },
    { MODKEY,           XK_period,  focusmon,       {.i = +1 } },
    { MODKEY|ShiftMask, XK_comma,   tagmon,         {.i = -1 } },
    { MODKEY|ShiftMask, XK_period,  tagmon,         {.i = +1 } },
    { MODKEY,                       XK_Left,   cycle,          {.i = -1 } },
    { MODKEY,                       XK_Right,  cycle,          {.i = +1 } },
    { MODKEY|ControlMask,           XK_Left,   tagcycle,       {.i = -1 } },
    { MODKEY|ControlMask,           XK_Right,  tagcycle,       {.i = +1 } },
    { MODKEY|ControlMask,           XK_j,      pushdown,       {0} },                                                                                      
    { MODKEY|ControlMask,           XK_k,      pushup,         {0} },
    { MODKEY|ControlMask,           XK_q,      quit,           {0} },
    TAGKEYS(            XK_1,       0)
    TAGKEYS(            XK_2,       1)
    TAGKEYS(            XK_3,       2)
    TAGKEYS(            XK_4,       3)
    TAGKEYS(            XK_5,       4)
    TAGKEYS(            XK_6,       5)
};

static Button buttons[] = {
    { ClkLtSymbol,      0,          Button1,        setlayout,      {0} },
    { ClkClientWin,     MODKEY,     Button1,        movemouse,      {0} },
    { ClkClientWin,     MODKEY,     Button2,        togglefloating, {0} },
    { ClkClientWin,     MODKEY,     Button3,        resizemouse,    {0} },
    { ClkTagBar,        0,          Button1,        view,           {0} },
    { ClkTagBar,        0,          Button3,        toggleview,     {0} },
    { ClkTagBar,        MODKEY,     Button1,        tag,            {0} },
    { ClkTagBar,        MODKEY,     Button3,        toggletag,      {0} },
};</pre>
&nbsp;

&nbsp;

dwm-statusbar
<pre># ~/bin/dwm-statusbar
# Adapted from w0ng status bar: https://github.com/w0ng/bin
# Adapted from jasonwryan status bar: https://bitbucket.org/jasonwryan/shiv/src/1ad5950c3108a4e5a9dcb78888a1ccfeb9252b45/Scripts/dwm-status?at=default
# Some original work/modifications by frank: https://github.com/frank604

# Colour codes from dwm/config.h
color0="x01" # normal  
color6="x06" # brightblue

#---separator                              
sp="$(echo -ne "${color0} ")" 
sp1="$(echo -ne "${color0} | ")" 
sp2="$(echo -ne "${color0}| ")"
sp3="$(echo -ne "${color0}|")"

#print_song_info() {
#  track="$(mpc current)"
#  artist="${track%%- *}"
#  title="${track##*- }"
#  [[ -n "$artist" ]] &amp;&amp; echo -e "${color0}ê${sp}${color5}${artist}${color9}${title} ${color0}|"
#}

print_power() {
  status="$(cat /sys/class/power_supply/ADP1/online)"
  battery="$(cat /sys/class/power_supply/BAT0/capacity)"
  if [ "${status}" == 1 ]; then
    echo -ne "${color6}Â${color0}ON ${battery}%"
  else
    echo -ne "${color6}ð${color0}${battery}%"
  fi
}

print_wifiqual() {
  wifiessid="$(/sbin/iwconfig 2&gt;/dev/null | grep ESSID | cut -d: -f2)"
  wifiawk="$(echo $wifiessid | awk -F',' '{gsub(/"/, "", $1); print $1}')"
  wificut="$(echo $wifiawk | cut -d' ' -f1)"
  echo -ne "${color6}¤${color0}${wificut}"
}

print_hddfree() {
  hddfree="$(df -Ph /dev/sda4 | awk '$3 ~ /[0-9]+/ {print $4}')"
  echo -ne "${color6}¨${color0}${hddfree}"
}

print_email_count() {
   mail1="$(find $HOME/Mail/FWS/INBOX/new/ -type f | wc -l)"
   mail2="$(find $HOME/Mail/GMAIL/INBOX/new/ -type f | wc -l)"
   emailcount="$(($mail1 + $mail2))"
    if [[ "${emailcount}" -eq 0 ]]; then
        echo -en "${color6}Ð${color0}0"
    else
        echo -en "${color6}Ð${color0}${emailcount}"
    fi
}
print_pacup(){
   pup="$(pacman -Qqu --dbpath /tmp/checkup-db/frank604/ | wc -l)"
   if [[ "${pup}" -eq 0 ]]; then
        echo -en "${color0}0"
   else
        echo -en "${color0}${pup}"
   fi
}

print_aurups(){
    ups="$(awk '$0 !~ /tamsyn/' /tmp/aurupdates* | wc -l)"
    if [[ "${ups}" -eq 0 ]]; then
        echo -en "${color0}0"
    else 
        echo -en "${color0}${ups}"
    fi
}

print_aurphans(){
    aur="$(awk '$0 !~ /^No /' /tmp/aurphans* | wc -l)"
    if [[ "${aur}" -gt 0 ]]; then
        echo -en "∆"
    else 
        echo -en ""
    fi
}
 print_volume(){
    mix=`amixer get Master | tail -1`
    vol="$(amixer get Master | tail -n1 | sed -r 's/.*[(.*)%].*/1/')"
    if [[ $mix == *[off]* ]]; then
      #red 2                                                
      echo -e "${color6}í${color2} OFF"
    elif [[ $mix == *[on]* ]]; then
      #green 9
      echo -e "${color6}í${color0}${vol}% "
    else
      #yellow6
      echo -e "${color6}í${color2} ---"
    fi
 }

print_datetime() {
  datetime="$(date "+%a %d %b %I:%M")"
  echo -ne "${color6}É${sp}${color0}${datetime}"
}

# cpu (from: https://bbs.archlinux.org/viewtopic.php?pid=661641#p661641)

while true; do
  # get new cpu idle and total usage
  eval $(awk '/^cpu /{print "cpu_idle_now=" $5 "; cpu_total_now=" $2+$3+$4+$5 }' /proc/stat)
  cpu_interval=$((cpu_total_now-${cpu_total_old:-0}))
  # calculate cpu usage (%)
  let cpu_used="100 * ($cpu_interval - ($cpu_idle_now-${cpu_idle_old:-0})) / $cpu_interval"

  # output vars
print_cpu_used() {
  printf "%-1b" "${color0}Ñ${sp}${color11}${cpu_used}%"
#"%-10b" "${color7}CPU:${cpu_used}%"
}

  # Pipe to status bar, not indented due to printing extra spaces/tabs
  xsetroot -name "$(print_power)${sp1}$(print_wifiqual)$(print_hddfree)${sp1}$(print_email_count)$(print_pacup)$(print_aurups)$(print_aurphans)${sp2}$(print_volume)${sp2}$(print_datetime)"

  # reset old rates
  cpu_idle_old=$cpu_idle_now
  cpu_total_old=$cpu_total_now
  # loop stats every 1 second
  sleep 1 
 done</pre>
