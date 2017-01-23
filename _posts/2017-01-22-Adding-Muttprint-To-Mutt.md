---
layout: post
title: Adding Muttprint to Mutt 
---

Switching my work computer to linux has been a challenge.  I am not a well learned linux user and have only learned by solving these challenges.  At work I wanted to print from Mutt and stumbled across [muttprint](https://aur.archlinux.org/packages/muttprint/).

The [mutt archwiki](https://wiki.archlinux.org/index.php/mutt) provides an example syntax to add into muttrc:
```
set print_command="/usr/bin/muttprint %s -p {PrinterName}"
```

For me, I had to change it to:
```
set print_command="/usr/bin/muttprint %s"
```
And edit line 9 of /etc/Muttprintrc:
```
PRINTER="lp"
```
to:
```
PRINTER="Brother_HL-L5200DW_series"
```

To find the printer name I ran:
```
lpstat -s
```
And the provided output was:
```
system default destination: Brother_HL-L5200DW_series
device for Brother_HL-L5200DW_series: socket://192.168.88.202
```

Back to editing muttrc, ensure that your key binding for 'print-message' is defined:
```
bind    pager   P           print-message
```
