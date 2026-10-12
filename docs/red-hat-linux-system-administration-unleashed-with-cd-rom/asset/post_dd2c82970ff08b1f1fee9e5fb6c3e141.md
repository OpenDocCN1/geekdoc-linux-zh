
could probably improve on this to get even more information. This is a trivial example and having an alternative to the ls command may not be of much use. However, applying the same principle to other commands, such as ps, can be very useful because it is common for system crackers to replace commands that can show their presence on the system. In the case of the ls command, application of this principle means that even if the cracker has subverted the ls command to hide directories and files from me, he would also have had to subvert my shell, awk, and the wc command as well.

Additional sources of information on security tools is included in Chapter 27, which contains a number of references to Web sites and FTP archives that are devoted to security.

The problem with dealing with any intrusion is that you don’t know what has been affected on the system. Binaries may have been trojaned and their dates touched back to their original values. The tripwire binary could be trojaned, as could shutdown. I know this is rough, but I recommend that when an intrusion is discovered, you pull the plug. This freezes the intrusion in progress and prevents more damage. If you can afford it, have an extra disk on hand and dd a copy of the compromised disk to it to keep a clean version for you to experiment on. Now you can boot off a floppy, like Trinux as described in the next section, and inspect the system. Of course, this may be overkill, but you need to determine a security policy and stick to it. You should (if you’re administering for a business) talk to lawyers and/or law enforcement officials when you’re defining your security policy to make sure you don’t do anything that could be considered evidence tampering!

## Trinux as a Security Tool

A very useful tool that you can use in the event of a system break in is the Trinux Linux distribution. This is a floppy-based Linux distribution that uses RAM disks to provide an extensive collection of security and recovery tools in a minimal amount of space. This section takes a look at how Trinux can assist you in determining the extent of an intrusion and in preventing repeat performances.

One of the most compelling reasons for using Trinux is that you can boot the affected system using the Trinux floppies and use the included tools to diagnose the system. This allows you to investigate without affecting the state of the system and bypassing all of the tools on the system, which may have been altered by the intruder. Also, because Trinux boots from floppies, you can easily carry it with you to remote locations. The networking support in Trinux also means that you can access the network if you find a problem that cannot be dealt with by the tools included.

To get a copy of Trinux, visit its Web site at http://www.trinux.org and download the latest images and packages. These packages include tools such as packet sniffers, network monitors, network mapping and vulnerability scanners, firewall and proxies, and other utilities. With these tools, you can perform the analysis required after a security breach to determine the source of the vulnerability, while at the same time correct damage done to the system that you know was compromised.

## Remedying Security Issues with Trinux

A suggested strategy that you can employ involving Trinux is to attack the problem in three phases. First, use Trinux on a laptop or other portable system attached to your network to probe the system that suffered the intrusion. You can determine how the system cracker got in and identify other possible methods of entry to the damaged system. For this phase, you can use the scanning tools on the Trinux disks, such as nmap. The nmap program is a network mapper/port scanner that identifies open ports on a system, as well as the system type and lots of other information that can be used to determine possible vulnerabilities. You can then determine if any of the services that are reported as open have security announcements regarding them and suggested fixes to remove the vulnerability, or you can simply turn off the service in question.

The second phase is to use the Trinux disks to boot the attacked system and use the utilities on the disks to look for changes to the system. This ensures that the tools you are using to check for discrepancies are not the ones that may have been compromised by the system cracker. This is very important so that you do not miss anything due to corrupted or subverted system utilities such as ls or ps.

The final phase is to use the Trinux tools to scan your entire network to look for vulnerabilities on hosts other than the one that was attacked. This is best done from somewhere outside of your network so that your firewall is tested as well. One of the security tools available with Trinux that serves this purpose is SAINT, which not only scans the host that was attacked, but can also run in an exploratory mode to determine other hosts that may have vulnerabilities based on trust relations with the compromised hosts.

The following sections discuss some of the tools that are available with the Trinux distribution. The list of tools is broken down by category and each tool is briefly described.

## Packet Sniffers

Packet sniffers are tools that listen on a network interface and gather information about the packets that are passing through that interface. Three such utilities that come with Trinux are
- Tcpdump
- Ipgrab
- Ngrep

### Tcpdump

Tcpdump is the standard packet sniffer that comes with most flavors of UNIX and Linux. The description from the manual page states that tcpdump prints out the headers of packets that match the boolean expression supplied on the command line. This package is available by anonymous ftp from ftp://ftp.ee.lbl.gov/tcpdump.tar.Z.

### Ipgrab

Ipgrab is another packet sniffer based on the Berkeley packet capture library. It prints out complete header information for packets at the Data Link, Network, and Transport layers. Written by Mike Borella, it is available on the Web at http://www.xnet.com/~cathmike/MSB/Software/.

### Ngrep

The functional tool in this category is ngrep. This utility is an attempt to provide GNU grep-like functionality across the Network layer. It allows you to specify a regular expression and filter expressions as understood by the Berkeley packet capture library and print out information on matching packets. This tool is available at http://www.packetfactory.net/ngrep/.

## Network Monitors

Network monitors are used to display statistical information regarding traffic passing over a network. These types of tools can be used to determine the amount and type of traffic, including byte counts, number and types of packets, error counts, and other similar information. Here are two of tools distributed with Trinux:
- IPTraf
- Ntop

### IPTraf

IPTraf is a network statistics package that displays general and detailed interface statistics showing packet counts, sizes, and a wealth of other information regarding the traffic on your network in full-screen mode. It includes a filtering mechanism that allows you to single out specific types of traffic by protocol. IPTraf is available at http://cebu.mozcom.com/riker/iptraf/.

### Ntop

Ntop is another monitoring package that displays information in a manner similar to the top utility and, like top, shows network usage statistics in a variety of sort orders. Ntop can be used in interactive mode or Web mode. It is available from http://www.serra.unipi.it/~ntop/.

## Network Mapping/Vulnerability Scanning

Network mapping and vulnerability scanning tools use a variety of methods to determine the layout of a network. They probe the various well-known services and use the responses to identify open ports. Or, through the use of techniques such as TCP fingerprinting, they determine the type of system it is reaching. Trinux includes several of these tools, such as
- Nmap
- Exscan
- SAINT
- QueSO
- Hping
- Firewall
- Cgichk

### Nmap

One of the most useful tools in the Trinux tool set is nmap. This utility explores networks, identifying the types of hosts attached and possible vulnerabilities for each of them. Nmap is an excellent security auditing tool that should become part of any serious security administrator's toolset. The nmap utility is available at http://www.insecure.org/nmap/index.html.

### Exscan

Another scanning utility is exscan. This utility, like nmap, is able to identify the operating system of the system being scanned through the use of TCP fingerprinting, a capability it gets from integrating queso. In addition to this, it captures banner information from various services on remote systems like SMTP and FTP and queries servers for information such as HTTP version and finger information. Get it at http://exscan.netpedia.net/exscan.html.

### SAINT

SAINT is the Security Administrator's Integrated Network Tool. It probes systems looking for vulnerabilities, such as unprotected ports, and is also capable of examining vulnerabilities based on trust relationships between systems. SAINT is similar in many ways to SATAN. The SAINT home page is at http://www.wdsi.com/.
