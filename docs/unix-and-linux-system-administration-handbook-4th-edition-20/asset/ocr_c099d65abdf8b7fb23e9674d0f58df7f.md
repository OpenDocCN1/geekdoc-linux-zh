# Chapter 11 Syslog and Log Files

SDSC Secure Syslog (from the San Diego Supercomputing Center) is also known as high-performance syslog. It provides a forensically sound auditing system by implementing the specifications of RFC3195 (Reliable Delivery for syslog). It was designed with high-traffic sites in mind and contains a number of performance optimizations. You can download the source from SourceForge:

sourceforge.net/projects/sdcsyslog

Ryslog, another powerful, next-generation alternative, is the default shifted with several Linux distributions, including Fedora. Ryslog is multithreaded and aims for high reliability and robust security. It supports over TCP (as opposed to UDP, by the original syslog) and can use SSL, which may be required at some sites for regulatory reasons. Ryslog can even log to databases. Learn more at ryslog.com.

# Linux kernel and boot-time logging

![](bbox=[0.195, 0.385, 0.233, 0.423])

The kernel and system startup scripts present some special challenges in the domain of logging. In the case of the kernel, the problem is to create a permanent record of the boot process and the operation of the kernel without building dependencies on any particular filesystem or filesystem organization. In the case of the startup scripts, the challenge is to capture a coherent narrative of the startup procedure without penting any of the system daemon to a startup log file, interfering with any program's logging, or gooping up the startup scripts with double entries or redirection.

Kernel logging is dealt with having the kernel store its entries in an internal buffer of limited size. The buffer is large enough to accommodate messages about all the kernel's boot-time activities. The system has come all the way up, a user process accesses the kernel's log buffer and makes a final disposition of its contents. The dmesg command is the best way to view the kernel buffer; the output even contains messages that were generated before started.

The kernel's ongoing logging is handled by a daemon called klogd. The functions of klogd are a superset of dmesg; in addition to dumping the kernel log exiting are generated and pass them along to a file or to syslog. In normal operation, klogd runs in this latter mode. Syslog processes the messages according to the instructions for the “kern” facility. They are typically sent to /var/log/messages or /var/log/syslog.

Our example distributions' startup scripts do not use dmesg -c flag when they make their initial dump of log messages, so the kernel's message buffer is not reset. When klogd starts up, it finds the same set of messages seen by dmesg in the buffer and submits them to syslog. For this reason, some entries appear in both the dmesg and boot.msg file and in the system's primary syslog file.