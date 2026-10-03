♦ Adding or removing a line-feed character. UNIX uses just the line-feed character to separate lines. The first problem you might encounter when testing a printer is that the text comes out in a stair-step manner. Most printers have a carriage return/line feed and auto line-feed dip switch that controls what the printer will use. The stair-step problem can be fixed by modifying the interface program that performs the necessary translation on all output going to the printer or by setting the printer’s dip switch to the setting recommended by the hardware manufacturer.

The differences between BSD and SVR4 are in the configuration files and the spooling directories, which the Solaris operating environment configured automatically. Differences also exist in the way that the lpsched daemon handles print jobs as compared to the lpd daemon in BSD.

# BSD Print Service

Each printer connected to a BSD system must have its own spooling directory that is serviced by one lpd daemon. The spool directories are located in the /var/spool/lpd directory. Each printer has its own lpd daemon. In BSD, lpd accesses the file /etc/printcap for any information it requires concerning the printer. The printcap file is the system’s printer database file that stores all the necessary information about all printers connected to the system. To use a printer, that printer must have an entry in the /etc/printcap file. The lpr function is BSD’s equivalent to lp under SVR4. If users want to print something, they use the lpr command, which sends the necessary information to a specified spooling directory.

# SVR4 Print Service

In SVR4, one lpsched daemon services all printers. The lpsched daemon is continually running and provides the “power” for the print service. Only one instance of lpsched should be running at any one time.

The LP print service performs the following functions:

+   ♦ Administers files and schedules local print requests
♦ Receives and schedules network requests