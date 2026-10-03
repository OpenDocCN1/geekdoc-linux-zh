with 20–25MB of disk space allocated to /var is probably sufficient. However, if many users are printing lengthy PostScript files, they will probably fill up the spooling space quite frequently. When /var fills up and users cannot queue their jobs for printing, workflow is interrupted. The size of /var is set when the operating system is loaded and disks are partitioned.

For SunOS users, the SVR4 lp program is equivalent to the BSD lpr print program. In SunOS, the print spooler is located in /usr/spool. When Sun switched from SunOS 4.x (which was based on BSD UNIX) to SunOS 5.x (which is based on SVR4 UNIX), print systems between BSD and SVR4 were quite different. Throughout this chapter, I'll make reference to the BSD print system for system administrators who might be familiar with it. The BSD printing protocol is an industry standard. It is widely used and provides compatibility between different types of systems from various manufacturers. For sites that have a mix of BSD and SVR4 UNIX, Sun has provided compatibility for both print systems in Solaris.

> **CAUTION**

Some print jobs consume large amounts of disk space. In fact, one of my clients had a report that consumed more than 800MB when it was spooled to the printer. When /var runs out of disk space, many system functions cannot continue, such as printing, message logging, and mail. Make sure you provide adequate space in /var when setting up your system.

# The LP Print Daemons

The /usr/lib/lpsched daemon is the UNIX utility responsible for scheduling and printing in Solaris 8. Sometimes this is referred to as the lp daemon. The lpsched print daemon is the UNIX process responsible for taking output from the spooling directory and sending it to the correct printer. lpsched also tracks the status of printers and filters on the print server. Again, for SunOS users, lpsched is equivalent to lpd in BSD UNIX.

> **NOTE**

/usr/lp/lpsched is actually a soft link to the binary named /usr/lib/lp/lpsched.

The /usr/sbin/inetd daemon is started at bootup and listens for service requests on all the ports associated with each of the services listed in its configuration file /etc/inetd.conf, which was described in Chapter 8, “System Security”. When a request arrives, inetd executes the server program associated with the service.

The /usr/lib/print/in.lpd daemon is started by inetd and implements the network listening service for the print protocol. When inetd receives a print request, in.lpd is started to service the connection. The in.lpd daemon exits after the request has been serviced.