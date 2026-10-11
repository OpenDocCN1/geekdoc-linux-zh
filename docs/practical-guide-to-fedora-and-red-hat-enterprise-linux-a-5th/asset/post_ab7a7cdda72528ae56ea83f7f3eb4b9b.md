
The Internet is a loosely administered network of networks (an internetwork) that links computers on diverse LANs around the globe. An internet (small i) is a generic network of networks that may share some parts in common with the public Internet. It is the Internet that makes it possible to send an email message to a colleague thousands of miles away and receive a reply within minutes. A related term, intranet, refers to the networking infrastructure within a company or other institution. Intranets are usually private; access to them from external networks may be limited and carefully controlled, typically using firewalls (page 363).

Over the past decade many network services have emerged and become standardized. On Linux and UNIX systems, special processes called daemons (page 1078) support such services by exchanging specialized messages with other systems over the network. Several software systems have been created to allow computers to share file systems with one another, making it appear as though remote files are stored on local disks. Sharing remote file systems allows users to share information without knowing where the files physically reside, without making unnecessary copies, and without learning a new set of utilities to manipulate them. Because the files appear to be stored locally, you can use standard utilities (such as cat, vim, lpr, mv, or their graphical counterparts) to work with them.

Developers have created new tools and extended existing ones to take advantage of higher network speeds and to work within more crowded networks. The rlogin, rsh, and telnet utilities, which were designed long ago, have largely been supplanted by ssh (secure shell, page 621) in recent years. The ssh utility allows a user to log in or execute commands securely on a remote computer. Users rely on such utilities as scp and tftp to transfer files from one system to another across the network. Communication utilities, including email utilities and chat programs (e.g., talk, Internet Relay Chat [IRC], ICQ, and instant messenger [IM] programs, such as AOL's AIM and gaim) have become so prevalent that many people with very little computer expertise use them on a daily basis to keep in touch with friends, family, and colleagues.

An intranet is a network that connects computing resources at a school, company, or other organization but, unlike the Internet, typically restricts access to internal users. An intranet is very similar to a LAN (local area network) but is based on Internet technology. An intranet can provide database, email, and Web page access to a limited group of people, regardless of their geographic location.

The ability of an intranet to connect dissimilar machines is one of its strengths. Think of all the machines that you can find on the Internet: Macintosh systems, PCs running different versions of Windows, machines running UNIX and Linux, and so on. Each of these machines can communicate via IP (page 365), a common protocol. So it is with an intranet: Dissimilar machines can all talk to one another.

Another key difference between the Internet and an intranet is that the Internet transmits only one protocol suite: IP. In contrast, an intranet can be set up to use a number of protocols, such as IP, IPX, AppleTalk, DECnet, XNS, or other protocols developed by vendors over the years. Although these protocols cannot be transmitted directly over the Internet, you can set up special gateway boxes at remote sites that tunnel or encapsulate these protocols into IP packets and then use the Internet to pass them.

You can use an extranet (also called a partner net) or a virtual private network (VPN) to improve security. These terms describe ways to connect remote sites securely to a local site, typically by using the public Internet as a carrier and employing encryption as a means of protecting data in transit.

Following are some terms you may want to become familiar with before you read the rest of this chapter:

- ASP (page 1069)
- bridge (page 1072)
- extranet (page 1081)
- firewall (page 1082)
- gateway (page 1083)
- hub (page 1086)
- Internet (page 1088)
- Intranet (page 1088)
- ISP (page 1089)
- packet (page 1098)
- router (page 1104)
- sneakernet (page 1107)
- switch (page 1110)
- VPN (page 1114)

## TYPES OF NETWORKS AND HOW THEY WORK

Computers communicate over networks using unique addresses assigned by system software. A computer message, called a *packet*, *frame*, or *datagram*, includes the address of the destination computer and the sender's return address. The three most common types of networks are *broadcast*, *point-to-point*, and *switched*. Once popular token-based networks (such as FDDI and token ring) are rarely seen anymore.

Speed is critical to the proper functioning of the Internet. Newer specifications (cat 6 and cat 7) are being standardized for 1000BaseT (1 gigabit per second, called gigabit Ethernet, or GiG-E) and faster networking. Some of the networks that form the backbone of the Internet run at speeds of almost 10 gigabits per second (OC192) to accommodate the ever-increasing demand for network services. Table 10-1 lists some of the specifications in use today.

**Table 10-1 Network specifications**

| Specification | Speed |
| :------------ | :--------------------------------------------------- |
| DS0 | 64 kilobits per second |
| ISDN | Two DS0 lines plus signaling (16 kilobits per second) or 128 kilobits per second |
| T-1 | 1.544 megabits per second (24 DS0 lines) |
| T-3 | 43.232 megabits per second (28 T-1s) |
| OC3 | 155 megabits per second (100 T-1s) |
| OC12 | 622 megabits per second (4 OC3s) |
| OC48 | 2.5 gigabits per seconds (4 OC12s) |
| OC192 | 9.6 gigabits per second (4 OC48s) |

## BROADCAST NETWORKS

On a *broadcast network*, such as Ethernet, any of the many systems attached to the network cable can send a message at any time; each system examines the address in each message and responds only to messages addressed to it. A problem occurs on a broadcast network when multiple systems send data at the same time, resulting in a collision of the messages on the cable. When messages collide, they can become garbled. The sending system notices the garbled message and resends it after waiting a short but random amount of time. Waiting a random amount of time helps prevent those same systems from resending the data at the same moment and experiencing yet another collision. The extra traffic that results from collisions can strain the network; if the collision rate gets too high, retransmissions may result in more collisions. Ultimately the network may become unusable.

## POINT-TO-POINT NETWORKS

A point-to-point link does not seem like much of a network because only two endpoints are involved. However, most connections to WANs (wide area networks) go through point-to-point links, using wire cable, radio, or satellite links. The advantage of a point-to-point link is its simplicity: Because only two systems are involved, the traffic on the link is limited and well understood. A disadvantage is that each system can typically be equipped for only a small number of such links; it is impractical and costly to establish point-to-point links that connect each computer to all the rest. Point-to-point links often use serial lines and modems. The combination of a modem with a point-to-point link allows an isolated system to connect inexpensively to a larger network.

The most common types of point-to-point links are the ones used to connect to the Internet. When you use DSL1 (digital subscriber line), you are using a point-to-point link to connect to the Internet. Serial lines, such as T-1, T-3, ATM links, and ISDN, are all point-to-point. Although it might seem like a point-to-point link, a cable modem is based on broadcast technology and in that way is similar to Ethernet.

## SWITCHED NETWORKS

A *switch* is a device that establishes a virtual path between source and destination hosts in such a way that each path appears to be a point-to-point link, much like a railroad roundhouse. The switch creates and tears down virtual paths as hosts seek to communicate with each other. Each host thinks it has a direct point-to-point path to the host it is talking to. Contrast this approach with a broadcast network, where each host also sees traffic bound for other hosts. The advantage of a switched network over a pure point-to-point network is that each host requires only one connection: the connection to the switch. Using pure point-to-point connections, each host must have a connection to every other host. Scalability is provided by further linking switches.

> 1. The term DSL incorporates the xDSL suite of technologies, which includes ADSL, XDSL, SDSL, and HDSL.
