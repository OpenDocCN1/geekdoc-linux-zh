# Printing Services

In this chapter, we examine how IFS provides services for printing. Historically, printer support on the various flavors of Unix was inconsistent. Manufacturers created drivers for their printers, but often only on a select number of operating systems. This meant that certain printers were supported only on specific platforms.

The Line Printer Daemon (LPD) was used to control the printing of requests on specific queues. Running this application would define the local server as being a print server. Local queues could then be made available to other systems. Clients could then use the LPR application to submit print jobs to a target print server and queue.

The Common UNIX Printing System (CUPS) is designed to be a replacement for the LPD and LPR environments present on these older systems. In SUSE Linux Enterprise Edition 9 and higher, these older printer environments have been deprecated. Because of this, this chapter focuses only on the features available through CUPS.

All the aspects of producing printed output are tightly related. For purposes of this chapter, we subdivide the printing process into the following sections:

+   - Printer configuration
+   - Job lifecycle
+   - Queue management

Each of these categories will be examined using YaST, command-line tools, and the CUPS web interface.