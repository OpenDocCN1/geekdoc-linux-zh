
mini-HOWTO out there which describes how to obtain and install it. It generates PostScript or PCL, so it should work with most any printer that works otherwise on Linux. Apparently it's an Office clone and is rather bloated.

**WordPerfect** Corel distributes a basic version of WordPerfect 8 free for Linux and has suggested that they will distribute Corel Draw and Quattro Pro as well, once they are ported. This is probably the best option if you have an ARM machine; Corel makes the ARM-based Newfinder Linux computers and is almost certain to offer ARM Linux versions of everything. You can also buy the full-blown version and support, together or separately. The Linux WordPerfect Fonts and Printers (http://www.channel11.com/users/rodsmith/wpfonts.html) page has information about configuring WordPerfect for use with either Ghostscript or its built-in printer drivers (which are apparently identical to the DOS WordPerfect drivers, if your printer's driver isn't included in the WP8 distribution).

**Applix** Applix is a cross-platform (i.e., various versions of Unix, Windows, and others) office suite sold by the Applix company. Red Hat and SuSe sold it themselves when it was the only game in town; now sales have reverted to Applix.

**LyX** LyX is a front end to LaTeX, which looks very promising. See the LyX home page (http://www.lyx.org/) for more information. There is a KDE-styled version of LyX, called Klyx; the author of LyX and the instigator of KDE are the same person.

**Maxwell** Maxwell is a simple MS RTF-format based word processor which started as a commercial product but is now distributed under the GPL.

**The Andrew User Interface System** AUIS includes ez, a WYSIWYG-style editor with the most basic word processor features, HTML capabilities, and full MIME e-mail and newsgroup support. Unfortunately, AUIS is no longer maintained.

**Koffice** The KDE project is working toward a whole office suite. I don't think it's ready for prime time yet. The word processor will apparently be a descendant of LyX.

**GNOME** The GNOME project also is working toward various GNU-licensed Office-like tools. None are available yet, though.

![](img/a3584dae761d2e3abed8bf40d7637389_180_0.png)

Jeff Phillips <jeff@IRATUS.org> uses Caldera's WordPerfect 7 for Linux (on Slackware, of all things) and says that it works well. It apparently includes built-in printer support, as one would expect. Caldera should have info at http://www.caldera.com/. You can also buy a newer version of WordPerfect directly from Corel’s chosen Unix port company.

Other vendors should feel free to drop me a line with your offerings.

## ON-SCREEN PREVIEWING OF PRINTABLE THINGS

In this section you’ll learn that nearly anything you can print can be viewed on the screen, too.

### PostScript

Ghostscript has an X11 driver best used under the management of the PostScript previewer `gv`. The latest versions of these programs should be able to view PDF files, as well. Note that `gv` has replaced the older previewer `Ghostview`; the new user interface is much prettier and more full of features than Ghostview’s plain old Athena GUI.

### TeX DVI

TeX Device Independent files may be previewed under X11 with `xdvi`. Modern versions of `xdvi` call Ghostscript to render PostScript specials.

A VT100 driver exists as well. It’s called `dgvt`. `Tmview` works with Linux and `svgalib`, if that’s all you can do.

### Adobe PDF

Adobe’s Acrobat Reader is available for Linux; just download it from their Web site at http://www.adobe.com/.

You can also use `xpdf`, which is freeware and comes with source, and I should think Ghostview supports viewing PDF files with `gs` under X11 by now.

## SERIAL PRINTERS UNDER lpd

This section discusses how to set up and use a serial printer with lpd.

### Setting Up in Printcap

lpd provides five attributes which you can set in */etc/printcap* to control all the settings of the serial port a printer is on. Read the printcap man page and note the meanings of *br*, *fc*, *xs*, and *xs*. The last four of these attributes are bitmaps indicating the settings for using the port. The *br* attribute is simply the baud rate, i.e., *br9600*.

It is very easy to translate from *stty* settings to printcap flag settings. If you need to, see the man page for *stty* now.

Use *stty* to set up the printer port so that you can cat a file to it and have it print correctly. Here’s what *stty* –a looks like for my first serial port:

```text
dina:/usr/users/andy/work/!lpd/!pd8stty -a </dev/ttyS2
speed 9600 baud; rows 0; columns 0; line = 0;
intr = ^C; quit = ^\\; erase = ^?; kill = ^U; eof = ^D;
eol = <undef>; eol2 = <undef>; start = ^Q; stop = ^S;
susp = ^Z; rprnt = ^R; werase = ^W; lnext = ^V; min = 1;
time = 0;
 -parenb -parodd cs8 hupcl -cstopb cread -clocal -crtscts
 -ignbrk -brkint -ignpar -parmrk -inpck -istrip -inlcr
 -igncr -icrnl ixon -ixoff -iuclc -ixany -imaxbel
 -opost -olcuc -ocrnl -onocr -onlcr -oxtabs -ofill -ofdel
 nl0 cr0 tab0 bs0 vt0 ff0 -isig -icanon -iexten -echo -echoe
 -echok -echoctl -noflsh -xcase -tostop -echoprt -echock
 -echoke
```

The only changes between this and the way the port is initialized at bootup are -clocal, -crtscts, and -ixon. Your port may well be different depending on how your printer does flow control.

You actually use *stty* in a somewhat odd way. Since *stty* operates on the terminal connected to its standard input, you use it to manipulate a given serial port by using the *<* character as above.

Once you have your stty settings right, so that cat `file > /dev/ttyS2` (in my case) sends the file to the printer, look at the file `/usr/src/linux/include/asm-1386/termbits.h`. This contains a lot of defines and a few structs (You may wish to cat this file to the printer [you do have that working, right?] and use it as scratch paper). Go to the section that starts out

```text
/* c_cflag bit meaning */
#define CBAUD 0000017
```

This section lists the meaning of the fc and fs bits. You will notice that the names there (after the baud rates) match up with one of the lines of stty output. Didn’t say this was going to be easy?

Note which of those settings are preceded with a - in your stty output. Sum up all those numbers (they are octal). This represents the bits you want to clear, so the result is your fc capability. Of course, remember that you will be setting bits directly after you clear, so you can just use fc0177777 (I do).

Now do the same for those settings (listed in this section) which do not have a - before them in your stty output. In my example the important ones are CS8 (0000060), HUPCL (0002000), and CREAD (0000200). Also note the flags for your baud rate (mine is 0000015). Add those all up, and in my example you get 0002275. This goes in your fs capability (fs02275 works fine in my example).

Do the same with set and clear for the next section of the include file, c1flag bits. In my case I didn’t have to set anything, so I just use xc0157777 and xs0.

### Older Serial Printers that Drop Characters

Jon Luceky points out that some older serial printers with ten-cent serial interfaces and small buffers really mean stop when they say so with flow control. He found that disabling the FIFO in his Linux box’s 16550 serial port with setserial corrected the problem of dropped characters (you apparently just specify the uart type as an 8250 to do this).

## CREDITS

The smbrprint information is from an article by Marcel Roelofs <marcel@paragon.nl>.

The nprint information for using NetWare printers was provided by Michael Smith <mikes@bi.ox.ac.uk>.

The serial printers under lpd section is from Andrew Tefft <teftta@engr.dnet.ge.com>.

The blurb about gennas and such for gs was sent in by Andreas <quasi@hub-fue.franken.de>.

The two paragraphs about the 30-second closingwait of the serial driver was contributed by Chris Johnson <cdj@netcom.com>.

Robert Hart sent a few excellent paragraphs about setting up a print server to networked HPs, which I used verbatim.

And special thanks to the dozens upon dozens of you who've pointed out typos, bad URLs, and errors in the document over the years.
