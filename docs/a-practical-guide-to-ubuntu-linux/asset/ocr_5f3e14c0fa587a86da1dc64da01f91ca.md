# INTRODUCTION

LPD and LPR Traditionally, UNIX had two printing systems: the BSD Printer Daemon (LPD) and the System V Line Printer system (LPR). Linux adopted those systems at first, and both UNIX and Linux have seen modifications and replacements for these systems. CUPS is the default printing system under Ubuntu.

CUPS CUPS (Common Unix Printing System) is a cross-platform print server built around IPP (Internet Printing Protocol), which is based on HTTP. CUPS provides many printer drivers and can print different types of files, including PostScript. Because it is built on IPP and can be written to, CUPS runs under many operating systems, including Linux and Windows. Other UNIX variants, including Mac OS X, cups; recent versions of Windows have the ability to print to IPP printers. Thus CUPS is an ideal solution for printing in a heterogeneous environment. CUPS provides System V and BSD command-line interfaces and, in addition to IPP, supports LPD/LPR, HTTP, SMB, and JetDirect (socket) protocols, others.

IPP The project (www.pwg.org/ipp) began in 1996, when Novell and several other companies designed a protocol for printing over the Internet. IPP enables users to

+   * Determine the capabilities of a printer.
* Submit jobs to a printer.
* Determine the status of a printer.
* Cancel a print job.

IPP is a client/server protocol in which the server side can be a print server or a network-capable stand-alone printer.
Printers and queues On a modern computing system, when “send a job to a printer,” you actually add the job to the list of jobs waiting their turn to be printed on. This list is called a print queue or simply a queue. The phrase configuring (or setting up) a printer is used when configuring a (print) queue. This chapter uses these phrases interchangeably.

# PREREQUISITES

Install the following packages (most are installed with the Base Ubuntu system):

+   * cups-common
* cups-bsd (optional; BSD printing commands)
* cups-client (optional; System V printing commands)
* openprinting-ppds (PPD files)
* openprinting-ppds-extra (optional; more PPD files)
* system-config-printer-gnome (optional; graphical printer tool)