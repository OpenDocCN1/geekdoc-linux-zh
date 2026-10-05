# Recommended reading

The kernel allows a process to restrict its own use of physical memory by calling the setlimit call. This facility is also available in the C shell through the built-in limit command. For example, the command

% limit memoryuse 32m

causes all subsequent commands that the user runs to have their use of physical memory limited to 32Mib (Solaris uses memoriesize rather than memory). This feature is roughly equivalent to renice for memory-bound processes.

If a runaway process doesn't seem to be the source of poor performance, investigate other possible causes. The first is an overloaded network. Many programs are intimately bound by the network and it's hard to tell where system performance ends and network performance begins. See Chapter 21 for more information about the tools used to monitor networks.

Some network overloading problems are hard to diagnose because they come and go quickly. For example, if every machine on the network runs a network-related program out of cron at a particular time each day, then there will be a brief but dramatic glitch. Every machine on the net will hang for five seconds, and then the problem will disappear as quickly as it came.

Server-related delays are another possible cause of performance issues. UNIX and Linux systems are constantly consulting remote servers for NFS, Kerberos, DNS, and any of a dozen other facilities. If a server is dead or some other problem makes the server expensive to communicate with, the effects ripple back through client systems.

For example, on a busy system, process may use the geosthent library every few seconds or so. If a DNS glitch makes this routine two seconds to complete, you will likely perceive a difference in overall performance. DNSforward and reverse lookup configuration problems are responsible for a surprising number of server performance issues.

# 29.6 RECOMMENDED READING

COCKSOFT, ADRIAN, AND BILL WALKER Capacity Planning for Internet Services. Upper Saddle River, NJ: Prentice Hall. 2001.

DREPPER, URICH. What Every Programmer Should Know about Memory. lwn.net/Articles/250967.

EZOL, Phillip. Optimizing Linux Performance. Upper Saddle River, NJ: Pren- Hall PTR, 2005.

JOHNSON, S., et AL. Performance Tuning for Linux Servers. Indianapolis, IN: IBM Press, 2005.

+   7. More granular resource management can be achieved through the Class-based Kernel Resource Management functionality; see ckrm.sourceforge.org.

![](bbox=[0.933, 0.678, 0.996, 0.788])