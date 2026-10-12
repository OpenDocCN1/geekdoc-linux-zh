# # PostScript Printers

If you want a print spooler specifically designed for PostScript printers, give Dave Chappell's PPR a try. PPR works with printers attached to parallel, serial, and AppleTalk (LocalTalk) ports, along with other network interfaces. PPR can also work much like other non-PostScript printer filters and converts a number of graphics file formats for printing.

You can find PPR at http://ppr-dist.trincoll.edu/pub/ppr/.

# # Infrared Printer Support

If you are fortunate enough to have a printer with infrared support (such as the Canon BJC 50 or BJC 80, HP LaserJet 6MP or HP LaserJet 100TN) and a Linux system with an infrared port (such as a laptop), here is good news: You can print without a printer cable! Recent efforts in Linux device driver development have yielded infrared printing (and networking) support, and the latest Linux kernels now have IrDA support built in. IrDA support is supplied as a series of loadable kernel modules and support features such as system logging, networking, serial-port emulation, and printing.

You'll definitely need to read Warner Heuser's IR-HOWTO, found at http://home.snafu.de/wehe/IR-HOWTO.html. Development of IrDA for Linux is still experimental, but offers the promise of wireless networking, communication, PalmOS support, and of course, printing! The basic steps to enable infrared printing involve

+   1. Determining the correct `/dev/ttySX` device used by computer for the IrDA port.
+   2. Enabling your system's infrared port.
+   3. Creating the correct device(s), using the irattach command to start the port, then using the ircmm module to connect to the port.
+   4. Crafting a correct `/etc/modules.conf` entry to enable the port when booting.
+   5. Ensuring your setup correctly detects and identifies a remote IrDA device.
+   6. Testing the connectivity of your printer.

After you have configured your system, the easiest way to print to an infrared printer is to create a special printer entry in your /etc/printcap printer database with a special name, such as irlp. Laptop users may need to press certain function keys to disable an existing serial port, or to enable an IR port.

To download the latest set of irDA utilities browse to http://www.cs.uiuc.no/linux-irda/. For a detailed description of a working irDA printing system for the Canon BJC 80, browse to Dave Davey's page at http://www.physiol.usyd.edu.au/daved/linux/bjc-80.html.