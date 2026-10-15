script, and the service won’t run. You can still start it manually if you like, however, by typing the script’s name and, if needed, start or some other parameter to signal startup. You may need to disable the service again if you upgrade it, however, because the upgrade process may place a new initialization script in /etc/rc.d/init.d.

+   Direct startup—You may need to remove an entry from /etc/rc.d/rc.local or some other startup file for some services. Most servers you install from RPMs don’t add lines to startup files in this way, but you may have done so for a few servers, particularly those that you compiled yourself. You can comment out such startup lines by preceding them with pound signs (#).

# NOTE

> Different distributions sometimes use different service startup protocols. Slackware, for instance, places most of its network startup commands in the /etc/rc.d/rc.inet1 and /etc/rc.d/rc.inet2 files. Consult your distribution’s documentation or a good book about your distribution for details.

Sifting through configuration files isn’t easy, and you may miss some services in this way. Therefore, you may want to use a port scanner, such as Nessus (http://www.nessus.org), to check what ports are open. There are also Internet-based services that will do this job, such as one available at http://www.dsireports.com. Port scanners may also be useful in checking the effectiveness of packet filtering firewalls or other measures.

# Using TCP Wrappers

One basic security measure employed by default in Red Hat Linux is known as TCP Wrappers. This is a tool that screens incoming connection requests. The TCP Wrappers daemon, tcpd, sits between inetd and the daemon for the requested service, as illustrated by Figure 24.3. When inetd receives a request for service, inetd passes that request, fairly indiscriminately, to the associated server—inetd isn’t primarily a security tool, but one to reduce the load on the system. TCP Wrappers, by contrast, serves as a filter, much as a personal secretary can filter phone calls. (My own personal fantasy is to have such a secretary who shields me from telemarketers, while quickly and unobtrusively passing calls from my friends, family, and editors at Sams. TCP Wrappers can do the equivalent for Linux daemons, but sadly not for voice telephone calls.)