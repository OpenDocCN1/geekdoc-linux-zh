
A typical workstation on a LAN (Local Area Network) will have two interfaces. The first is the loopback interface (though of course this is an abstract construct of the TCP/IP implementation, rather than an actual physical interface), and the second is the interface that is on the LAN itself. The common case is for the LAN interface to be on an Ethernet segment, and that is the case this chapter deals with.

## Ethernet Cards and Cables

Ethernet interfaces are designed for most systems as ISA or PCI cards, although laptop computers often have PCMCIA Ethernet cards, and a few systems have Ethernet interfaces built directly onto the motherboard. Ethernet cards are often referred to as NICs, or Network Interface Cards.

There are three types of physical media commonly used for Ethernet networks: 10Base-2, 10Base-T, and 100Base-T. The “10” or “100” part of each of these designations indicates the theoretical maximum data transmission speed in megabits per second (Mbps). (Gigabit Ethernet systems have been developed, but are not yet widely available.) Many Ethernet cards support more than one of these physical media types. So-called “Combo” cards offer both 10Base-2 and 10Base-T, and there are also dual-speed cards (which can do either 10Base-T or 100Base-T).

10Base-2 Ethernet uses coaxial cable with BNC connectors. It requires a backbone, or bus, topology (see Figure 14.1): All nodes on a 10Base-2 Ethernet must connect directly to what is essentially a single length of 50-ohm thin coaxial (coax) cable. This cable must be terminated by resistors at either end, and it is broken by T-connectors. Each node is plugged into one of these T-connectors.

![](img/4886c42c7629f445c7f7f3011ffbf3c3_411_0.png)

10Base-T and 100Base-T Ethernet use unshielded twisted pair (UTP) cables with RJ45 connectors (which are similar to telephone jacks). UTP cables come in various categories; Category 3 is sufficient for 10Base-T, whereas the faster data rates of 100Base-T need the higher quality provided by Category 5 cables. 10Base-T and 100Base-T networks use a different topology, known as a star topology, where each node connects to a central hub (see Figure 14.2). This means that when designing a 10Base-T or 100Base-T network, you must budget for a hub in each Ethernet.

Figure 14.2
10Base-T networks use a star topology.

![](img/4886c42c7629f445c7f7f3011ffbf3c3_412_0.png)

## Ethernet Hubs

Ethernet hubs typically have from 4 to 24 ports for Ethernet connections. Some hubs run at only one speed (10 or 100 Mbps), whereas others are dual-speed. Cheaper dual-speed hubs will force all ports to be the same speed, so adding a 10 Mbps Ethernet interface to a network that is otherwise 100 Mbps will substantially decrease network performance. However, most modern dual-speed hubs will automatically detect the correct connection speed for each port individually; these are called auto-sensing hubs. Some hubs are stackable, which means that one or more ports can be used for connecting a second hub. Obviously, stackable hubs give far more opportunity for expanding a network after its original installation.

## Switches

One of the distinguishing features of Ethernet is known as CSMA/CD, or Carrier Sense Multiple Access with Collision Detection. CSMA/CD is an approach for deciding what to do when more than one device on the Ethernet tries to send a frame of data simultaneously (since only one frame can be active at any given moment). Each device detects this "collision." At this point, the devices must be able to re-send their frames at different times, without communicating between themselves or using any external arbitration. The approach that Ethernet adopts is for each device to wait a random length of time before re-sending the frame.

In normal operation, this is entirely adequate. However, if a network is heavily loaded, performance degrades severely, as the Ethernet devices end up spending more and more of their time waiting for collision situations to be resolved. The network becomes saturated.

Ethernet switches get around this problem. They behave in a similar way to hubs, but where hubs create a single Ethernet out of multiple independent cables, a switch essentially puts each of its ports on a separate Ethernet, and transmits (or switches) frames between each network. You can put a network hub on each port of a switch. Alternatively, you can directly connect a single host; this would be useful for a heavily used server that many other hosts must communicate with.

Switches can also reduce a network's vulnerability to certain security problems. A host or hub on a given port of a switch is on its own Ethernet; this makes it considerably harder for would-be attackers to snoop on data being transmitted using trace tools. Such data could include passwords or other sensitive data, for example. Obviously, the advantages of this approach are limited if several hosts are placed on a switched Ethernet segment using a hub, but switches are nonetheless particularly beneficial for multi-user machines.

### Using Switches

When should you use a switch? In many environments, the increased flexibility of switched Ethernet is unnecessary, and would be wasted. However, if you start seeing many collisions on a network, it is well worth examining the situation carefully. Under Linux, you can use the ifconfig command to check how many collisions have been detected on a network. Listing 14.1 shows some sample output.

### LISTING 14.1 Using ifconfig to Examine Ethernet Collisions

```
$ ifconfig eth0
eth0 Link encap:Ethernet HWaddr 00:E0:98:04:37:59
inet addr:192.168.1.1 Bcast:192.168.1.255 Mask:255.255.255.0
UP BROADCAST RUNNING MULTICAST MTU:1500 Metric:1
RX packets:455299 errors:6 dropped:0 overruns:0 frame:25
TX packets:403376 errors:14 dropped:0 overruns:0 carrier:14
collisions:7004 txqueuelen:100
Interrupt:10 Base address:0x300
```

In this case, there have been 7004 collisions, out of 403,376 packets transmitted (TX), giving a collision rate of slightly under 2%. I know from experience that this rate is considerably higher than normal for this network. In this instance, it's a direct result of running several concurrent flood-pings (that is, sending ICMP Echo Request packets as fast as possible) specifically to acquire some interesting data on Ethernet collisions. In general, collision rates below 5% are nothing to worry about. If collision rates above 5% are seen consistently, and among a broad sampling of hosts on the network, it may well be time to consider splitting the network with a switch.

## Choosing Ethernet Media

Which type of physical Ethernet media should you choose when setting up a new network? Each type has advantages and disadvantages.

### Coax-based or UTP-based Ethernets

Coax-based Ethernets incur lower costs than the alternatives, mainly because there is no requirement to use a hub, but also because 10Base-2 NICs tend to be cheap. (Some would say that you get what you pay for with the very cheapest 10Base-2 cards, though.) Compared to UTP-based Ethernets, they use one fewer piece of cable for a given number of hosts. (Moreover, depending on the physical location of the hub in relation to the hosts, UTP-based networks may need substantially more cable overall.) Coax networks are also very simple to set up.

The biggest problem with 10Base-2 is precisely the requirement for a single backbone connecting all the nodes. If there is a failure at any point in the backbone cable, the entire network goes down. This also makes it comparatively difficult to expand them if requirements change. This makes it hard to recommend a 10Base-2 network for the majority of new installations; however, home users may find that 10Base-2 Ethernet is an ideally cheap and simple mechanism for connecting a few machines together.

### 10Base-T or 100Base-T UTP Ethernets

As for the UTP media types, the principal difference between 10Base-T and 100Base-T is obviously speed. Of course, this difference comes at a price: 100Base-T parts are more expensive than 10Base-T equivalents, especially for high-quality components. However, the price differential is getting smaller, and it may be cheaper in the long run to go for 100Base-T initially, rather than to start with 10Base-T only to discover at some later date that a 100 Mbps network is in fact necessary.

I would normally recommend investing in Category 5 cable even for 10Base-T networks because re-cabling a network is an expensive and time-consuming procedure. Using Category 5 for 10Base-T is unlikely to be prohibitively expensive unless you are connecting a large number of machines together. Once you have Category 5 cables in place, upgrading from 10Base-T to 100Base-T is a simple matter of installing dual-speed hubs; then individual hosts can be upgraded to 100 Mbps Ethernet cards when appropriate. Indeed, in some situations it can make sense to get dual-speed hubs initially, even if to begin with no host on the network has a NIC that can run at 100Mbps.

Now that we've described the workings of Ethernet and how it fits in with TCP/IP, the next stage is to actually get an Ethernet interface working under Red Hat Linux. The next section discusses how this is done.
