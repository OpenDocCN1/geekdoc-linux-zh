
## Paralle Port Cable (PLIP Cable)

If you intend to use the PLIP protocol between two machines, then this cable will work for you irrespective of what sort of parallel ports you have installed.

| Pin Name | pin | pin |
| :--- | :--- | :--- |
| STROBE | 1* | |
| D0->ERROR | 2 | 15 |
| D1->SLCT | 3 | 13 |
| D2->PAPOUT | 4 | 12 |
| D3->ACK | 5 | 10 |
| D4->BUSY | 6 | 11 |
| D5 | | 7* |
| D6 | | 8* |
| D7 | | 9* |
| ACK->D3 | 10 | 5 |
| BUSY->D4 | 11 | 6 |
| PAPOUT->D2 | 12 | 4 |
| SLCT->D1 | 13 | 3 |
| FEED | | 14* |
| ERROR->D0 | 15 | 2 |
| INIT | 16* | |
| SLCTIN | 17* | |
| GROUND | 25 | 25 |

- Do not connect the pins marked with an asterisk “*,.”
- Extra grounds are 18,19,20,21,22,23, and 24.
- For the cable you are using with a metallic shield, it should be connected to the metallic DB-25 shell at one end only.

*Warning: A miswired PLIP cable can destroy your controller card. Be very careful and double-check every connection to ensure you don’t cause yourself any unnecessary work or heartache.*

While you may be able to run PLIP cables for long distances, you should avoid it if you can. The specifications for the cable allow for a cable length of about 1 meter or so. Please be very careful when running long PLIP cables, as sources of strong electromagnetic fields, such as lightning, power lines, and radio transmitters can interfere with and sometimes even damage your controller. If you really want to connect two of your computers over a large distance, you really should be looking at obtaining a pair of thin-net Ethernet cards and running some coaxial cable.

## 10base2 (Thin Coax) Ethernet Cabling

10base2 is an Ethernet cabling standard that specifies the use of 52 ohm coaxial cable with a diameter of about 5 millimeters. There are a couple of important rules to remember when interconnecting machines with 10base2 cabling. The first is that you must use terminators at both ends of the cabling. A terminator is a 52 ohm resistor that helps to ensure that the signal is absorbed and not reflected when it reaches the end of the cable. Without a terminator at each end of the cabling, you may find that the Ethernet is unreliable or doesn't work at all. Normally you'd use "T-pieces" to interconnect the machines, so that you end up with something that looks like:

![](img/a3584dae761d2e3abed8bf40d7637389_304_0.png)

where the bars at either end represents a terminator, the parallel lines represents a length of coaxial cable with BNC plugs at either end, and the "T" represents a "T piece" or connector. You should keep the length of cable between the "T piece" and the actual Ethernet card in the PC as short as possible. Ideally the "T piece" will be plugged directly into the Ethernet card.

## Twisted Pair Ethernet Cable

If you have only two twisted pair Ethernet cards and you wish to connect them, you do not require a hub. You can cable the two cards directly together. A diagram showing how to do this is included in the Ethernet-HOWTO (see `Ethernet-HOWTO.html`).

## GLOSSARY OF TERMS USED IN THIS DOCUMENT

The following is a list of some of the most important terms used in this document.

- **ARP** This is an acronym for the *Address Resolution Protcol*, and this is how a network machine associates an IP Address with a hardware address.
- **ATM** This is an acronym for Asynchronous Transfer Mode. An ATM network packages data into standard-size blocks which it can convey efficiently from point to point. ATM is a circuit-switched packet network technology.
- **client** This is usually the piece of software at the end of a system where the user is. There are exceptions to this. For example, in the X11 window system it is actually the server with the user, and the client runs on the remote machine. The client is the program or end of a system that is receiving the service provided by the server. In the case of peer-to-peer systems such as SLIP or PPP the client is taken to be the end that initiates the connection, and the remote end being called is taken to be the server.
- **datagram** A datagram is a discrete package of data and headers that contain addresses. It is the basic unit of transmission across an IP network. You might also hear this called a “packet.”
- **DLCI** The DLCI is the Data Link Connection Identifier and is used to identify a unique virtual point-to-point connection via a Frame Relay network. The DLCIs are normally assigned by the Frame Relay network provider.
- **Frame Relay** Frame Relay is a network technology ideally suited to carrying traffic that is of a bursty or sporadic nature. Network costs are reduced by having many Frame Relay customers sharing the same network capacity and relying on them wanting to make use of the network at slightly different times.
- **Hardware address** This is a number that uniquely identifies a host in a physical network at the media access layer. Examples of this are Ethernet Addresses and AX.25 Addresses.
- **ISDN** This is an acronym for Integrated Services Digital Network. ISDN provides a standardized means by which Telecommunications companies may deliver either voice or data information to a customers premises. Technically ISDN is a circuit-switched data network.
- **ISP** This is an acronym of Internet Service Provider. These are organizations or companies that provide people with network connectivity to the Internet.
- **IP address** This is a number that uniquely identifies a TCP/IP host on the network. The address is 4 bytes long and is usually represented in what is called the “dotted decimal notation,” where each byte is represented in decimal from with dots ( "." ) between them.
- **MSS** The Maximum Segment Size (MSS) is the largest quantity of data that can be transmisted at one time. If you want to prevent local fragmentation, MSS would equal mtu-IP header.
- **MTU** The Maximum Transmision Unit (MTU) is a parameter that determines the largest datagram that can be transmited by an IP interface without it needing to be broken down into smaller units. The MTU should be larger than the largest datagram you wish to transmit unfragmented. Note, this only prevents fragmentation locally; some other link in the path may have a smaller MTU and the datagram will be fragmented there. Typical values are 1500 bytes for an Ethernet interface, or 576 bytes for a SLIP interface.
- **route** The route is the path that your datagrams take through the network to reach their destination.
- **server** This is usually the piece of software or end of a system remote from the user. The server provides some service to one or many clients. Examples of servers include ftp, Networked File System, or Domain Name Server. In the case of peer-to-peer systems such as SLIP or PPP, the server is taken to be the end of the link that is called, and the end calling is taken to be the client.
- **window** The window is the largest amount of data that the receiving end can accept at a given point in time.

## LINUX FOR AN ISP?

If you are interested in using Linux for ISP purposes, I recommend you take a look at the Linux ISP homepage (see http://www.anime .net/linuxisp/) for a good list of pointers to information you might need and use.

## ADMINISTRATION

I’d like to thank the following people for their contributions to this document (in no particular order): Terry Dawson, Axel Boldt, Arnt Gulbrandsen, Gary Allpike, Cees de Groot, Alan Cox, Jonathan Naylor, Claes Ensson, Ron Nessim, John Minack, Jean-Pierre Cocatrix, and Erez Strauss.

### Copyright

NET-5-HOWTO, information on how to install and configure networking support for Linux is copyright © 1997 by Terry Dawson, 1998 Alessandro Rubini.

This program is free software. You can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation—either version 2 of the License, or (at your option) any later version.

This program is distributed in the hope that it will be useful, but without any warranty, without even the implied warranty of merchantability or fitness for a particular purpose. See the GNU General Public License for more details.

You should have received a copy of the GNU General Public License along with this program (the GPL is reprinted as “Appendix D” of this book). If not, write to the Free Software Foundation, Inc., 675 Mass Ave., Cambridge, MA 02139, USA.
