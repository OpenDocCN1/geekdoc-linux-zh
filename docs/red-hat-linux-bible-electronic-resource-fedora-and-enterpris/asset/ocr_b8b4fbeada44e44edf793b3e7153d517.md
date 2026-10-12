properties. It also lets you send test pages to those printers to make sure they are working properly.

The key here is that you are configuring printers that are managed by your print daemon (cupsd for the CUPS service). Once a printer is configured, users on your local system can use it. After that, you can refer to the “Configuring Print Servers” section to learn how to make the server available to users from other computers on your network.

The printers that you set up can be connected directly to your computer (as on a parallel port) or to another computer on the network (for example, from another UNIX system, Windows system, or NetWare server).

# # Configuring local printers

Add a local printer (in other words, a printer connected directly to your computer) with the Printer configuration window using the following procedure. (See the “Choosing a Printer” sidebar if you don’t yet have a printer.) Go to Edit a Printer to change the settings for an existing printer.

> **TIP:** You should connect your printer before starting this procedure. This enables the printer software to autodetect the printer’s location and to immediately test the printer when you have finished adding it.

# # Choosing a Printer

If you are choosing a new printer to use with your Red Hat Linux system, look for one that is PostScript-compatible. The PostScript language is the preferred format for Linux and UNIX printing and has been for many years. Every major word processing product that runs on Red Hat Linux and UNIX systems supports PostScript printing.

If you get a PostScript printer and it is not explicitly shown in the list of supported printers, simply select the PostScript filter when you install the printer locally. No special drivers are needed. Your next best choice is to choose a printer that supports PCL. In either case, make sure that the PostScript or PCL are implemented in the printer hardware and not in the Windows driver.

When selecting a printer, avoid those that are referred to as *Winprinters*. These printers use nonstandard printing interfaces (those other than PostScript or PCL). Support for these low-end printers is hit-or-miss. For example, some low-end HP DeskJet printers use the pnm2ppa driver to print documents in Printing Performance Architecture (PPA) format. Some Lexmark printers use the pnm217k driver to print. Although drivers are available for many of these Winprinters, many of them are not fully supported.

Ghostscript may also support your printer; if it does, you can use that tool to do your printing. Ghostscript (found at *www.ghostscript.com*) is a free PostScript-