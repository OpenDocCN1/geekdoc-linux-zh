# CHAPTER 28 Printing

CUPS.org Home Administration Classes Help Jobs Printers

# CUPS 2.0.2

CUPS is the standards-based, open source printing system developed by Apple Inc. for OS X® and other UNIX-like operating systems.

# CUPS for Users

# CUPS for Administrators

# CUPS for Developers

+   Overview of CUPS

+   Adding Printers and Classes

+   Introduction to CUPS Programming

+   Command-Line Printing and Options

+   Managing Operation Policies

+   CUPS API

+   User Forum

+   Using Network Printers

+   Filter and Backend Printing

+   cupsd.conf Reference

+   HTTP and IPP APIs

+   Developer Forum

Figure 28-1 CUPS administration web page

possibilities exist under each method. The modes with which CUPS addresses the printer resources are specified by using the device Uniform Resource Information (URI) in CUPS. These are examples of possible device URIs that can be configured in CUPS:

+   * Directly connected (local) A stand-alone home system running Linux most likely be connected to the printer directly through the use of a printer cable (commonly a parallel cable) or will perhaps connect a Universal Serial Bus (USB) cable to the printer's USB port. This is an example of a locally attached printer. In CUPS limbo, some device URIs for a locally attached printer are specified as follows:

+   * /dev/lp* For a printer attached to the parallel port

+   * serial/dev/tty* For a printer attached to the serial port

+   * /dev/usb/lp* For a printer attached to the USB port

+   * IPP (network) The Internet Printing Protocol allows a printer to be accessed over the network. Most modern operating systems support this protocol, so that this is usually not a problem. An example of an IPP device URI in CUPS is `ipp://hostname/ipp/`.

+   * LPD (network) CUPS supports printers that are attached to systems running the Line Printer Daemon (LPD). Most UNIX/Linux systems (even some Windows servers) support this daemon. So if a printer is attached to a host that supports LDP, CUPS can be used to make that printer available on the network to other hosts that do not necessarily support LDP. Virtually all HP laser printers