
# Securing Your Network

Generating the database...
*** Processing Unix File System ***

...
Wrote database file: /var/lib/tripwire/shuttle2.twd
The database was successfully generated.

Note that not all the output is shown here. After Tripwire has created its database (which is a snapshot of your filesystem), it will use this baseline along with the encrypted configuration and policy settings under the /etc/tripwire directory to monitor the status of your system. You should then start Tripwire in its integrity checking mode, using a desired option. (See the Tripwire manual for details.) For example, you can have Tripwire check your system, and then generate a report at the command line, like so:

```
# tripwire -m c
```

No output is shown here, but a report will be displayed in this example. The output could be redirected to a file, but a report will be saved as /var/lib/tripwire/report/hostname-YYYYMMDD-HHMMSS.twr (in other words, using your host's name, the year, month, hour, minute and seconds). This report can be read using the twprint utility, like so:

```
# twprint --report-report -r /var/lib/tripwire/report/shuttle2-20020119-181049.twr | less
```

Other options, as emailing the report, are supported by Tripwire, which should be run as a scheduled task by your system's scheduling table, /etc/crontab on off-hours. (It can be resource intensive on less powerful computers.) The Tripwire software package also includes a twadmin utility you can use to fine-tune or change settings or policies, or perform other administrative duties.

# Devices

Do not ever advertise that you have set a NIC to promiscuous mode. Promiscuous mode (which can be set on an interface using ifconfig promis) is good for monitoring traffic across the network and often allow you to monitor the actions of someone who has broken into your network. The tcpdump command will also set a designated interface to promiscuous mode while the program runs; unfortunately, the ifconfig command will not report this while tcpdump is running! Keep in mind that this is one way that a cracker will monitor your network to gain the ever-so-important root password.

> NOTE
Browse to http://www.redhat.com/docs/manuals/linux/RHL-8.0-Manual/security-guide/s1-ids-net.html to read about how to detect unauthorized network intrusions or packet browsing (known as network sniffing).

Don’t forget to use the right tool for the right job. Although a network bridge can be used to connect your network to the Internet, it wouldn’t be a good idea. Bridges almost become obsolete because they will forward any packet that comes their way. That isn’t good when it is connected to the Internet. A router will allow you to filter which packets are relayed.

# Securing DHCP

DHCP so far appears to be fairly secure on UNIX/Linux servers. Be sure that only root can modify the dhcpd.conf file, and you should have no DHCP related security issues.

# Securing NFS

As mentioned previously, even the concept of what NFS does is a security nightmare. If you use your favorite Internet search engine and search for “NFS exploits,” you will be given many, many different listings. If you don’t need NFS to share files across your network or to mount remote directories, be sure it is disabled and not enabled to start at boot using the ntsysf or chconfig commands.

# Making Samba Secure

Samba is well-written. There aren’t too many exploits (security flaws that can be used for malicious purposes). The biggest security issues are the ones created by improper configuration or incorrect file permissions on important files. Like DHCP, you need to protect your configuration (/etc/samba.conf). Other precautions to include making sure that you have the latest, most secure and stable version installed and using software packages from Red Hat. Be careful giving privileges with Samba, restrict anonymous access to your server, and you should be safe.

# Keeping Up-to-Date on Linux Security Issues

A multitude of Web sites relate to security. In one particular host is an excellent mailing list. The list is called Security Focus, and the mailing list is called BugTraq. BugTraq is well-known for its unbiased discussion of security flaws. Be warned: it receives a relatively large amount of traffic (20–100+ messages daily).

Often security holes are discussed on BugTraq before the software makers even released the file. The Security Focus site has other mailing lists and sections on its Web site dedicated to Linux in general and is an excellent resource.

> Related Red Hat and Linux Commands
You’ll use these commands when managing network connectivity in your Red Hat Linux system:
- etereal–GNOME graphical network scanner
- gome-lokkit–Red Hat’s basic graphical firewalling tool for X
- config–Displays and manages Linux networking devices

Reference 443

```
iwconfig—Displays and sets wireless network device parameters
lokkit—Red Hat's basic graphical firewalling tool
netconfig—Red Hat's console-based graphical network interface configuration tool
pump—Automatically configures a network interface
redhat-config-nfs—Red Hat's graphical Network File System configuration tool
redhat-config-network—Red Hat's graphical network and service management client for X
route—Displays and manages Linux kernel routing table
setup—Red Hat's console-based graphical management tool
ssh—The OpenSSH remote-login client and preferred replacement for telnet
```

# Using Patches/Upgrades to Keep Your Network Secure

One of the keys to security is to keep up-to-date with the latest stable versions. Each time a new version of software package comes out, it corrects any security holes. Your network is only as strong as the weakest link. See Chapter 8 for details. Use RPM to update Red Hat. With effort, your system can be secure.

# Reference

The more you take the time to learn, the easier maintaining your network will be. The following Web sites and books are great resources for the topics covered in this chapter.

# General

```
http://www.redhat.com/docs/manuals/linux/RHL-8.0-Manual/custom-guide/ch-network-config.html—Red Hat's guide to network configuration.
```

```
http://www.ietf.org/rfc.html—Go here to search for, or get list of, Request for Comments (RFC).
```

# DHCP

```
http://www.oth.net/dyndns.html—For a list of Dynamic DNS providers, go to this site.
```

```
http://www.isc.org/products/DHCPv3—README.html—The DHCP README is available at this site.
```

#

http://www.ieee.org—The Institute of Electrical and Electronics Engineers (IEEE) Web site.

http://www.mozillaquest.com/Network_02/Wireless_Technology_03_Story_01.html—Wireless networking with Red Hat 7.2

http://crl.cs.uiuc.edu/doc/wireless_redhat.html—Wireless networking using Red Hat at the Computing Research Laboratory (CRL), the information technology support group for the Department of Computer Science at the University of Illinois at Urbana-Champaign

http://www.sorgonet.com/network/wirelessnap/—Building a wireless network using an access point, using Red Hat 8.0

# Security

http://www.redhat.com/docs/manuals/linux/RHL-7.3-Manual/custom-guide/ch-gnomelikkit.html—Red Hat's guide to basic firewall configuration.

http://www.insecure.org/nmap/—This site contains information on nmap.

http://www.securityfocus.com/—The Security Focus Web site.

http://www.psionic.com/abacus/portsentry/—Has information on PortSentry.

http://www.tripwire.com—Has information on TripWire.

# Books

Sams Teach Yourself TCP/IP Network Administration in 21 Days, Sams Publishing, ISBN: 0-672-31250-6

TCP/IP Network Administration, O'Reilly Publishing, ISBN: 1-56592-322-7

Practical Networking, Que Publishing, ISBN: 0-7897-2252-6

Samba Unleashed, Sams Publishing, ISBN: 0-672-31862-8

The DHCP Handbook, Sams Publishing, ISBN: 0-672-32327-3
