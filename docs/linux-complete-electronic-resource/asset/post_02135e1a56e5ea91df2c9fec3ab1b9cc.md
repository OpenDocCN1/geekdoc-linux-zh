
Registering the care-of address with a home agent. The home agent sends datagrams destined for the mobile node through a tunnel to the care-of address. After arriving at the end of the tunnel, each datagram is then delivered to the mobile node.

Point-to-Point Tunneling Protocol (PPTP) is a networking technology that allows the use of the Internet as a secure virtual private network (VPN). PPTP is integrated with the Remote Access Services (RAS) server which is built into the Windows NT server. With PPTP, users can dial into a local ISP, or connect directly to the Internet, and access their network as if they were at their desks. PPTP is a closed protocol and its security has recently been compromised. It is highly recommended to use other Linux-based alternatives, since they rely on open standards that have been carefully examined and tested.

A client implementation of the PPTP for Linux is available at `http://www.pdos.lcs.mit.edu/~cananian/Projects/PPTP/`.

Mobile IPS can be found at `http://www-uk.hpl.hp.com/people/jt/mip.html` and `http://anchor.cs.binghamton.edu/~mobielp/`.

Virtual Private Network-related documents can be found at `http://Metalab.unc.edu/mdw/HOWTO/mini/VPN.html` and `http://sites.inka.de/sites/bigred/develop/cipe.html`.

## NETWORK MANAGEMENT

This section describes network management applications and SNMP.

### Network Management Applications

There is an impressive number of tools focused on network management and remote administration. Some interesting remote administration projects are linucxconf—which can be found at `http://solucor.solucorp.qc.ca/linucxconf/` and webmin—which can be found at `http://webmin.com/webmin/`.

Other tools include network traffic analysis tools, network security tools, monitoring tools, configuration tools, etc. An archive of many of these tools may be found at Sunsite at `http://www.Metalab.unc.edu/pub/Linux/system/network/`.

## SNMP

The Simple Network Management Protocol is a protocol for Internet network management services. It allows for remote monitoring and configuration of routers, bridges, network cards, switches, etc. There are a large number of libraries, clients, daemons, and SNMP-based monitoring programs available for Linux. A good page dealing with SNMP and Linux software may be found at http://linas.org/linux/NMS.html.

## ENTERPRISE LINUX NETWORKING

In certain situations it is necessary for the networking infrastructure to have proper mechanisms to guarantee network availability near 100 percent of the time. Some related techniques are described in the following sections. Most of the following material can be found at Linas' excellent Web site at http://linas.org/linux/index.html and in the Linux High-Availability HOWTO at http://MetaLab.unc.edu/pub/Linux/ALPHA/linux-ha/High-Availability-HOWTO.html.

### High Availability

Redundancy is used to prevent the overall IT system from having single points of failure. A server with only one network card or a single SCSI disk has two single points of failure. The objective is to mask unplanned outages from users to let users continue to work quickly. High availability software is a set of scripts and tools that automatically monitor and detect failures, taking the appropriate steps to restore normal operation and to notify system administrators.

### RAID

RAID, short for Redundant Array of Inexpensive Disks, is a method whereby information is spread across several disks using techniques such as disk striping (RAID Level 0) and disk mirroring (RAID level 1) to achieve redundancy, lower latency, and/or higher bandwidth for reading and/or writing and recoverability from hard-disk crashes. Over six different types of RAID configurations have been defined. There are three types of RAID isolation options available to Linux users: software RAID, outboard DASD boxes, and RAID disk controllers.

**Software RAID**
Pure software RAID implements the various RAID levels in the kernel disk (block device) code.

**Outboard DASD Solutions**
DASD (Direct Access Storage Device) are separate boxes that come with their own power supply, provide a cabinet/chassis for holding the hard drives, and appear to Linux as just another SCSI device. In many ways, these offer the most robust RAID solution.

**RAID Disk Controllers**
Disk Controllers are adapter cards that plug into the ISA/EISA/PCI bus. Just like regular disk controller cards, a cable attaches them to the disk drives. Unlike regular disk controllers, the RAID controllers will implement RAID on the card itself, performing all necessary operations to provide various RAID levels.

Related HOWTOs can be found at:
- `http://MetaLab.unc.edu/mdw/HOWTO/mini/DPT-Hardware-RAID.html`
- `http://MetaLab.unc.edu/mdw/HOWTO/Root-RAID-HOWTO.html`
- `http://MetaLab.unc.edu/mdw/HOWTO/mini/Software-RAID.html`

RAID at Linas.org:
- `http://linas.org/linux/raid.html`

### Redundant Networking

**IP Address Takeover (IPAT)**
When a network adapter card fails, its IP address should be taken by a working network card in the same node or in another node.

**MAC Address Takeover**
When an IP takeover occurs, it should be made sure that all the nodes in the network update their ARP caches (the mapping between IP and MAC addresses).

See the High-Availability HOWTO for more details at `http://MetaLab.unc.edu/pub/Linux/ALPHA/linux-ha/High-Availability-HOWTO.html`.

## Sources of Information

You can get further information at:
- Linux: `http://www.linux.org`
- Linux Documentation Project at `http://MetaLab.unc.edu/mdw/linux.html` (check out the *Linux Network Administrator Guide*)
- Freshmeat: The latest releases of Linux Software at `http://www.freshmeat.net`
- Linux links at `http://www.linuxlinks.com/Networking/`

## Acknowledgements and Disclaimer

This document is based on the work of many other people who have made it possible for Linux to be what it is now: one of the best network operating systems. All credit is theirs. A lot of effort has been put into this document to make it simple but accurate and complete and not excessively long. Nevertheless, no liability will be assumed by the author under any circumstance. Use the information contained here at your own risk. Please feel free to e-mail me with suggestions, corrections, or general comments about the document so I can improve it. Other topics that will probably be included in futures revisions of this document may include radius, Web/ftp mirroring tools such as wget, traffic analyzers, CORBA, and many others that may be suggested and suitable. You can reach me at `ridruejo@es1.us.es`.

Finally I would like to thank FinnBjorn Av Teilgun `<efat@kampsax.dtu.dk>` for his careful “beta-testing” of this HOWTO.

![](img/a3584dae761d2e3abed8bf40d7637389_211_0.png)

## Chapter 8

### LINUX NETWORKING

The Linux Operating System boasts kernel-based networking support written almost entirely from scratch. The performance of the TCP/IP implementation in recent kernels makes it a worthy alternative to even the best of its peers. This document aims to describe how to install and configure the Linux networking software and associated tools.

This chapter is a good read for everyone. Even though most Linux distributions today provide point-and-click tools for the configuration of common network types like Ethernet and PPP, there will always be a time when something unusual comes up. In these odd situations, even the most basic background in how it’s really working under the hood will be useful. That’s what this chapter provides: a description of how all the little user programs and all the kernel code work together to provide your Linux system with its powerful networking capabilities.

Linux Networking is reprinted from the Linux NET-3 HOWTO version 1.4 of August 1998 by Terry Dawson and Alessandro Rubini.

## INTRODUCTION

The original NET-FAQ was written by Matt Welsh and Terry Dawson to answer frequently asked questions about networking for Linux at a time before the Linux Documentation Project had formally started. It covered the very early development versions of the Linux Networking Kernel. The NET-2-HOWTO superceded the NET-FAQ and was one of the original LDP HOWTO documents. It covered what was called version 2 and later version 3 of the Linux kernel networking software. This document in turn supercedes it and relates only to version 3 of the Linux Networking Kernel.

Previous versions of this document became quite large because of the enormous amount of material that fell within its scope. To help reduce this problem a number of HOWTO’s dealing with specific networking topics have been produced. This document will provide pointers to them where relevant and cover those areas not yet covered by other documents.

In April 1998 Terry left as NET-3 maintainer, due to his high load. Alessandro Rubini is the new maintainer and would like to keep the document as good as before, although he’s new to this kind of stuff.

## Feedback

I always appreciate feedback and especially value contributions.

Please direct any feedback or contributions to me by e-mail `<rubini@linux.it>`.

## How to Use This HOWTO Document

This document is organized top-down. The first sections include informative material and can be skipped if you are not interested; what follows is a generic discussion of networking issues, and you must ensure you understand this before proceeding to more specific parts. The rest, “technology-specific” information, is grouped in three main sections: Ethernet and IP-related information, technologies pertaining to widespread PC hardware, and seldom-used technologies.
