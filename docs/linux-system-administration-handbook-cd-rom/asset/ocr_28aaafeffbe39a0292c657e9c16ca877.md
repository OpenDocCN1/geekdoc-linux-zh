now. If not, recompile the kernel and be sure to add support for your particular Ethernet card. The first Ethernet card is usually designated eth0.

In order to add networking for this Ethernet card, you have to first initialize and set up the IP interface; then you have to set up routing for the interface you just set up, the two are not the same. The IP interface merely gives the IP address to work with. It still needs to know when a packet wants to go out and what interface it should use. Otherwise, you're likely to use the loopback interface, and your packets will get nowhere fast.

The /sbin/ifconfig program will register the Ethernet card with the TCP/IP services. The typical syntax is

```
/sbin/ifconfig eth0 netmask <addr> broadcast <addr> <IP address>
```

The netmask and broadcast addresses are given, by the IP address for that interface. The interface is automatically brought up if you give it a new IP address, so you don't need to explicitly tell the interface to.

Now that you have that, you can get the routing setup up:

```
add default gw <addr>
```

This sets up a route to a gateway (firewall, router, etc). This is set up to be a default route, so any packets Linux cannot determine how to route will be sent to this address for further processing.

The RedHat network configuration is an excellent tool for setting up your network devices. Get your IP address, nameserver information, gateway, and netmask from your network administrator. If you're the network administrator, look further in this chapter for instructions on finding this information. Under the Names section, verify your hostname, domain, and IP address for your nameservers. The Hosts section lists what IP addresses and hostnames you have in /etc/hosts file. This should contain at least your IP address and hostname. If you have other hosts you want to list here, go ahead and add them.

The Interfaces section lists which interfaces are available to you. The lo0 interface is the loopback interface and is used to route TCP/IP packets to itself. Think of it as a virtual Ethernet interface. Changing it will cause prob

> Except the 3C501. If you find one, throw it out. Yuk. A standing offer in the Linux world early on was that the author of the Linux 3Com would replace a 3C501 card with a 3C503 if you sent it to him just so there would be many fewer 3C501 cards left on the planet.