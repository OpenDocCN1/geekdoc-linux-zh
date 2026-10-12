
## Summary
- all communication on a TCP/IP network is made up of individual packets
- each packet contains the IP address of the sender and the recipient
- using simple tools you can look at the packets travelling on the wire and see what your system is doing. This often makes a networked system easier to understand and debug than a stand-alone machine.

## What’s next?
In Chapter 2 we’ll build the simplest possible network – two machines connected to a single Ethernet LAN – and we’ll see how packets are sent between them. But before we do that, in Chapter 1 we install **tcpdump** so we have the tools we need for the job.
An important part of our approach is that we cover topics from the bottom up, starting simple and adding extra functions only one at a time. Our test and example networks reflect this. Here’s an outline of where we’re going in Part 1 of the book:
- two PCs on a single wire (Chapter 2)
- two small networks connected by a router (Chapter 3)
- a simple LAN talking to the Internet (Chapter 3)
- networks connected with multiple routers (Chapters 5 and 6)
- more than one network on the same wire (Chapter 6)
- sub-netted networks (Chapter 6). The most complex example is a network broken into sub-nets with multiple routers, talking over the Internet to another LAN elsewhere.

The final chapters in Part 1 deal with the DNS – the domain name system that lets you refer to machines by name rather than using IP numbers.

## Notes and further reading
For a delightful history of how the Internet evolved, see:
□ Peter Salus *Casting the Net: from ARPAnet to Internet and beyond* (1995, Addison-Wesley)
(Peter Salus also wrote *A Quarter Century of UNIX* (1994, Addison-Wesley). It’s not relevant to what we’re doing here but it’s well worth a read.)
For a huge amount of historical material, including some fascinating maps of the early Internet – e.g. the Internet in 1969, containing just four machines – see:
□ [http://www.archive.org/arpnet/](http://www.archive.org/arpnet/)
Comer *Internetworking with TCP/IP Volume 2* (2000, Prentice Hall), Chapters 1 and 2 also gives some history of the Internet and the bodies involved in developing it.

## Appendices
Appendix 1: layers, the protocol stack, and network reference models

Appendix 2: RFCs and Internet standards

## 1 The tcpdump packet sniffer – your eyes and ears on the network
- 1.1 How **tcpdump** works
- 1.2 How to run **tcpdump**
- 1.3 How to select just the packets you’re interested in
- 1.4 Common problems with **tcpdump**
- Summary

## Introduction
You’ve already seen how you can use **tcpdump** in a simple way to get information about how your network is operating. This chapter describes **tcpdump** in more detail, tells you how you can display only the particular packets you are interested in, and how to tailor its display format to your particular needs.

### 1.1 How tcpdump works
**tcpdump** is a *packet sniffer* – it lets you watch the packets on your network in real-time and prints details from them in the format you specify. Because of the way Ethernet works you are able to look at other computers' traffic as well as your own. **tcpdump** is your fundamental network tool for diagnosing problems or just for understanding how your network operates. It looks at *all* the packets on the network but you can tell it to display only a particular set of packets that you're interested in.

Ethernet is a *bus* network. When one machine sends a packet to another over an Ethernet the packet is visible over the whole length of the wire (Figure 1.1).

![](img/a2132b646d336d5f9a21102d6320e537_45_0.png)

**Figure 1.1 Ethernet packet visible everywhere on the wire**

It is the Ethernet card (network interface card, or “NIC”) in each machine that decides what to do with the packet by looking at the packet’s destination address:
- if the packet is destined for this machine, the Ethernet card passes the packet up to the operating system, which passes the packet up to the appropriate application (shown at A in Figure 1.2).

![](img/a2132b646d336d5f9a21102d6320e537_45_1.png)

**Figure 1.2 Passing the packet from source to destination**
- with the Ethernet card in normal mode, if the packet wasn’t addressed to this machine, the Ethernet card “discards the packet silently”, i.e. it ignores it and doesn’t generate any error message (B in Figure 1.2)
- however, **tcpdump** puts the Ethernet card into a special mode called *promiscuous mode*. In this mode the card passes the packet up to the operating system, no matter what the destination address of the packet is (C in Figure 1.3). Then the operating system passes it to **tcpdump**.

Promiscuous mode is a hardware setting on the Ethernet card, so your card must support it if you’re going to use **tcpdump**. (Just about every Ethernet card you get now does support it. We haven’t come across one that doesn’t.)

![](img/a2132b646d336d5f9a21102d6320e537_46_0.png)

Figure 1.3 Promiscuous mode – tcpdump sees all traffic on the wire

By setting promiscuous mode on the Ethernet card, **tcpdump** gets to examine all the packets on the network. Then, for each packet, **tcpdump** prints the source and destination addresses, and a summary of its contents.

### Types of Ethernet – coaxial cabling v. UTP hubs and switches
Figures 1.1, 1.2, and 1.3 show the Ethernet as a single cable connected to all machines via their NICs. This is exactly how old-style Thick Ethernet and Thin-net (thin Ethernet) works: you run a long coaxial cable throughout your building, and machines are connected to it using special coaxial T-piece connectors (Thin-net) or connection boxes called transceivers (Thick Ethernet). However, nowadays almost everybody uses UTP (unshielded twisted pair) cabling. With UTP you have central wiring hubs: each machine is connected to the hub with its own UTP cable, and hubs are chained together with more UTP cables.

As far as **tcpdump** is concerned, there’s no difference between a network connected up using UTP hubs and the older coaxial cable network. In both, the packets are visible over the whole length of the network and therefore **tcpdump** can see everything.

However, UTP *switches* or *switched hubs* behave differently. When two machines on the same switch communicate, they are given a dedicated channel; all their traffic goes through this channel, and no other machine can see it. In configurations like this, **tcpdump** can see only traffic to/from its own machine (Figure 1.4), which is generally not what you need. There are two solutions to this: either use a hub instead of (or in conjunction with) your switch (Module 2.6) or use a “managed switch” that lets you configure the type of behavior you need for **tcpdump**. (Appendix 3 gives more information on switches and hubs in general and explains what managed switches are.)

![](img/a2132b646d336d5f9a21102d6320e537_46_1.png)

on a switch **tcpdump** can't see other machines’ traffic

connection via Ethernet switch

Figure 1.4 On a switch, only source and destination see the traffic

### 1.2 How to run tcpdump
#### Where to get tcpdump
See the Notes on page 24 for how to obtain and install **tcpdump**, and also the Windows version, which is called **windump**.

#### Running tcpdump
This module and the next give a summary of how to use **tcpdump**. Appendix 4 contains a summary of **tcpdump**’s options, and the full manpage is in Appendix 5.
- 1. you must be a privileged user to run **tcpdump** (because it looks at other people’s network traffic). On Linux you must be user **root** (or the program must be setuid roots). On Windows NT you must be **administrator** (although not all **tcpdump** versions enforce this)
- 2. start the program from the command line (Command Window in Windows); it announces the name of the network interface it’s listening on, followed by details of the packets (Figure 1.5). We’ll explain in a moment why you use the “**-n**” option, but be warned: if you omit it, **tcpdump** may appear to hang for a minute or two.
```shell
tcpdump -n
```
- 3. to terminate **tcpdump** type ctrl-C (or whatever the interrupt or kill character is on your system). **tcpdump** prints its usage statistics and exits.

![](img/a2132b646d336d5f9a21102d6320e537_47_0.png)

The format of the output varies with the type of packet being displayed, but a typical line starts with the time of day, the “dotted decimal” four-part source IP address and destination IP address separated by a “>” symbol, and then the details for that packet. For most types of traffic, the source and destination IP addresses contain a fifth number at the end (e.g. **4141** in the source address on the first line), which is the “port number.” As we’ll explain in Chapter 10, different types of TCP/IP traffic are sent to different “ports” on a host. For example,
