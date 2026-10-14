The lp command is the command-line interface for submitting print jobs. Multiple options can be entered with the lp command to specify destination, number of copies, and other options. lpadmin configures spooling systems to describe printers, classes, and set the default printer.

# AIX

AIX provides a very robust set of print services. IBM has put a lot of time and effort into developing a robust print system. AIX is interoperable with BSD and SysV systems. It supports both the lp and lpr commands. The underlying structure, however, is quite different from BSD and SysV systems. AIX print services utilize the /etc/qdaemon to schedule printing jobs. The starting and stopping of qdaemon is controlled in the /etc/inittab file. The /etc/qconfig file contains descriptions of the queues and devices available for print services. The qdaemon reads the qconfig file on startup and when qdaemon is refreshed. The /usr/sbin/lpd daemon is responsible for inbound TCP/IP remote printing requests. The lpd daemon can be started at system boot (add entry to /etc/inittab file) or via the command line.

Manipulation of print jobs and queues can be accomplished in many different ways in AIX. The enq command can start and stop queues and printers. It can also change the priority of a job, remove a job from a queue, and list the status of a printer's queue. enq is a very useful and powerful print services command.

AIX offers two GUIs to set up print services. Both GUIs are simple to use and do all of the hard work for you. SMIT provides a graphical interface that allows you to configure, start, stop, and manipulate all local printers and queues. All that is required is to enter the command smit and select the Print Spooling button under System Management. The other GUI is the Web-based System Manager (WSM). WSM is located at /usr/bin/wsm, and it provides a Web-based interface to manage an AIX system. Click the Printer Queues icon and you can perform all similar functions contained in SMIT.

enq can start and stop queues and printers. It can also change the priority of a job, remove a job from a queue, and list the status of a printer's queue.

# HPUX

HPUX is based on SysV print services. It has enhanced the lpsched daemon to spool jobs to a remote BSD printer. HPUX can also accept remote jobs from a BSD system through rlpdaemon. The HP Distributed Print