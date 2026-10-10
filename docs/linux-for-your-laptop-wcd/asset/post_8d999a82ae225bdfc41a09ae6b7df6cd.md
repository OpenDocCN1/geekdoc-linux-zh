
## Canon BJC-50

The Canon BJC-50 is a very compact, lightweight printer that easily fits into a backpack or briefcase. This road-friendly printer sprints through black-and-white print jobs with surprising speed for its size. Here are some features of this printer:

- Removable Li-ion battery
- IrDA port built into the printer
- Nonstandard (on the printer's end), short parallel-printer cable
- Dimensions: 11.9 inches × 4.4 inches × 2 inches
- Weight: about 2 lbs., including battery
- Page-per-minute speed: about 7 in black-and-white and 2 in color
- Dots per inch: 720×360 for color
- Pages per charge: not available
- Paper weight range: 17- to 28-lb. paper
- Pages per cartridge: about 170 quality black-and-white; about 40 high-quality color
- Time to charge: about 6 hours for a 100 percent depleted battery
- Lifespan of battery: longer than NiCad
- Sheet feeder capacity: optional; otherwise, manual feed

The Canon BJC-50 is the smallest of the Canon BubbleJet series. A larger sibling, the Canon BJC-80, has nearly all the same features, including a sheet feeder, which is sorely missed on the BJC-50. When you print with the BJC-50, you have to manually hand-feed each new page and press a button on top of the printer. Although this is fine for one- or two-page print jobs, you might want to shell out a little more money for the optional sheet feeder.

Besides its speed, two other features make this printer (and even the larger BJC-80) a great portable printer for the mobile Linux user. First, its built-in Li-ion battery means more pages per charge, faster charging time, and longer battery life. Second, it works with Linux IrDA! This is a definite bonus, because you can go on the road and forgo not only a transformer, but also a printer cable!

Read on to learn about printing with Linux and how to configure Linux to work with the HP340 and Canon BJC-50.

### Printing with Linux

Most Red Hat–based Linux distributions use the Berkeley Software Distribution (BSD) printer spooling system. Others, such as Caldera’s OpenLinux and SuSE Linux, might use an improved hybrid system named LPing. These print-spooler systems work through the lpd daemon, which runs in the background, waiting for print jobs to appear in a selected directory, such as /var/spool/lpd/nameofprinter. *nameofprinter* is the printer you define when you create a printer for Linux (see the next section).

### Alternative Printing with LPing

LPing is a new and enhanced print spooling system available for Red Hat–based Linux distributions. LPing is also used by other distributions, such as Caldera’s OpenLinux and SuSE Linux. This system is transparently compatible with BSD’s lpd but offers enhanced security features and better controls for managing large printer installations on big networks. LPing is compatible with Red Hat’s print filter system. For more information, see the LPing URL under “Resource Information” at the end of this chapter.

When a document appears in the printer’s spool directory, lpd spawns a copy of itself to take care of printing the document according to the printer’s specifications, contained in the printer’s entry in the Linux printer capabilities database, /etc/printcap. The main daemon is used to control print queuing, ordering of print jobs, and your system’s printers.

Many, if not most, Linux applications output print documents and graphics as text documents in the PostScript language. These PostScript documents are then automatically sent or *filtered* through the Ghostscript interpreter, *gs*, and then translated to HPCL for output to your printer, according to a specified filter entry in the printer’s /etc/printcap entry.

### Creating a Printer

To create a printer for Linux, you need to create a proper entry in /etc/printcap. A single printer may have multiple entries and different names in /etc/printcap. This way, you can define the same printer as a color printer, gray-scale printer, or black-and-white-only printer. Although you can manually edit /etc/printcap (as root) with a text editor, most mobile Linux users prefer to use a software tool with a graphical interface. Red Hat, Mandrake, and Yellow Dog Linux users can use the *printtool* client, which requires that you run X11. (SuSE users use YaST, and Caldera OpenLinux users may use the *Lisa* command or COAS.)

### Remote Printing for iBook

Although the Apple iBook runs Linux, full support for external printers attached via the USB port is not complete. However, iBook Linux users can print to remote Linux printers by using *printtool* to create a remote printer entry. See "Printing to a Remote Linux Printer" later in this chapter.

Red Hat's *printtool* may be started from Red Hat's control-panel client, from the GNOME panel menu, or from the command line of an X11 terminal window like this:

```
$ printtool
```

In this first example, you'll create a printer that will be attached to your notebook. Make sure your printer is attached to your laptop (or port replicator) and turned on. After you press Enter, click the Add button in the dialog box. You'll see a small dialog box, as shown in Figure 14.1.

Click the Local Printer button to start creating a printer, and then click OK. You should hear your printer activate when *printtool* detects your printer. If *printtool* does not report that a printer port has been found in the "Autodetection has found the following:" dialog box, check to make sure that the parport, parport_pc, and lp kernel modules have been loaded. You can do this by using the `lsmod` (list modules) command like this:

```
$ /sbin/lsmod

Module           Size  Used by
parport_probe    2960  0 (autoclean)
parport_pc       5620  1 (autoclean)
lp               4476  0 (autoclean)
...
```

If the modules have not been loaded, make sure that your Red Hat (or Mandrake) module configuration file, `/etc/conf.modules`, contains the following line:

```
alias parport_lowlevel parport_pc
```

If Linux still doesn’t recognize an attached printer, go back and make sure that the printer cables are properly attached on both ends and that the printer is turned on. If you use a Lowmark parallel-port Zip drive, check to make sure the `paride.o` module is unloaded from memory (using the `rmmod` command). After you get your printer working, you can try to use both devices with module support in memory. Next, click the OK button. You’ll see the **Edit Local Printer Entry** dialog box, shown in Figure 14.2.

Note the information returned in this dialog box. The `printtool` command assigns a default name, such as lp, but you can change this to any name you like. Also note the printer device recognized by Linux, such as `/dev/lp0`. When finished, click the Select button to continue. You’ll see the large dialog box shown in Figure 14.3.

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_344_0.png)

*Figure 14.1 Use the Red Hat*  
*printtool* *client's Add a Printer*  
*Entry dialog box to configure a*  
*variety of printers for Linux.*

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_345_0.png)

**Figure 14.2** Use the `printtool` Edit Local Printer Entry dialog box to name a printer and select additional print-filter options.

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_346_0.png)

Use the printtool Configure Filter dialog box to select a proper print filter for your printer.

Selecting the right options in this dialog box is critical to the success of configuring Linux to work with your printer. Scroll through the list and choose a printer type that matches your printer. Don't be discouraged if you don't see your printer's exact model listed in the filter list. Many printers work well using a filter designed for related printers, such as the HP500 filter, which also works with many HP600-series printers.

If you have an HP 340, select the HP DeskJet 500 filter. If you have a BJC-50 or BJC-80, select the Canon BJC-600 filter.

You should also select a resolution, paper size, color depth, and other printing options. Click the OK button when finished, and then click the OK button again. You'll then see your new printer listed in the printtool dialog box. Click the printer's name, and then select Tests, Print ASCII Test Page.

If all goes well, your printer should print a single page of test information. You can then print a PostScript test page. Make sure that you have a color cartridge installed in your printer if you defined a printer with color capabilities. You can also create a black-and-white printer with a different name if you don't want to use your color cartridge all the time.
