your system. Most are very easy to configure. The HP Jetdirect print server is the most popular but not the only print server available.

The first step is to connect the print server to the network and set the IP address. This process varies on print servers, so follow the manufacturer’s guidelines on how to do this. Next, install the print server software and follow the manufacturer’s guidelines for configuring the printer. The vendor’s software configures everything—no additional software configuration is required.

For printers with a parallel or serial connection, you must use the Solaris tools to configure the operating system to recognize the printer.

# BSD Versus SVR4 Printing Software

The software that drives the UNIX printing process is an area in which the two UNIX versions, BSD and SystemV, are similar and yet very different. The two print systems are similar in that both are based on the concept of spooling. Both SystemV and BSD print services support the concept of an interface program, which acts as a filter through which all output sent to the printer is passed. Example uses of an interface program include

+   - Adding a banner page—Most UNIX systems automatically add a banner page to the front of a print job. The purpose of the page is to identify the owner of the printer output.
- Adding or removing a line feed character—UNIX uses just the line feed character to separate lines. The first problem you might encounter when testing a printer is that the text comes out in a stair-step manner. Most printers have a carriage return/line feed and auto line-feed dip switch that controls what the printer will use. The stair-step problem can be fixed by modifying the interface program that performs the necessary translation on all output going to the printer or by setting the printer’s dip switch to the setting recommended by the hardware manufacturer.

The differences between BSD and SystemV are in the configuration files and the spooling directories, which are configured automatically by the Solaris operating system. There are also differences in the way the lp daemon handles print jobs as compared to the lpd daemon in BSD.

# BSD Print Service

Each printer connected to a BSD system must have its own spooling directory that is serviced by one lpd daemon. The spool directories are located in the /var/spool/lpd directory. Each printer has its own lpd daemon. In BSD, lpd accesses the file /etc/printcap for any information it requires concerning the printer. The /etc/printcap file is the system’s printer database file and stores all of the necessary information about all printers connected to the system. To use a printer, that printer must have an entry in the /etc/printcap file. The lpr function is BSD’s equivalent to lp under SystemV. If users want to print something, they use the lpr command, which sends the necessary information to a specified spooling directory.