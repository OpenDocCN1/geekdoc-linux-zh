+   6. The printer should now be added to your CUPS facility. Now click one of the following buttons:

+   - Print Test Page — Determines whether the printer is working by printing a page.

+   - Stop Printer — Temporarily stops print jobs from printing.

+   - Reject Jobs — Prevents print jobs from even being queued.

+   - Modify Printer — Lets you change the name, location, and/or description of the printer.

+   - Configure Printer— Enables you to change details about the printer, such as filters used and image resolution (dots per inch).

+   - Delete Printer — Removes the printer definition completely.

+   - Add Printer — Enables you to go back and add another printer.

At this point you should have a working local printer. Because CUPS uses many of the same interfaces as LPRng, you can continue throughout the rest of this chapter to choose a printer and use various printing commands to control how you use your print service (whether it is LPRng or CUPS).

# Choosing a Printer

If you are choosing a new printer to use with your Red Hat Linux system, look for one that is PostScript-compatible. The PostScript language is the preferred format for Linux and UNIX printing and has been for many years. Every major word-processing product that runs on Red Hat Linux and UNIX systems supports PostScript printing.

If you get a PostScript printer and it is not explicitly shown in the list of supported printers, simply select the PostScript filter when you install the printer locally. No special drivers are needed. Your next best choice is to choose a printer that supports PCL. In either case, make sure that the PostScript or PCL are implemented in the printer hardware and not in the Windows driver.

When selecting a printer, avoid those that are referred to as *Winprinters*. These are printers that use nonstandard printing interfaces (that is, those other than PostScript or PCL). Support for these low-end printers is hit-or-miss. For example, some low-end HP DeskJet printers use the pnm2ppa driver to print documents in Printing Performance Architecture (PPA) format. Some Lexmark printers use the pbm217k driver to print. Though there are drivers available for many of these Winprinters, many of them are not fully supported.

Instead of a PostScript printer, Ghostscript may support your printer; if it does, you can use that tool to do your printing. Ghostscript (found at `www.aladdin.com`) is a free PostScript- interpreter program. It can convert PostScript content to output that can be interpreted by a variety of printers.