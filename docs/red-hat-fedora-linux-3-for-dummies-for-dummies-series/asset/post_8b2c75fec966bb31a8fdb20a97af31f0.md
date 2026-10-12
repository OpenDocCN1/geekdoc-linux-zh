
## Chapter 15
### Building Your Own Private Network

**In This Chapter**
- Designing and creating your private network
- Building an Internet gateway
- Building a private network firewall

A private network is made up of two or more computers, interconnected so they can communicate with each other; you can also refer to a private network as a *local-area network* (LAN). The computers are generally in close proximity within a room or building. Unlike the Internet, which is designed to allow the world’s computers to communicate with each other, LANs are designed to keep communication local and private. (You can always connect your LAN to the Internet, of course, but we talk about that topic elsewhere in this book.)

Building a private network isn’t as difficult as it may sound. First, you have to decide on a general network layout. Second, you have to physically connect the computers with cables and wireless devices. Third, and last, you have to configure each computer’s network settings. Design, connect, configure — one, two, three — it’s as simple as that.

This chapter shows how to build a simple LAN. If you want to know how to add a Linux computer to an existing network, check out Chapter 7. To find out about adding a firewall to your LAN, check out Chapter 8.

![](img/41feae212f5c6612ff709354891f7b39_210_0.png)

In this chapter, we show you how to wire computers together. You should refer to the Linux network-configuration instructions in Chapter 7 to connect individual computers on your network. The steps in Chapter 7 are also designed to work with any LAN, including the one you’re building here.

In this chapter, we describe how to connect computers to form a LAN. However, you can connect many other devices to a network. You can connect a wide range of devices to a network (whether it's wireless or wired); these include broadband (cable and DSL) Internet modems, routers, switches, hubs, network-capable printers, and even some personal digital assistants (PDAs). In the future, we fully expect to be able to connect nearly every electronic device to a LAN. We discuss only computers here because we're focusing on getting your Fedora Core computer connected. However, remember that you're not limited to networking *only* computers.

### Designing and Building Your Private Network

Private networks take on many shapes and sizes. As you may expect, the design of a LAN for a large- or medium-size organization is different from what you'd use for a small office or home. Individuals and small organizations generally don't require complex networks unless the work is complex enough to need such a tool. For the purposes of this book, we assume that you want and need a simple network - and Linux excels at networking. We describe how to design a basic LAN that is both powerful and reliable. This network can be used for many small- or medium-size businesses and most households.

This chapter shows you how to design a simple, flat network. *Flat* refers to the fact that all the computers connected to the network communicate over a single *subnet* (or *subnet*). Subnets can be combined within a single LAN, but that makes the network more complex to design, build, and maintain.

The network we describe in this section is also designed to use a Fedora Core *Internet gateway* - a computer that acts as a portal, connecting the private network to the Internet. The networked computers in the private network - also referred to as *hosts* or *clients* - are connected via one of two methods:

- **Wired connections:** Hosts are connected to the LAN through a device called an *Ethernet hub* or *Ethernet switch* (or just *hub* or *switch*). Switches are superior to hubs in performance and security, and have become the standard. For your LAN, we suggest that you use an Ethernet switch to connect all the computers (hosts) - including the Internet gateway. Figure 15-1 shows an example of our private network, where the interconnecting fabric is the Ethernet switch. (In recent years, Ethernet switches have become so inexpensive that Ethernet hubs have all but disappeared.) Our example network consists of two computers: Veracruz and Cancun.

- **Wireless connections:** Wireless devices make it possible to build a network without interconnecting cables. Wireless networks can take two forms:
  - **An access point:** Using a device called an access *point*, you can connect wireless hosts to a LAN. This design has the hosts connect to the access point via radio frequency (RF) signals. The access point also connects to a wired network, and the wireless hosts communicate with the wired network through that connection.

    Access points have become the most popular system for creating wireless LANs. You can find access point devices in consumer electronics stores for much less than $100.

  - **Ad-hoc mode:** This is an alternative wireless-connection method that doesn’t require a separate access point, other than a wireless device for each host (*ad hoc* is the Latin equivalent of “whatever works”). Wireless hosts communicate directly with each other by using ad-hoc mode. (You can read more about ad-hoc mode in the “Wiring without wires” section later in this chapter.)

![](img/41feae212f5c6612ff709354891f7b39_212_0.png)

### Where did all the wires go?

The RF (radio-frequency) signals used by wireless networks are the same ones you tune in to on your radio — or communicate with on your cell phone — or use to open your garage door. The only differences between the RF signals coming from an AM radio station and a wireless network device are its frequency and strength.

The *Federal Communications Commission* (FCC) permits anybody to use the 5-gigahertz (GHz) portion of the frequency spectrum — billions of cycles per second — for any purpose as long as the signal strength is low. In effect, radio signals replace the wires in a wireless LAN.

### The ABCs of switches and hubs

Switches are better than hubs because switches are more secure and faster. Here's a quick comparison to illustrate the differences.

Suppose your network consists of three machines — A, B, and C — all connected to a switch. When Machine A wants to communicate with Machine B, the switch transmits the network traffic from A directly to B. Machine C is out of the loop. By making sure that C doesn't know what A and B are saying, the switch keeps network communication private. Hubs, on the other hand, broadcast the network traffic from one machine to all machines connected to the hub. When A sends information to B, the hub broadcasts that information to both B and C.

Switches are faster than hubs because network traffic flows only between the machines that are talking to each other. The computers that aren't talking to each other don't use the switch's bandwidth (the maximum rate at which information can be transmitted). For example, when Machine A is sending information to Machine B, Machine C doesn't slow up the communication speed by sucking up the bandwidth.

### Wiring your network with, yes, wires

This section describes how to build a wired network. You can mix wired and wireless networks, but, for simplicity, we describe how to build a pure wired or wireless network.

Way back in prehistoric times (circa 1996), you had to be technically savvy to wire your own network. Wiring consisted of coaxial cables like those used for cable-TV connections. Coaxial cables are bulky and require you to use special tools to attach the connectors to the cable ends.

Life is easy now. Wiring your network requires that you obtain Cat-5 cables, similar in appearance to telephone cables. Cat-5 cables are manufactured with telephone-like connectors that are a snap (pardon the pun) to use. No muss, no fuss.

![](img/41feae212f5c6612ff709354891f7b39_213_0.png)

You can buy Cat-5 cables at any electronics store. They come in many colors and sizes. Cat-5 cables aren't cheap, but they're not terribly expensive either. They're reliable and much easier to work with than coaxial cables.

You have to use a network switch or hub in conjunction with Cat-5 cables. Switches and hubs are the glue that holds your network together. Both switches and hubs connect individual computers so they can communicate with each other.
