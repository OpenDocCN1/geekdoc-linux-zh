
myprinter|MyPrinter|Printer on my desk:\
:lP=myprinter.mydomain.com#9100:sD=/var/spool/lpd/myprinter:\
:lf=/var/spool/lpd/myprinter/log:\
:mx#0:sF:sh:\
:if=/usr/local/lib/filters/ifhp:\
:of=/usr/local/lib/filters/ofhp:

Here, myprinter.mydomain.com is the printer’s network host name and 9100 is the TCP port to connect on. We’ve completely suppressed the header page (with :sh:).

## PROBLEM 55

Symptom: lpd complains that myprinter.example.com#9100 is not a device.

Problem: You’re using ifhp with Berkeley lpd, and the device isn’t supported.

Fix: The recommended fix is to ditch the old lpd and install LPRng. Barring that, you can fake a device and write a shell script wrapper for ifhp. To do this, first change the device to a null device with :lp=/var/spool/lpd/name/null: [see the section on AppleTalk printers later in the chapter for instructions on how to create the null device]. Then write a /var/spool/lpd/name/ifhp.wrapper script that looks like this:

```
#!/bin/sh
/usr/local/lib/filters/ifhp -Tdev=myprinter.example.com#9100 $@
```

Now change the printcap to reflect the new filter with :if=/var/spool/lpd/name/ifhp.wrapper:

If you don’t have a host name for the printer, you can use an IP address; if you haven’t set one, you’ll need to. You have several options for doing so—either by hand through the printer’s control panel, or with RARP/ARP, bootp, DHCP, tftp, or another method. Your best bet is to look at the printer manual, since printers can have very different requirements.

Chances are if you have a network printer, you have some other machines on the network as well. If just one of those machines is a Linux or Unix machine, designate it as a print server with an /etc/printcap like the one above, and have the other machines treat the printer as a remote device; in other words, they send their jobs to the print server for queuing and processing. (For the print server, take a look at the earlier section called Network Printer Access on remote printer access; the other machines will have entries that look like the remote printer example in Section 5.2.)

Here’s another example, this one for an HP duplex printer attached locally to a parallel port:

```
myprinter|MyPrinter|Printer on my desk:\
:lP=/dev/lp0:sd=/var/spool/lpd/myprinter:\
:lf=/var/spool/lpd/myprinter/log:\
:mx#0:sf:sh:\
:ifhp=duplex,status@:\
:if=/usr/local/lib/filters/ifhp:\
:of=/usr/local/lib/filters/ofhp:\
:vf=/usr/local/lib/filters/ifhp -c:
```

As the example above shows, the special ifhp= part of the printcap specifies various filter options. To turn an option off, put an "@" sign (@) at the end. In this example, note the status@ filter setting due to the parallel port connection. The device is /dev/lp0, the parallel port on most PCs (as of Linux kernel version 2.2).

There are two kinds of options: administrator options (also called -T options), and user options, which any user can access through the command line using -Z (also known as -Z options). For example, lpr -Zduplex allows two-sided printing if the printer supports it.

The following options also provide language support. (We’re most interested in PostScript, but the others come in handy for selecting paper trays, turning modes on, and printing text.) You can enable any available language support options:

- PS or ps  PostScript
- pjl  PJL, Printer Job Language
- pcl  PCL, Printer Control Language

> NOTE Separate multiple options with commas, as in :ifhp=duplex,status@:. To turn off both PJL and PCL, use :ifhp=pjl@,pcl@ in /etc/printcap.

Other filter options include:

### model=name

ifhp predefines a number of printer models with their various capabilities and limitations. See the ifhp.conf file for a list.

### status

This fetches the printer status. Since this requires a bidirectional connection and a printer that supports status in the first place, sometimes you must turn it off.

### pagecount

In order to do accounting, you need to get page counts.

### no_ps_eoj, no_pcl_eoj

Some printers don't like the end-of-job code, which the ifhp filter sends at the beginning of each job to clear any lingering errors. Use these options to turn the code off for PostScript or PCL, as appropriate.

## Selecting Other Options with ifhp.conf

The options described above are the basic ones to start with, and they may be all you need. But what about selecting other options, such as duplex for double-sided printing? This is where a new file, ifhp.conf, comes into play.

As it turns out, the default ifhp.conf file contains a large number of prebuilt option definitions for various printers, including default settings for most HPs. Type `less /etc/ifhp.conf` (or wherever you installed ifhp.conf), then type `/ps_user_opts` to jump to a line of user options that ifhp can make available. As the first line in the file, this should also include the default settings. Look them over to get an idea of what's available, keeping in mind that your printer may not support all of them.

## Two Parts to the ifhp.conf File

The ifhp.conf file is very large and contains a tremendous amount of information, but you can divide it into two parts:

**Part 1: _Default options and definitions._** Each option is defined as a printer code for each language. For example, the `ps_duplex` definition tells you what the filter will hand to the printer when PostScript is the active language. The `pcl_duplex` definition performs a similar function for PCL.

**Part 2: _Specific printer definitions._** As in Part 1, each option is defined as a printer code, except that each printer configuration begins with a label enclosed in square brackets; for example, `[apple postscript ps]`. Search for apple in the ifhp.conf file to see this definition.

> Part 2 is where the `model=name` option becomes relevant. If you put `:ifhp::model=apple:` in any entry in your `/etc/printcap`, ifhp will search for apple in the labels and use the modifications that configuration defines.

![](img/8131acdd754b0d26c380a2035b509e34_131_0.png)
