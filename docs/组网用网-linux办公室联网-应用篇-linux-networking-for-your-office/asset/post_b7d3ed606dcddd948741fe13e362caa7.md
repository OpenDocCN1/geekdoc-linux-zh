
## NOTE

Some printers attach directly to an Ethernet network, and you can purchase small adapters that let you connect parallel-port printers to Ethernet networks without using a computer as a server. If you're using such a printer, you access it as a remote printer. Consult the printer's (or adapter's) documentation to determine whether to select the Ipd, SMB, or NetWare queue type. If the printer or adapter uses AppleTalk, "Printing from Linux to Mac Printers," p. xxx, provides instructions on setting up an appropriate Linux queue.

If you choose Local Printer, Linux attempts to locate parallel port hardware to tell you what parallel ports are available. In my experience, Red Hat often gets this wrong, missing ports that do exist, so don't be alarmed if a dialog box lists all the parallel ports as "not detected." You then see the Edit Local Printer Entry dialog box, as shown in Figure 14.5. This is where you enter basic information on what you want to call the printer, to what port the printer is attached, and so on.

![](img/5d4d3092919d1d16884788127447cc6d_389_0.png)

## FIGURE 14.5

If you set up a networked printer rather than a local one, you have slightly different options in the network equivalents of the Edit Local Printer Entry dialog box.

The name you enter in the Names field is the Linux printer queue name. You can actually enter several names, separated by vertical bars (|), to make the queue available locally under several names. These names need bear no resemblance to the name under which the printer is available under Samba, Netatalk, or on remote UNIX systems. Likewise, the Spool Directory entry is well hidden from users, even local Linux users. Nonetheless, it's best to name the spool directory after the primary printer name. The Printer Device is the device file for the printer—/dev/lp0 for the first printer port, /dev/ttyS0 for the first serial port, and so on. If you deselect Suppress Headers, Linux prints a header identifying the user who queued the print job, which can be convenient for identifying the owners of print jobs. (Netatalk queues all print jobs under a single username, however, so this option isn't terribly useful on a Macintosh network.)

Finally, you set the model of printer and print options, such as resolution, by clicking the Select button next to the Input Filter field. You get the Configure Filter dialog box, as shown in Figure 14.6. For non-PostScript printers, this dialog box lets you set the Ghostscript options for the printer.

![](img/5d4d3092919d1d16884788127447cc6d_390_0.png)

## FIGURE 14.6

The Configure Filter dialog box is the core of the printer configuration utility; it lets you select the printer, its resolution, and assorted other options.

### TIP

If you want to create a raw queue for printing with the client OSs’ native drivers for the printer, do not select an input filter. When you leave the Input Filter field blank, Red Hat doesn’t set an input filter, so lpd passes the print data to the printer unchanged.

Options you can set in the Configure Filter dialog box include the following:

- Printer Type—If you see your printer model in this list, select it. If not, select something close. Most laser printers today emulate some variety of Hewlett-Packard LaserJet, so select the model of LaserJet that the printer claims to emulate. For inkjet printers, select the model that’s closest to the one you use. If you have any model of PostScript printer, select PostScript printer. If you’re certain you’ll never need to print raw text from Linux, or if your PostScript printer can handle raw text, you may leave the Input Filter field of the Edit Local Printer Entry dialog box blank instead of selecting PostScript printer.
- Driver Description—You don’t actually set or select anything in this field. Instead, it provides additional information concerning the Printer Type item you’ve selected.
- Resolution—Many printers provide a choice of resolutions. Select the resolution you want to use.
- Paper Size—Choose the paper size that you normally use in this printer.
- Color Depth/Unip rint Mode—The options in this field vary from one printer to another. They generally relate to paper types, printer-specific options, or dithering options that affect the appearance of printed color. You set the resolution here, rather than in the Resolution field, for some printers.
- Send EOF after job to eject page?—On some printers, you must select this option or else the page isn’t printed or isn’t ejected from the printer when you print text pages.
- Fix stair-stepping text?—Some printers stair-step their text, as shown in Figure 14.7, when printing ASCII text from Linux. You can select this option to correct the problem.

Type the following:

```
/usr/bin/yes
```

to see a string of ys appear

## Figure 14.7

Stair-stepped text results from a printer expecting DOS-style end-of-line characters and not understanding UNIX/Linux-style end-of-line characters.

- Fast text printing—If you select this option with a non-PostScript printer, Linux sends text files to the printer unfiltered. If you deselect this option, Linux first converts the text to PostScript, which typically results in slower printing.
- Pages per output page—You can reduce the size of each input page to fit several input pages on each physical sheet by using this option.
- Margins—This option adjusts the margins between multiple selected output pages.
- Extra GS options—Any text you enter here gets passed to Ghostscript as an extra option. This could be useful for enabling features that printtool doesn’t offer.

## Testing Your Printer Setup

When you’ve set all the options you want, click OK in the Configure Filter dialog box, and then in the Edit Local Printer Entry dialog box. You should now see a new entry in the main printtool window. You can test the configuration as follows:

- 1. Choose lpd, Restart lpd to be sure lpd is aware of the new printer configuration.
- 2. Select the printer you want to test.
