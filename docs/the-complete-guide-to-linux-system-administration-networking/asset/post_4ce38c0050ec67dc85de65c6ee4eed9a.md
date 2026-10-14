
first prompt. The system boots from the CD and then asks you to select a language, keyboard, and whether to start networking devices (which you may want to access as needed to repair the system). After this, the system informs you that it will search for Fedora installations. You can either select Continue to mount the installation under /mnt/sysimage, Read-Only to make that file system read-only, or Skip to not mount any file systems. In any case, you then see a text-mode shell prompt. At this shell prompt, you can use whatever utilities are appropriate to diagnose and repair problems. If you selected Skip at the last prompt while entering rescue mode, you need to manually mount the correct disk partition before you can access any data on your Fedora installation. Entering exit in the rescue shell causes the system to reboot.

## CHAPTER SUMMARY

- X Window System configuration is handled by the Linux installation program, but can be adjusted using several graphical tools such as xvidtune and system-config-display.
- Many scripts are used by the X Window System to determine exactly what programs to start as the graphical environment is started. These scripts are less relevant when using a desktop such as GNOME or KDE.
- Features of X such as resources, fonts, and interaction with the mouse can all be configured using simple command-line utilities. Some features overlap those controlled by desktop interfaces such as GNOME, which are also configurable using graphical preferences tools in those desktops.
- The graphical login screen is handled by a program called xdm, or gdm and kdm in GNOME and KDE. This screen can be accessed remotely using the XDMCP protocol.
- Graphical programs in Linux can be displayed remotely to any system that has an X server installed. Security for this feature is provided by either xhost or xauth security, the second being harder to configure but much more secure. Remote applications are often run over an SSH connection to prevent security breaches.
- Computer security is often divided into categories that include physical, user, file, and network security.
- Examples of security attacks include password cracking, Trojan horses, buffer overflow attacks, DoS and DDoS attacks, viruses, and worms.
- Both attackers and system administrators use a variety of security software tools. These include tools for port scanning (such as nmap), for packet sniffing (such as tcpdump and Ethereal), IDS programs, and security auditing tools such as SAINT.
- Several organizations support computing professionals as they try to maintain secure systems. Two of the most important are CERT/CC and SANS.
- Linux uses a firewalling and packet-filtering system called NetFilter, which uses IP tables to define rules used to process network packets. This feature of Linux supports IP masquerading, transparent proxying, and other advanced routing and packet control features.
- A DNS server on Linux is implemented using the named daemon, with zone information files stored on a master or slave DNS server providing data in response to client requests. A caching name server does not act as a master or slave for any domain, but only stores information for quicker local access.
- NFS permits remote users to mount a file system on an NFS server as a part of their directory structure. The directories that are available are defined on the server in the /etc/exports file.
- The Samba suite provides Microsoft Windows-compatible file and print services using the SMB and CIFS protocols. The Samba server can be configured manually by editing the smb.conf file or using the SWAT browser-based configuration tool.
- Squid is a proxy server that provides caching and many other features to clients on a local network.
- Apache is a Web server that is included with most Linux distributions. It is configured using the httpd.conf file, and controlled using the apachectl program. It supports such advanced features as virtual hosting and a modular architecture.
- The most popular MTA (e-mail server) is sendmail. It is challenging to configure, but provides many useful features such as forwarding and aliases. The m4 program is usually used to simplify configuration of sendmail.
- Superservers such as inetd and xinetd are often used to manage multiple network services. These programs start the needed network service only when a client request for that service arrives. These programs use built-in security to control who can access each network service, or else they rely on the TCP Wrappers program, which in turn uses the hosts.allow and hosts.deny files to determine which connections should be permitted for a specific network service.
- Systematically eliminating possible problems is a sound methodology for troubleshooting. The more you understand about the underlying technology and helpful utilities, the easier it is to locate and fix problems.
- Linux includes numerous utilities to help you learn about and configure hardware. Networking problems can be very challenging, but basic programs such as ping and traceroute can help isolate problems.
- A boot disk or rescue disk is a huge time saver when a system goes down. When these are not available, using a Red Hat Linux or Fedora CD to enter rescue mode is also useful. In this mode, you can mount hard disk partitions and use a variety of system utilities to track down and fix problems.

## COMMAND SUMMARY

| Command | Description | Example |
|---|---|---|
| apachectl | Control program used to manage the Apache Web server | apachectl -k start |
| dig | A utility used to query specific DNS servers for specific resource records | dig @ns.xmission.com www.xmission.com any |
| dnscache | A minimalist DNS caching server | dnscache |
| ethereal | Graphical program that displays the contents of and statistical information about network packets; a packet sniffer | ethereal |
| exportfs | Causes the NFS daemon to use an updated (recently edited) version of the /etc/exports file | exportfs |
| hoststat | Displays the status of hosts that have recently sent e-mail to your sendmail daemon | hoststat |
| inetd | A widely used superserver program | inetd |
| iptables | Configures rules within the IP tables (packet filtering/firewall) part of the Linux kernel; common options are listed in Table 15-1 | iptables -A INPUT -p udp -s 0/0 --sport 67:68 -d 0/0 --dport 67:68 -i eth0 -j ACCEPT |
| iptraf | A popular "packet sniffer" program for viewing network activity on a LAN | IPTraf |
| lokkit | A text-mode program that sets up basic firewall rules according to the level of security protection desired | lokkit |
| lspci | Lists information about PCI devices on the system | lspci |
| m4 | A program that converts a text file containing configuration parameters into a complete sendmail.cf file | m4 /etc/mail/sendmail.mc > /etc/sendmail.cf |
| mailq | Displays a list of messages waiting to be sent out | mailq |
| mailstats | Displays a summary of the amount of e-mail traffic that sendmail has handled | mailstats |
| mkbootdisk | Creates a boot disk | mkbootdisk --device /dev/fd0 2.4.22 |
| named | The Linux program that implements the DNS protocol to create a DNS server; part of the BIND collection of programs | named |
| newaliases | Reconfigures the aliases (alternate names) stored in /etc/aliases after changes have been made to that file; used in connection with the sendmail e-mail server | newaliases |
| nfsd | The main daemon used by NFS to provide access to local file systems by remote clients | nfsd |
| nmap | The most widely used port-scanning utility | nmap -sS www.myplace.net |
| nmapfe | A utility that acts as a graphical front end to the nmap command; requires the GNOME desktop | nmapfe |
| nmbd | The Windows name-server component of the Samba suite of programs | nmbd |
| nslookup | A utility used to query DNS servers for resource records | nslookup www.xmission.com |
| pdbedit | Edit the Samba user account database | pdbedit -a -u abutler |
| pinfo | Provides color-coded display of info and man pages | pinfo bash |
| rmdc | A control program used to manage the named daemon | rmdc reload |
| rpc.mountd | Daemon used by NFS to permit mounting of local file systems by remote clients | rpc.mountd |
| rpc.quotad | Daemon that tracks user disk space quotas for remotely mounted file systems | rpc.quotad |
| rpc.statd | Daemon that manages NFS-mounted file systems when the remote NFS server to which a mount point refers has crashed | rpc.statd |
| setserial | Used to display and configure serial port settings | setserial /dev/ttyS0 |
| smbd | The file and print sharing daemon for the Samba suite of programs | smbd |
| startx | Starts the X Window System from a text mode prompt | startx |
| system-config-bind | Graphical utility for configuring the named DNS server | system-config-bind |
| system-config-display | Graphical program used to change screen resolution or color depth | system-config-display |
| system-config-securitylevel | Graphical utility for configuring an overall security level in Red Hat Linux and Fedora | system-config-securitylevel |
