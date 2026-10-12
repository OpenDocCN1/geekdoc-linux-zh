# Check for Altered System Files

Make sure files on your system have not been altered. If a hacker gains access to your system, he may be able to change your executables to contain trojan horses and the like. You can use programs like tripwire to take snapshots of your filesystem (even daily) and compare them to make sure nobody has altered your system files. Tripwire can be obtained from ftp://coast.cs.purdue.edu/pub/COAST/Tripwire.

Frequently running programs that check your system for holes is also a good idea. Nmap, SAINT, and COPS are good programs to run frequently to make sure nothing is amiss on your system.

# Be Aware of the Latest Threats

CERT (Computer Emergency Response Team) provides a set of attack warnings and system bugs as they become available. The CERT Web page is an excellent place to look for advisories (http://www.cert.org), and the Red Hat site contains security information about Red Hat itself (http://www.redhat.com/cgi-bin/support). See Figure 25.2.

FIGURE 25.2
The Red Hat Web site is a good place to keep up on security issues.

![](bbox=[0.35, 0.6, 0.88, 0.9])