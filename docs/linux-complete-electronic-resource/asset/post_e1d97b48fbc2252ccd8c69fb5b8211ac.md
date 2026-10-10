
More colors make your video card transfer more data during the same time. If your video card cannot cope, then either the resolution or the refresh rate has to be reduced. By default, XFree reduces the resolution. If you want to keep the resolution and reduce the refresh rate, you must insert a new appropriate Modeline into your XF86Config file. This defines that resolution with a lower refresh rate. For instance replace the old value

```
Modeline '1024x768' 75 1024 1048 1184 1328 768 771 777 806 -hsync -vsync
```

with the following value:

```
Modeline '1024x768' 65 1024 1032 1176 1344 768 771 777 806 -hsync -vsync
```

The magic numbers 75 and 65 are the respective clock rates that you find reported by X in your `.X.err` file. Consult the monitor's file in the XF86 documentation for Modelines suitable for the maximum clock rate your video card can deliver under 16-bit color depth.

## RUNNING XFree86

With your XF86Config file configured, you're ready to fire up the X server and give it a spin. First, be sure that `/usr/X11R6/bin` is on your path.

The command to start up XFree86 is

```
startx
```

This is a front-end to `xinit` (in case you're used to using `xinit` on other Unix systems).

This command will start the X server and run the commands found in the file `.xinitrc` in your home directory. `.xinitrc` is just a shell script containing X clients to run. If this file does not exist, the system default `/usr/X11R6/lib/X11/xinit/xinitrc` will be used.

A standard `.xinitrc` file looks like this:

```
#!/bin/sh

xterm -fn 7x13bold -geometry 80x32+10+50 &
xterm -fn 9x15bold -geometry 80x34+30-10 &
oclock -geometry 70x70-7+7 &
xsetroot -solid midnightblue &

exec fwm2
```

This script will start up two `xterm` clients, an `oclock`, and set the root window (background) color to midnightblue. It will then start up `fwm2`, the window manager. Note that fwm2 is executed with the shell's exec statement; this causes the xinit process to be replaced with fwm2. Once the fwm2 process exits, the X server will shut down. You can cause fwm2 to exit by using the root menus: depress mouse button 1 on the desktop background--this will display a pop-up menu that will allow you to exit fwm2.

Be sure that the last command in .xinitrc is started with exec, and that it is not placed into the background (no ampersand on the end of the line). Otherwise the X server will shut down as soon as it has started the clients in the .xinitrc file.

Alternatively, you can exit X by pressing Ctrl+Alt+Backspace in combination. This will kill the X server directly, exiting the window system.

The above is a very, very simple desktop configuration. Many wonderful programs and configurations are available with a bit of work on your .xinitrc file.

![](img/a3584dae761d2e3abed8bf40d7637389_149_0.png)

> If you are new to the X Window System environment, we strongly suggest picking up a book such as *The Joy of X: An Overview of the X Window System* by Niall Manchester (Addison-Wesley 1993, ISBN 0201-565129). Using and configuring X is far too in-depth to cover here. See the man pages for xterm, oclock, and fwm2 for clues on getting started.

## TERMS OF USE

This document is copyright © 1996 by Eric S. Raymond. You may use, disseminate, and reproduce it freely, provided you

- Do not omit or alter this copyright notice.
- Do not omit or alter the version number and date.
- Do not omit or alter the document's pointer to the current WWW version.
- Clearly mark any condensed or altered versions as such.

These restrictions are intended to protect potential readers from stale or mangled versions. If you think you have a good case for an exception, ask me.

## ACKNOWLEDGEMENTS

This document was originated by Matt Welsh in the dim and backward abysm of time. Thanks, Matt!

## TRANSLATIONS

Italian: http://www.pluto.linux.it/ildp/HOWTO/XFree86-HOWTO.html

Slovenian: http://www.lugos.si/delo/slo/HOWTO-sl/XFree86-HOWTO-sl.html

Croatian: http://meta.mioc.hr/XFree86-KAKO.html

## Chapter 6

## PRINTERS

This chapter comprises the Linux Printing HOWTO, a collection of information on how to generate, preview, print, and fax anything under Linux (and other kinds of Unix).

This is the complete text of the Linux Printing HOWTO, version 3.29 of 9 March 1999, by Grant Taylor <gtaylor+ph t@picante.com>.

### INTRODUCTION

The Printing HOWTO should contain everything you need to know to set up printing services on your Linux box(en). As life would have it, it’s a bit more complicated than in the point-and-click world of Microsoft and Apple, but it’s also a bit more flexible and certainly easier to administer for large LANS.

This document is structured so that most people will only need to read the first half or so. Most of the more obscure and situation-dependent information in here is in the last half and can be easily located in the Table of Contents, whereas most of the information through the “Vendor Solutions” or “Ghostscript” sections is probably needed by most people.

Since version 3.x is a complete rewrite, much information from previous editions has been lost. This is by design, as the previous HOWTOs were so large as to be 60 typeset pages and had the narrative flow of a dead turtle. If you do not find the answer here, you are encouraged to (a) scan the previous version at the Printing HOWTO Home Page (http://www.ppcante.com/~gtaylor/pht/) and (b) drop me a note saying what ought to be here but isn’t.

The Printing HOWTO Home Page is a good place to find the latest version; it is also, of course, distributed from Metalab <metalab.unc.edu> and your friendly local LDP mirror.

### History

This is the third generation, which is to say the third complete rewrite, of the Printing HOWTO. The history of the PHT may be chronicled thusly:

1. I wrote the Printing HOWTO in 1992, in response to too many printing questions in comp.os.linux, and posted it. This pre-dated the HOWTO project by a few months and was the first FAQlist called a HOWTO. This edition was in plain ASCII.
2. After joining the HOWTO project, the Printing HOWTO was merged with an lpd FAQ by Brian McCauley <B.A.McCauley@bham.ac.uk>; we continued to coauthor the PHT for two years or so. At some point we incorporated the work of Karl Auer <Karl.Auer@anu.edu.au>. This generation of the PHT was in TeXInfo and available in PS, HTML, ASCII, and Info.
3. After letting the PHT rot and decay for over a year and an unsuccessful attempt at getting someone else to maintain it, this rewrite happened. This generation of the PHT is written in SGML using the LinuxDoc DTD and the SGML-Tools-l package. Beginning with version 3.27, it incorporates a summary of a companion printer support database; before 3.27 there was never a printer compatibility list in this HOWTO.

### Copyright

This chapter is Copyright ©1992-1999 by Grant Taylor. Feel free to copy and redistribute it according to the terms of the GNU General Public License, revision 2 or later.

### HOW TO PRINT

If you've already got lpd set up to print to your printer, your system administrator already did so, or your vendor did so for you, then all you need to do is learn how to use the 1pr command. The Printing Usage HOWTO (http://metalab.unc.edu/LDP/HOWTO/Printing-Usage-HOWTO.html) covers this and a few other queue manipulation commands you should probably know.

If, however, you have a new system or new printer, then you'll have to set up printing services one way or another before you can print. Read on!

### KERNEL PRINTER DEVICES

There are two completely different device drivers for the parallel port; which one you are using depends on your kernel version. The driver changed in Linux 2.1.53.

A few details are the same for both styles of driver. Most notably, many people have found that Linux will not detect their parallel port unless they disable Plug and Play in their PC BIOS. (This is no surprise; the track record for PnP of non-PCI devices with Windows and elsewhere has been something of a disaster).

#### The lp Device (Kernels <=2.1.32)

The Linux kernel (<=2.1.32), assuming you have compiled in or loaded the lp device (the output of cat /proc/devices should include the device
