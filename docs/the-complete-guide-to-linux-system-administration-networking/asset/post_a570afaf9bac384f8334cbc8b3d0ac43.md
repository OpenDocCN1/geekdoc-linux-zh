
**security audit** — A review or test of how secure a system really is and what needs to be done to improve its security.

**sendmail** — The most widely used Linux e-mail server.

**server-parsed documents** — See server-side includes.

**server-side includes** — Statements within a text file that are processed on the fly by a Web server when that document is requested.

**session** — A configuration that defines a set of graphical programs to run when a user logs in.

**slave DNS server** — A backup to a master DNS server, containing the same database files as the master DNS server.

**share** — A Microsoft Windows term referring to a resource intended to be shared over a network.

**social engineering** — A method used by attackers to violate user security measures, typically by using clever lies or persuasion to convince a user to divulge a password or other crucial system information. The attacker typically poses as a system administrator or similar person.

**soft mount** — A method of mounting an NFS file system in which NFS will wait for a while if a data request is made and the NFS server does not respond, then the client will give up.

**squashing** — A method of preserving user security in NFS by preventing a user with root access on one system from automatically acquiring root access on an NFS server by virtue of mounting an exported NFS directory.

**Squid** — The most widely used Linux proxy server.

**standalone mode** — Using a network program without support from a superserver such as *xinetd* or *inetd*.

**superserver** — A program that listens on multiple network ports and starts appropriate network service daemons when a client connection arrives for that port. Also called a metaserver. Examples include *inetd* and *xinetd*.

**SWAT** — A browser-based graphical configuration interface for setting up and managing the Samba SMB server.

**System Administration, Networking, and Security (SANS) Institute** — A prestigious and well-regarded education and research organization whose members include most of the leading computer security experts in the country. Also called simply SANS.

**TCP Wrappers** — An application-level access control (security) program that examines incoming network connections when requested by a superserver, then compares the connection details to a configuration file to determine whether the connection is allowed.

**transparent proxy** — A networking technique in which a packet is redirected to a different port on the same computer.

**Trojan horse** — A technique for gaining access to a computer system by having a system administrator execute a program that appears normal but which actually creates a security hole for a cracker or destroys data on the host when it is run.

**virtual hosting** — A feature of the Apache Web server that lets a single copy of Apache serve documents for several Web sites (several domains).

## Review Questions

+   1. Describe at least one advantage and one disadvantage of using xauth instead of xhost.
+   2. The DISPLAY environment variable:
+      a. is used only by xhost, not by xauth
+      b. must be used in conjunction with the --display command-line option
+      c. is only used when connecting via Telnet or SSH
+      d. often includes a 0.0 specification
+   3. The inetd superserver typically starts:
+      a. TCP Wrappers
+      b. an Internet service daemon such as in.ftpd
+      c. xinetd
+      d. standalone services such as a Web server
+   4. TCP Wrappers is configured using:
+      a. /etc/hosts
+      b. /etc/inetd.conf
+      c. /etc/hosts.allow and /etc/hosts.deny
+      d. /etc/services
+   5. Select the meaning of the in.telnetd 192.168.0 line within /etc/hosts.allow:
+      a. Deny access to the Telnet service for all hosts on any network ID starting with 192.168.0.
+      b. Permit access to the Telnet service for all hosts on any network ID starting with 192.168.0.
c. Deny access to the Telnet service for any host except those on any network ID starting with 192.168.0.
d. Permit access to the Telnet service for all hosts except those on any network ID starting with 192.168.0.

# 6. Using a server in standalone mode refers to:

+   a. relying on information in /etc/services so that inetd can initiate it correctly
+   b. not using a superserver to control the server
+   c. resting the server by connecting only to localhost
+   d. relying on TCP Wrappers for security rather than built-in security functions

# 7. To what does the term "metaserver" refer?

# 8. Describe the difference between a DoS attack and a DDoS attack.

# 9. Linux firewalls consist of ______________ organized into ______________ or ______________.

+   a. commands, packets, datagrams
+   b. utilities, secure, insecure
+   c. chains, protocols, filters
+   d. rules, chains, tables

# 10. The three default rule sets used by IP tables are:

+   a. INPUT, FORWARDING, OUTPUT
+   b. INPUT, FORWARD, OUTPUT
+   c. DENY, REJECT, ACCEPT
+   d. NETFILTER, IPTABLES, SSH

# 11. IP tables can specify the following actions:

+   c. -i MASQUERADE
+   d. -A FORWARD

# 14. By using a transparent proxy configuration, a system administrator can:

+   a. securely transmit packets over the Internet using a variety of ciphers
+   b. hide logging and other security features from users sending packets through a LAN
+   c. redirect packets destined for a given port on a remote system to a different port on the router
+   d. cache packets in the router to provide higher performance for all users on the LAN

# 15. The __________ utility is the preferred tool for querying name servers for administrative or troubleshooting purposes.

+   a. nslookup
+   b. named
+   c. dig
+   d. host.conf

# 16. Modules allow the Apache Web server to:

+   a. Interact cleanly with the Linux kernel.
+   b. Load and unload functionality by recompiling Apache.
+   c. Make new functionality part of Apache as it is running.
+   d. Use LoadModule to specify programs that are loaded when a user requests a certain Web document.

# 17. Server-parsed documents are:

+   a. documents stored on the Web server that Apache examines or processes at the moment they are requested by a client
+   b. module information files that Apache examines or processes when the server starts up
+   c. document files that Apache can preload into memory to speed responses to browser queries
+   d. another name for virtual-hosted documents

# 18. Computer security for a host is often divided into four areas of concern:

+   a. physical, user, file, and network
+   b. network, firewall, VPN, and tunneling
+   c. physical, user, firewalls, intrusion detection
+   d. Trojan horse, buffer overflow, password cracking, worms and viruses

# 19. What is the purpose of /etc/nologin?

X resource — The separate screen elements of a graphical application, such as scroll bars, text fonts, and titles bars.

xdm — The program that provides a graphical login screen in Linux. Replaced by the very similar program gdm in GNOME, or kdm in KDE.

XDMCP — A protocol that allows remote hosts to use X running on a Linux system to provide a graphical login display.

zone — A part of the DNS domain tree for which a particular DNS server has authority to provide information.

zone information files — The files referred to in named.conf that contain detailed information about specific zones: the information that a DNS query seeks.

# 20. The X Window System files are normally located in which subdirectory in Linux?

+   a. /etc/X
+   b. /usr/share
+   c. /opt/kde
+   d. /usr/X11R6

# 21. Choosing not to run X:

+   a. is pointless because it runs in the background anyway
+   b. can cause configuration problems on server-based systems
+   c. saves the system resources that the X server would have consumed
+   d. would be unreasonable on a Linux system used as an Internet server

# 22. The _____________ program provides an insecure but easy-to-use method of permitting other computers to use your X server.

+   a. xhost
+   b. xauth
+   c. Xsession
+   d. xinit

# 23. Graphical programs use the X server that is:

+   a. defined by the --display option of the command, unless a DISPLAY variable defines a different X server
+   b. always on the same system as the program that is running
+   c. defined by the DISPLAY environment variable, or the --display option if it is included with the command
+   d. listed in the xinitrc script file

# 24. The command normally used to start the X Window System from a text-mode prompt in run level 3 is:

+   a. xinit
+   b. startx
+   c. xdm
+   d. xinitrc

# 25. The xdm, gdm, or kdm display manager is initially started by the _____________ program (or script).

+   a. init
+   b. startx
+   c. xinit
+   d. xrlb
