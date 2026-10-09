
Installing a syslog server (see Chapter 21) and having your switches log to it can mitigate this risk. While logging won't prevent switch failure, it will simplify listening to a dying switch when it tries to complain.

### Ethernet Speed

Ethernet originally supported only a couple of megabits per second but has expanded to handle tens-of-gigabits speeds. Most Ethernet cards are *gigabit* speed, meaning they can handle a gigabit per second, but you'll find a few 10Gbs or 100Gbs cards in high-speed applications. If a card is labeled *gigabit*, it doesn't mean it can actually push that much traffic—I've seen gigabit cards choke on a tenth that much bandwidth. Card quality is important when you want to push bandwidth, and the quality of the entire computer is important when pushing serious bandwidth.

Let the switch and the card negotiate their settings on their own through *autonegotiation*. While some old hands might remember disabling autonegotiation on older Ethernet cards, gigabit and faster Ethernet requires autonegotiation to function.

### MAC Addresses

Every Ethernet card has a unique identifier, a Media Access Control (MAC) address. This 48-bit number is sometimes called an *Ethernet address* or *physical address*. When a system transmits data to another host on the Ethernet, it first broadcasts an Ethernet request asking, “Which MAC address is responsible for this IP address?” If a host responds with its MAC address, further data for that IP is transmitted to that MAC address.

IPv4 uses the Address Resolution Protocol (ARP) to map IP addresses to hosts. Use `arp(8)` to view your FreeBSD system's knowledge of the ARP table. The most common usage is the `arp -a` command, which shows all of the MAC addresses and hostnames that your computer knows of.

```bash
# arp -a
gw.blackhelicopters.org (198.51.100.1) at 00:00:93:34:4e:78 on igb0 [ethernet]
sipura.blackhelicopters.org (198.51.100.5) at 00:00:93:c2:0f:0c on igb0 [ethernet]
```

This full listing of ARP information is known as the ARP table, or MAC table. (The terms MAC and ARP are frequently used interchangeably, so don't worry about it too much.) Here we see that the host gw.blackhelicopters.org has an IP address of 198.51.100.1 and a MAC address of 00:00:93:34:4e:78, and that you can reach these hosts on the local system's interface, igb0.

If a MAC address shows up as incomplete, the host cannot be contacted on the local Ethernet. In this case, check your physical layer (the wire), the remote system, and the configuration of both systems.

IPv6 uses Neighbor Discovery Protocol (NDP) to map IPv6 addresses to MAC addresses. It's a separate protocol from ARP to encompass router discovery. Use ndp(8) to view the host's ARP table and corresponding IPv6 addresses. The output deliberately resembles that of arp(1).

```text
# ndp -a
Neighbor                        Linklayer Address    Netif    Expire  S Flags
fe80::fc25:90ff:fee8:1270%vtnet0  fe::25:90:e8:12:70    vtnet0   4s     R R
www.michaelwluucas.com           00:25:90:e8:12:70      vtnet0   perm   R
fe80::225:90ff:fee8:1270%vtnet0   00:25:90:e8:12:70      vtnet0   perm   R
```

The output deliberately resembles that of arp(8) but is slightly more tabular. The Neighbor column shows either the IPv6 address, the hostname, or the link-local address of each neighbor. The Linklayer Address column shows the MAC address of the neighbor. The Netif column displays the network interface this host is attached to, while the Expire column shows when the cached entry will expire. The s (state) column shows further information about the entry. A state of R means the host is reachable, while an I (incomplete) means the host is unreachable. The only flags entry you're likely to see is R, indicating this host is advertising itself as a router. For more states and flags, see ndp(8).

Why two separate commands? Both arp(8) and ndp(8) exist to map IP addresses to MAC addresses. Some hosts might be available only via one protocol or the other. IPv6-only hosts will not show up in your ARP table, and IPv4-only hosts will not appear in the NDP table.

For both arp(8) and ndp(8), the -n flag turns off hostname lookups. This is highly useful when you debug network issues and can't get DNS resolution.

Now that you know how the network works, configuring an internet connection is pretty straightforward.

# Chapter 8
# CONFIGURING NETWORKING

![](img/f11aeb3fa2ed406688e13ccb43ed9dab_256_0.png)

Now that you know enough networking to be dangerous, you can configure a network connection. While FreeBSD supports many different protocols, we’ll focus on the nearly ubiquitous Ethernet connection, generally delivered over CAT5 or CAT6 cables.¹

We’ll start with the essentials for getting a host on the network and able to access other internet hosts. Raw TCP/IP connectivity isn’t enough, however; you also need the ability to resolve host names to IP addresses, so we’ll cover that next. Then we’ll talk about measuring network activity, performance, VLANs, and aggregating links.

Before you can do any of that, though, you need some information.

## Network Prerequisites

If your network offers Dynamic Host Configuration Protocol (DHCP), you can connect to the network as a client without knowing anything about the network. A static IP address makes much more sense on a server, however. While the installer will configure the network for you, eventually every server needs changes. Both IPv4 and IPv6 require the following information:

- An IP address
- The netmask for that IP address and protocol
- The IP address of the default gateway

Armed with this information, attach your system to the network with ifconfig(8) and route(8) and then make the configuration permanent in /etc/rc.conf.

### Configuring Changes with ifconfig(8)

The ifconfig(8) program displays the interfaces on your computer and lets you configure them. Start by listing the existing interfaces on your system by running ifconfig(8) without any arguments:

```
# ifconfig
em0: flags=8843<UP,BROADCAST,RUNNING,SIMPLEX,MULTICAST> metric 0 mtu 1500
    options=85259b<RXCSUM,TXCSUM,VLAN_MTU,VLAN_HWTAGGING,VLAN_HWCSUM,TSO4,LR0,WOL_MAGIC,VLAN_HWTILTER,VLAN_HWTSO>
    inet 203.0.113.43 netmask 0xffffff0 broadcast 198.51.100.47
    inet6 fe80::225:90ff:fe8:1270%m0 prefixlen 64 scopeid 0x1
    inet6 2001:db8::bad:c0de:cafe prefixlen 64
    ether 00:25:90:db:d5:94
    media: Ethernet autoselect (1000baseT <full-duplex>)
    status: active
rlo0: flags=8802<BROADCAST,SIMPLEX,MULTICAST> mtu 1500
    options=8<VLAN_MTU>
    ether 00:20:ed:72:3b:5f
    media: Ethernet autoselect (10baseT/UTP)
    status: No carrier
lo0: flags=8049<UP,LOOPBACK,RUNNING,MULTICAST> metric 0 mtu 16384
    options=600003<RXCSUM,TXCSUM,RXCSUM_IPV6,TXCSUM_IPV6>
    inet6 ::1 prefixlen 128
    inet6 fe80::1%lo0 prefixlen 64 scopeid 0x2
    inet 127.0.0.1 netmask 0xff000000
    nd6 options=21<PERFORMNUD,AUTO_LINKLOCAL>
```

Our first network interface is em0, or the first network card that uses the em(4) driver. The em(4) man page reveals that this is an Intel PRO/1000 card. You'll then see basic information about this card, including that it is in the UP state, meaning it's either working or trying to work. It's assigned the IPv4 address 203.0.113.43 and the netmask 0xffffff0 (or 255.255.255.240, per Table 7-2). This card has two IPv6 addresses, the link-local address (beginning with fe80) and the global IPv6 address ⑤. You’ll also see the MAC address ⑥ and the connection speed ⑦. Finally, the status entry shows that this card is active ⑧: a cable is plugged in and we have a link light.

The second card, rl0, has almost none of this information associated with it. One key fact is the no carrier signal ⑨: it’s not plugged in and there is no link light. This card is not in use.

Finally we have the interface lo0 ⑩, the loopback. This interface has the IPv4 address 127.0.0.1 and IPv6 address ::1 on every machine. This loopback address is used when the machine talks to itself. This is a standard software interface, which does not have any associated physical hardware. Do not attempt to delete the loopback interface, and do not change its IP address—things will break in an amusing way if you do so. FreeBSD supports other software interfaces, such as disc(4), tap(4), gif(4), and many more.

### Adding an IP to an Interface

The install process will configure any network cards you have working at install time. If you didn’t configure the network for all of your cards during the setup process, or if you add or remove network cards after finishing the install, you can assign an IP address to your network card with ifconfig(8). You need the card’s assigned IP address and netmask.

```
# ifconfig interface-name inet IP-address netmask
```

For example, if your network card is em0, your IP address is 203.0.113.250, and your netmask is 255.255.255.0, you would type:

```
# ifconfig em0 inet 203.0.113.250 255.255.255.0
```

Specify the netmask in dotted-quad notation as above or in hex format (0xffffff00). Perhaps simplest of all is to use slash notation, like this:

```
# ifconfig em0 inet 203.0.113.250/24
```
