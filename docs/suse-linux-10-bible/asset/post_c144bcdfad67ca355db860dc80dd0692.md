
layer-specific headers and footers. For example, an application layer packet is encapsulated into a transport packet, which is encapsulated into a network packet, which is finally encapsulated into a data link packet, and then sent via the physical layer.

You may notice that we don't have encapsulation of presentation and application layers. This is because these layers do not deal with packets of data; they are holders for standards of data — for example, XML, FTP, HTTP, and DOC.

The way network connection is made makes no difference to the FTP program you use, whether it is over gigabit or wireless networks. This allows the TCP/IP protocol to expand to growing demands. For example, FTP has no idea about gigabit Ethernet because the technology is quite new. FTP, on the other hand, was around before gigabit. A layered network model follows this abstraction to not impact the upper layers, as only the lower layers need to understand gigabit technology. This is why we can bolt on new technologies without having to worry about upper layers.

# The DoD Model

In reality, TCP/IP standard does not adhere 100 percent to the OSI model. As we said, the model is only a reference guide, and protocols do not have to follow it exactly. The TCP/IP model fits more closely to the DoD (Department of Defense) model of a network protocol shown in Figure 6-2. TCP/IP is not abstracted as the OSI model, and many of the components fit into the DoD model. For example, the TCP/IP application usually takes care of the format that the data is sent and also the creation of a TCP/IP session.

Figure 6-2: The DoD Model

| Application |
| :--- |
| Transport |
| Network |
| Link |

> Note: We spent so much time on the OSI model because everyone refers to it as the standard representation of how a network protocol can be implemented. You will see people refer to the OSI model more often than the DoD model.

# 162 Part II ♦ The SUSE System

The DoD model is so named because it was a TCP/IP four-layer protocol originally developed by the United States Department of Defense when defining TCP/IP. The seven layers of the OSI network model have many-to-one mapping to the four layers used in the DoD model.

For additional information about the OSI and DoD networking models and the relationships between the various layers that they define, see sites such as https://www.comptechdoc.org/independent/networking/guide/standards.nml and https://www.novell.com/info/primer5.html.

So you have here a TCP/IP conceptual overview. The information will become clearer as we progress through the chapter.

A wealth of good books about TCP/IP are available, as well as a plethora of Internet resources. This chapter provides an overview of networking theory to make it easier to understand how Linux works and what aspects of networking you may need to configure. This is not a networking book, so we provided only much detail as necessary for basic understanding.

# IP Addresses

Every machine takes part in a TCP/IP network such as the Internet has an IP address. If you dial up and check your email, you are given an IP address to distinguish from other machines so that you communicate with how to find you.

An IP address is something called a dotted decimal number. We will take a private IP address (which we talk about later in the chapter) of 192.168.0.1 as an example.

192.168.0.1 is a dotted decimal number. The dots split the number into separate entities, so the address is 192 168 0 1, separate from each other. It is not 19216801!

This distinction between the numbers is very important and should never be overlooked as it plays an integral role in the way that IP works. IP is the network layer protocol in the TCP/IP suite and provides addressing facilities.

IP has classes of addresses. This splits the address space into manageable chunks and provides a way for users to allocate these coherently. Table 6-2 shows classes and their.

Each section of an IP address expressed as a dotted decimal number is referred to as an octet because each section of an address is actually stored as an 8-bit binary number. There are 8 bits, you have a total of 256 (2^8) possible combinations in each octet. With most digital numbering systems, you have a range of 0–255, giving you the smallest IP address of 0.0.0.0 and the largest of 255.255.255.255. Both of these addresses are reserved for internal IP use, and we will talk about those later in the chapter.

# Chapter 6 ✦ Understanding Your Network 163

| Table 6-2 |
| IP Address Classes |
| Class | IP Range | Description |
| :--- | :--- | :--- |
| A | 1.0.0.0 to 126.0.0.0 | Large organizations, many host addresses |
| B | 128.1.0.0 to 191.254.0.0 | Midsized organizations, many host addresses |
| C | 192.0.1.0 to 223.255.254.0 | Small organizations, small amount of host addresses |
| D | 224.0.0.0 to 239.255.255.255 | Multicast addresses |
| E | 240.0.0.0 to 254.255.255.255 | Reserved for experimental use |

Classes D and E are out of bounds for normal IP addressing, and we will not discuss these further; we list them for reference purposes only.

An IP address is split into a network and a host component:

- **Network component** — Specifies a network of hosts
- **Host component** — Refers to a specific host on that network

To distinguish both, you use a *network mask*. A network mask is core to the routing of packets is calculated. We discuss that in the “Routing” section later in the chapter.

In a class-based IP model, there are defined network masks, as shown in Table 6-3.

| Table 6-3 |
| Address Classes and Network Masks |
| Class | Network Mask |
| :--- | :--- |
| A | 255.0.0.0 |
| B | 255.255.0.0 |
| C | 255.255.255.0 |

If you take the IP address of 192.168.0.1, you can refer to Table 6-2 and see that this is a Class C address. And in looking up the network mask, you see it is 255.255.255.0 for a Class C address.

# 164 Part II + SUSE System

To find a distinction between network and host components, the routing algorithm in the Linux kernel needs to binary AND operation on the network mask and the IP address. We discuss the math needed later in this chapter, but for now we will deal with class-based host/network distinction as this can be done with standard decimal math.

Wherever there is a 255 in the network mask, you effectively highlight the network component of the address. What you are left with is the network component of the IP address minus the host portion. So for a Class C address, the example address used here, with a mask of 255.255.255.0, you can see that 192.168.0 is the network component. You can be, as matter of deduction, that the host component of the address is .1. You write the network component as a zero-padded address, so the network address of 192.168.0.1 is 192.168.0.0.

So up now, you can see that the IP address of 192.168.0.1 has a network address of 192.168.0.0 and a broadcast address of 192.168.0.255.

# Special IP Addresses

Earlier in the chapter, we talked about the IP addresses 0.0.0.0 and 255.255.255.255. These are reserved addresses and are used to signify all and broadcast addresses, respectively.

- The 0.0.0.0 address is a way of saying "all networks" and is commonly seen when we define a default route in Linux.
- The 255.255.255.255 is a catchall address that is called a broadcast address. IP addresses on a network will listen to this address, as well as their own IP address for broadcast traffic.
- The 192.168.0.1 (in the example we are discussing) is called the network address and is again for internal use in TCP/IP. This is the same as the 0.0.0.0, but refers to the specific network as opposed to all networks.

> The term broadcast is used to describe a way of communicating with machines simultaneously on a network. In the case of 192.168.0.1, the broadcast address of 192.168.0.255 is used to broadcast to all machines in the 192.168.0.0 network. The term unicast refers to a one-to-one communication to a specific host. however, if you communicated directly to 192.168.0.1, you would be performing a unicast operation. The term multicast refers to a broadcast to a selected group of hosts, such as all hosts on the 192.168.0.0 network.
