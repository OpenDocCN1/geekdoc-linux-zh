
# Printing with SuSE Linux
CHAPTER 24

(such as irda-utils-0.9.4.tar.gz) from http://www.cs.uit.no/linux-irda/irda-utils/. Module support must be enabled for your kernel. (See Chapter 23.)

The basic steps to enable infrared inloading, building, and installing the Irda distribution. You then need to create appropriate entries in your system's /etc/conf.modules file and create the infrared device(s).

After you have installed the software and configured your system, the easiest way to say, print to an infrared printer is to create a special entry in your /etc/printcap printer database or to use a filter program, such as APSfilter (mentioned earlier). Laptop users need to depress certain function keys to disable an existing serial port or to enable an IR port, and you may need to use the setserial command to assign IRQ values to the Irda.

# Some Program Tips

The following are some tips to help you print documents or set up applications for easier printing.

## emacs

Want to print directly from GNU emacs? If you use emacs on the console or in text-only mode, you can print the entire buffer, unformatted or formatted, by pressing Esc+X, typing lpr-buffer, and pressing Enter. Alternatively, you can set the lpr-switches variable in your .emacs file to press Enter. Just make sure you set the point to the correct printer in your /etc/printcap file. If you use GNU emacs with X11, select the Tools menu and then click the Print or (if you have selected text) Print Region menu items (XEmacs users will find the Print option under the File menu or can use the Print icon in the Emacs toolbar).

![](img/cbac72550c7126a22162e94d91a0c360_772_0.png)

## WordPerfect 8 for Linux

Thanks to Corel, nearly one million Linux users are happily enjoying Core’s free-for-personal-use edition of WordPerfect 8 for Linux.

> Note
> You can register and download a copy of WordPerfect 8 for Linux from http://linux.corel.com/linux8/download.htm.

# SuSE System Administration
PART III

In order to print with WordPerfect, you must add and select the Passthrough PostScript printer driver. To configure WordPerfect, start the program and press the Print or F5 key. In the WordPerfect Print dialog box, click the Select button. A Select Printer dialog box appears, as shown in Figure 24.17.

FIGURE 24.17
Use the Word-Perfect Select Printer dialog box to create or edit printers for your.

![](img/cbac72550c7126a22162e94d91a0c360_773_0.png)

A Printer Create/Edit dialog box appears when you click the Printer Create/Edit button. Next, click the Add button. An Add Printer Driver dialog box with a scrolling list of printer drivers appears (see Figure 24.18). Scroll through the list, click the Passthrough PostScript driver (wp0ps2.us.all), and click the OK button.

FIGURE 24.18
Select the Pass-thru PostScript printer driver to create a printer for Linux.

![](img/cbac72550c7126a22162e94d91a0c360_773_1.png)

In the tiny Create Printer dialog box (with the name passport.prs), click the OK button. The Printer Create/Edit dialog box reappears with the Passthrough PostScript printer highlighted. Click the Setup button. A Printer Setup dialog box appears. The Destination button, found near the bottom of the dialog box, should be clicked. A Select Destination dialog box appears (see Figure 24.19), listing lPRINTER, Disk, and lp, (along with any other defined printers from /etc/printcap). Click a printer defined with YaST (the auto printer) and then click OK.

FIGURE 24.19
In the Select Destination dialog box, complete your printer setup by selecting a yast-created printer as the print destination.

![](img/cbac72550c7126a22162e94d91a0c360_774_0.png)

To finish up, click OK in the Printer Setup dialog box, and then click OK again in the Create/Edit dialog box. In the Select printer dialog box, click the OK button; you'll be at the main Print dialog box. Click OK to print your document.

# Other Helpful Programs

The following are short descriptions of just a few of the programs offering handy services available for Linux. You'll find some of them indispensable.

## pbm Utilities

To translate or manipulate your graphics files into a multitude of formats or effects for printing, try one of Jeff Poskanzer's numerous pbm utilities. At last count there were nearly 100 programs. Use the apropos command with the pbm and pnm keywords for pointers.

## gv

Most of the convenience of having PostScript documents print automatically on cheap printers under Linux derives from Aladdin Enterprises' interpreter, gs, or Ghostscript. Johannes Planck's X client,v, based on Tim Theisen's much-beloved ghostview, is another of those "insanely great" programs that come with nearly every Linux distribution.

# Troubleshooting and More Information

You can use gv, like the older Ghostview, to preview or print .ps files. This program features multiple levels of magnification and landscape and portrait modes, and prints PostScript files too.

I'll offer some general tips on troubleshooting printing and give some pointers to more information. You should not have trouble printing under Linux, but if you can't seem to get started, try some of these hints:

- Make your printer cable is properly connected to your computer and printer.
- Make sure your printer is on.
- Ensure that you have specified lpd service. (Ensure that the lpd daemon is running).
- Verify that you initially wanted printer support when you installed Linux or if you've rebuilt your Linux kernel.
- Make sure the kernel daemon is active. (This loads the printer driver module needed).
- Ensure you have the lpd.o module available and installed on your system. Also ensure you have a correct entry for the parport modules in your /etc/conf.modules file.
- Avoid PPA or Windows-only printers until hardware manufacturers offer better support.
- Make sure you select the correct printer filter for your printer with the yast or SETUP command, and use different names for local and remote printers.

Still having problems? See the man pages for printcap, lpd,lpr, l1pq, l1rm, and lpc.

For information about the BSD printing system, read Ralph Campbell's abstract “4.3BSD Line Printer Spool Manager,” which is part of the 4.4BSD System Manager's Manual,

For detailed information about printing under Linux, read the Linux Printing HOWTO by Grant Taylor. The Linux Printing HOWTO contains a host of great tips, tricks, traps, and hacks concerning printing under Linux, including setups for serial printers and network printing. Also read the Linux Printing Usage HOWTO by Mark Komarinski; it is found under /usr/doc/howto/en/mini.

![](img/cbac72550c7126a22162e94d91a0c360_776_0.png)
