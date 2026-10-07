
the hierarchy is variable. One domain might have many levels (such as a.very.deep.domain.structure.in.the.uk), whereas another can be quite shallow (such as oneroomco.com, which could conceivably point directly to a single computer).

Unfortunately, although hostnames of this form are reasonably easy for people to understand, computers work better with numbers. Therefore, although the Internet includes provisions for using hostnames, at its core it relies upon a different addressing scheme: IP addresses. IP addresses are 32-bit numbers that are generally expressed as four decimal numbers separated by dots (.), as in 192.168.204.98. IP addresses are broken into two components: a network address and a machine address. This division simplifies the job of routers, which are devices that send traffic between networks, because it means the router can be programmed in terms of networks rather than individual computers. A network mask (netmask for short) marks the network address portion of an IP address with binary 1’s. For instance, 255.255.255.0 places a binary 1 in each bit of the first three bytes of an address, indicating that those first three bytes are the network address, and that the final byte is the machine address. An IP or network address can be combined with a network mask using a shorthand form in which the number of leading binary 1’s in the netmask follows the IP address, as in 192.168.204.0/24. This is the same as the 192.168.204.0 network with a netmask of 255.255.255.0 (twenty-four 1’s, expressed in binary).

> **Note** In a hostname, the most significant portion (the machine name) is in the *leftmost* position of the address. In an IP address, the most significant portion (the machine address) is in the *rightmost* position of the address.

Traditionally, the available range of IP addresses is broken up into networks of various *classes*, as indicated in Table 12.1. As indicated by the classes’ netmasks, these classes differ in size—each Class A network can contain over 16 million computers; Class B networks can host 65,534 computers, and Class C networks can each have only 254 computers. More recently, however, networks have been merged or split up in nontraditional ways in order to make more efficient use of the dwindling supply of IP addresses. Each of the three major classes of IP addresses supports a range of *private* IP addresses (shown in Table 12.1), which routers do not route. These IP addresses can be used internally for private networks without acquiring “official” IP addresses. There are also Class D and E networks, which have special meaning and are reserved for future use.

### Table 12.1: IP Address Classes and Private Address Ranges

| Class Name | Range | Netmask | Private Addresses |
| :--- | :--- | :--- | :--- |
| Class A | 1.0.0.0–127.255.255.255 | 255.0.0.0 | 10.0.0.0–10.255.255.255 |
| Class B | 128.0.0.0–191.255.255.255 | 255.255.0.0 | 172.16.0.0–172.31.255.255 |
| Class C | 192.0.0.0–223.255.255.255 | 255.255.255.0 | 192.168.0.0–192.168.255.255 |

> **Note** The Internet is fast running out of IP addresses. Although a 32-bit address provides a theoretical limit of about 4 billion addresses, the actual limits are somewhat lower, and the number of Internet-connected computers is growing at a staggering rate. For this and other reasons, work is underway on IPv6, a new means of addressing for TCP/IP networks. IPv6 uses a 128-bit address, which permits roughly $3.4 \times 10^{38}$ addresses—that’s $2.2 \times 10^{18}$ addresses per square millimeter of land surface on the Earth, which ought to last us a while.

As a practical matter, it’s necessary to link IP addresses to hostnames and vice versa. This task is accomplished through the Domain Name System (DNS), which uses a highly distributed system of DNS servers. Each DNS server is responsible for its own domain or subdomain. These servers are arranged in a hierarchical manner mirroring the domain name structure. At the top of this hierarchy are the *root* servers, which know the addresses of the servers that handle the TLDs. Each TLD server knows the addresses of servers that handle each of its domains, and so on. Eventually, a server in this hierarchy is *authoritative* for a domain, meaning that it can say with authority whether a given hostname exists, and if it does, what its IP address is. A similar hierarchy allows *reverse* DNS lookups, so that a name can be found, given an IP address.

Typically, an organization’s DNS server performs two tasks:

- It fields name queries from computers inside its domain. It queries an appropriate root server and follows the chain of referrals from that server to locate an authoritative server for the requested domain. It then passes the result of this query (typically an IP address or a code saying that the name is invalid) back to the requesting client.
- It accepts queries from outside sources regarding the names and IP addresses of systems within its domain.

When you configure a Linux system for networking, chances are you need only know the IP addresses of from one to three DNS servers. You can then point your Linux system at those DNS servers to let them do the dirty work of traversing the tree of servers to resolve domain names into IP addresses. Linux can function as a DNS server, but configuring Linux in this way is well beyond the scope of this book. For that information, consult a book such as Craig Hunt’s *Linux DNS Server Administration* (Sybex, 2000).

A final address type is the network card’s *hardware address*. The card uses this to tell when packets are addressed to it. Part of the job of the network stack is to find a hardware address matched to any given IP address. The stack does this by broadcasting a query to all the computers on the local network. (For more distant systems, the computer need only send the packet to a local router, which can then forward the data appropriately.) In most cases, you need not concern yourself with the hardware address, although one exception is noted later in this chapter.

## Ports

Once a packet has been routed to a destination system, the target computer needs to know what to do with it. This information is conveyed, in part, through the use of multiple *ports*. Each TCP/IP packet is addressed to one of 65,536 ports, which you can think of as being similar to extensions on a business telephone system. By convention, specific server packages listen for traffic on specific ports. For instance, Web servers listen on port 80 and mail servers listen on port 25. The file */etc/services* lists the port assignments used by common servers. As a user, you don’t normally need to be concerned with port use, because client programs know which ports to call. As a system administrator, you must occasionally deal with port assignments. For instance, you may need to add an entry to */etc/services* if an appropriate entry isn’t present.

> **Note** TCP/IP ports are distinct from hardware ports, which are used to link devices like printers and modems to the computer. An Ethernet card usually has one Ethernet port, but that one Ethernet port supports thousands of TCP/IP ports.

Client programs also use ports to call *out* of a system. Linux assigns outgoing ports to programs on an as-needed basis, so you don’t need to be concerned with this detail. When a server replies to a client, it does so using the port that the client used, so Linux knows to which program it should deliver the return packet. Both client and server programs keep track of the IP addresses with which they’re exchanging data, so they can keep packets from different sessions separate.

## TCP/IP Configuration

With the theory of TCP/IP out of the way, it’s time to move on to practical Linux TCP/IP configuration. Most distributions, including Red Hat 7.3, allow you to configure TCP/IP at system installation; but this isn’t always practical, because you may need to install hardware or locate new drivers before you can proceed. Even if you use installation–time configuration options or a separate GUI interface, it’s helpful to understand the underlying text–mode tools. This chapter therefore emphasizes text–based TCP/IP configuration tools and utilities.

### Configuring Network Hardware

The first step in TCP/IP configuration is to set up the hardware. A working network includes a wide variety of network hardware, such as hubs or switches, routers, servers, and so on. The possibilities are so broad, in fact, that it’s impossible to cover them all here. Therefore, this chapter focuses upon configuring a single Linux system in a network. In this context, hardware configuration consists of locating and installing an appropriate network interface card (NIC) and ensuring that your system contains appropriate drivers for that card.

> **Note** Many isolated Linux systems use the *Point-to-Point Protocol* (*PPP*) to link the system to the Internet via a telephone modem. Chapter 11 describes PPP; this chapter is more concerned with networking via dedicated networking hardware.

Linux supports a wide variety of networking hardware. The most common type of network today is Ethernet, which comes in several varieties, including 10Base2 (also known as *thin coax*), 10Base5 (a.k.a. *thick coax*), 10BaseT, 100BaseT, 1000BaseT, and fiber–optic. The varieties whose names end in *T* are the most common in 2002, and use *unshielded twisted–pair* (*UTP*) wiring, which resembles telephone wires but with wider heads. Older varieties operate at speeds of up to 10Mbps, but 100BaseT supports 100Mbps speeds, and both 1000BaseT and fiber–optic support 1000Mbps (1Gbps) speeds. The Linux kernel supports most modern Ethernet adapters. To discover what devices your Linux distribution supports, check the kernel configuration options under Network Device Support → Ethernet (10 or 100Mbit) for 10Mbps and 100Mbps varieties, or Network Device Support → Ethernet (1000Mbit) for 1Gbps varieties. You can also check with a device’s manufacturer to see which Linux drivers to use. Some manufacturers provide Linux drivers for their boards, but these are usually just the drivers from the Linux kernel.

Some networks don’t use Ethernet, but instead use other types of networking hardware, such as Token Ring. Although Linux’s support for these more exotic types of hardware isn’t as complete as for Ethernet, you can usually find drivers for at least some NICs for most network types. As with Ethernet, you should consult the kernel’s configuration options and boards’ manufacturers to discover what’s supported.

If you compile a driver directly into your kernel, it will automatically load and detect your network card. If your driver is compiled as a module (which is typical of freshly installed Linux systems), *however*, you may need to add an entry or two to the */etc/modules.conf* file (called */etc/conf.modules* on some older distributions). Specifically, you may need to set up an alias between *eth0* and the name of your NIC’s driver. If you have multiple NICs, you may need to add multiple lines to make these associations, as in:

```bash
alias eth0 tulip
alias eth1 via-rhine
```
