---
title: Solarized RXVT with VIM in Archlinux
date: 2015-01-28T14:23:45+00:00
author: Frank S
layout: post
---
<a href="http://frankshin.com/wp-content/uploads/2015/01/2015-01-28-133518_1440x900_scrot.png"><img class=" size-medium wp-image-233 aligncenter" src="http://frankshin.com/wp-content/uploads/2015/01/2015-01-28-133518_1440x900_scrot-300x188.png" alt="2015-01-28-133518_1440x900_scrot" width="300" height="188" /></a>
<h3>Solarized RXVT with VIM</h3>
It is pretty common for a linux user to spend most of his/her time in a terminal.  We enjoy the low overhead, responsiveness, and customizeability of cli programs.  It is critical that we find a color scheme that is not only pleasant to look at but is functional and easy to read.  I've been using various color schemes throughout the year and although I knew about <a href="solarized%20by Ethan Schoonover">solarized by Ethan Schoonover</a> I've never personally tried it out - until yesterday!
<h3>Installing Solarized - RXVT</h3>
The best RXVT available in Archlinux is  <a href="https://aur.archlinux.org/packages/rxvt-unicode-patched/">rxvt-unicode-patched</a>.  As of this post it is out of date and you will have to manually enter in the sha1sum of 33297e5303e45d27e07f40060d3655ae019eefdc for 9.21.

If you aren't too sure, we can manually skip integreity check:
<pre><code>wget https://aur.archlinux.org/packages/rx/rxvt-unicode-patched/rxvt-unicode-patched.tar.gz
tar -xvf rxvt-unicode-patched.tar.gz
cd rxvt-unicode-patched
makepkg -s --skipinteg
pacman -U rxvt-unicode-patched-9.21-1-x86_64.pkg.tar.xz
</code></pre>
You will need to download the solarized color scheme either at Ethan's github or from <a href="https://raw.githubusercontent.com/frank604/dotfiles/master/.colours/solarized">here</a>.  Save it in your ~/.colours folder or wherever you store your color schemes.

Your .Xresources should include:
<pre><code>#include "/home/frank604/.colours/solarized" &lt;-- Obviously modify it to where you saved the color scheme</code></pre>
&nbsp;
<h3>Installing Solarized - VIM</h3>
Ethan explains the installation succintly and there is no need for me to reword it so here is a quote from his <a href="Solarized%20Installation Instructions">Solarized Installation Instructions</a>.
<pre><code>
Option 1: Manual installation

    Move solarized.vim to your .vim/colors directory. After downloading the vim script or package:

    $ cd vim-colors-solarized/colors
    $ mv solarized.vim ~/.vim/colors/

Option 2: Pathogen installation (recommended)

    Download and install Tim Pope's Pathogen.

    Next, move or clone the vim-colors-solarized directory so that it is a subdirectory of the .vim/bundle directory.

    a. Clone:

        $ cd ~/.vim/bundle
        $ git clone git://github.com/altercation/vim-colors-solarized.git

    b. Move:

    In the parent directory of vim-colors-solarized:

        $ mv vim-colors-solarized ~/.vim/bundle/

Modify .vimrc

After either Option 1 or Option 2 above, put the following two lines in your .vimrc:

syntax enable
set background=dark
colorscheme solarized

or, for the light background mode of Solarized:

syntax enable
set background=light
colorscheme solarized

I like to have a different background in GUI and terminal modes, so I can use the following if-then. However, I find vim's background autodetection to be pretty good and, at least with MacVim, I can leave this background value assignment out entirely and get the same results.

if has('gui_running')
    set background=light
else
    set background=dark
endif

See the Solarized homepage for screenshots which will help you select either the light or dark background.</code></pre>
<h3>Fixing Background Issue In VIM</h3>
I hope you've read this far because with rxvt + vim + solarized there is a glaring issue that needs to be resolved.  If you choose the dark color settings for solarized, the background will be white in vim.  This issue doesn't happen in termite and only rxvt so far.  Here is how to fix it:

Add this line to ~/.Xresources
<pre><code>URxvt.intensityStyles: false</code></pre>

Add these lines to ~/.vimrc
<pre><code>  7 set nocompatible
 set t_Co=16
 call pathogen#infect()
 syntax on
 set background=dark " dark|light "
 colorscheme solarized
 filetype plugin on
 filetype indent on</code></pre>

Now you are good to go! Enjoy!
&nbsp;
