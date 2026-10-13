
## Make Sure the Firewall Is Running

Once desired changes are saved to the /etc/sysconfig/iptables configuration file, it's important to make sure the Firewall is in operation, with the new rules. Since the reload option is not available in the /etc/init.d/iptables script, you'll need to do so with the following command:

> exam Watch
> *It's critical to understand how to secure a Red Hat Enterprise Linux system against unauthorized access.*

```
# service iptables restart
```

As discussed in Chapter 11, this is functionally equivalent to the /etc/init.d/iptables restart command.

## IP Masquerading

Red Hat Enterprise Linux supports a variation of NAT called IP masquerading. IP masquerading supports Internet access from multiple computers with a single public IP address. IP masquerading maps multiple internal IP addresses to that single valid external IP address. That helps as all public IPv4 address have now been allocated. While IPv4 addresses are often still available from these third parties, at a price. That cost is one more reason for IP Masquerading. On the other hand, systems on IPv6 networks may not need masquerading, as it's relatively easy for many requesting users to get their own subnet of public IPv6 addresses. Nevertheless, even on IPv6 networks, masquerading can help keep that system secure.

> exam Watch
> *The RHCE objectives specify the use of iptables to configure network address translation.*

IP Masquerading is a fairly straightforward process. It's implemented on a gateway or router, where the system has two or more network cards. One network card is connected to an outside network such as the Internet, and the second (and additional) network card is connected to a LAN. The card connected to the outside network may connect through an external device such as a cable "modem" or Digital Subscriber Line (DSL) adapter.

The following assumptions are made for the configuration:

- The public IP address is assigned to the network card that is directly connected to the outside network.
- Network cards on the LAN get IP addresses associated with a single private network.
- One network card on the gateway or router system gets an IP address on that same private network.
- The same iptables command and configuration files used to set up a firewall are also used to set up IP masquerading.
- IP forwarding is enabled on the router or gateway system, as discussed later in this chapter.
- Each system on the LAN is configured with the private IP address of the router or gateway system as the default gateway address.

When a computer on a LAN wants a web page on the Internet, it sends packets to the firewall. The firewall replaces the source IP address on each packet with the firewall's public IP address. It then assigns a new port number to the packet. The firewall caches the original source IP address and port number.

When a packet comes in from the Internet to the firewall, it should include a port number. If the firewall can match an associated rule with the port number assigned to a specific outgoing packet, the process is reversed. The firewall replaces the destination IP address and port number with the internal computer's private IP address and then forwards the packet back to the original client on the LAN.

In practice, the following command uses iptables to enable masquerading. The noted command assumes that eth1 represents the network card that is directly connected to the Internet, with a private IP network of 192.168.0.0/24:

```
# iptables -t nat -A POSTROUTING -s 192.168.0.0/24 -o eth1 -j MASQUERADE
```

In most cases, the private IP network address is not required, as most LANs protected by a masquerade are configured on a single private IP network.

If you're using separate private networks, such as for the KVM-based virtual machines configured in Chapters 1 and 2, masquerading of those networks enables communication between those systems. In that configuration, masquerading rules would be applied to the firewall of the physical host system. On my system, I have the following masquerading rules:

```
# iptables -t nat -A POSTROUTING -o wlan0 -j MASQUERADE
# iptables -t nat -A POSTROUTING -o virbr0 -j MASQUERADE
# iptables -t nat -A POSTROUTING -o virbr1 -j MASQUERADE
```

These rules work hand in hand with the IP forwarding rules discussed next. Just be aware, masquerading substitutes the IP address of the router for that of the originating system. So if you set up masquerading on the physical host system for two VMs, communication from one VM appears to be coming from the IP address of the physical host system.

## IP Forwarding

IP forwarding is more commonly referred to as routing. Routing is critical to the operation of the Internet or any IP network. Routers connect and facilitate communication between multiple networks. When you set up a computer to find a site on an outside network, it needs a gateway address. This corresponds to the IP address of a router on the LAN.

A router looks at the destination IP address of each packet. If the IP address is on one of its LANs, it routes the packet directly to the proper computer. Otherwise, it sends the packet to another gateway closer to its final destination. To use a Red Hat Enterprise Linux system as a router, you should enable IP forwarding in the /etc/sysctl.conf configuration file by changing

```
net.ipv4.ip_forward = 0
```

to

```
net.ipv4.ip_forward = 1
```

These settings take effect on the next reboot. Until then, IPv4 forwarding can be enabled with the following command:

```
echo 1 > /proc/sys/net/ipv4/ip_forward
```

But that is not enough. You'll also need to enable routing through the firewall for communications to other networks. For example, with the KVM-based VM systems on two virtual networks, they include two virtual network devices in the output to the ifconfig command on the physical host: virbr0 and virbr1. On the system that I'm using to write this book, it also includes the local wireless network device, wlan0. For a physical host with a regular wired Ethernet card, you may need to substitute eth0 for wlan0.

```
# iptables -A FORWARD -o wlan0 -j ACCEPT
# iptables -A FORWARD -o virbr0 -j ACCEPT
# iptables -A FORWARD -o virbr1 -j ACCEPT
```

If you actually need to configure a connection to external networks such as the Internet, a change is also required to the /etc/resolv.conf file on the VMs. Normally, it sets the default DNS server to the IP address of the virbr0 and virbr1 networks on the physical host system. You may need to change that DNS server IP address to that used for other systems on the local network. However, that should not be necessary, as Internet access is not available during the Red Hat exams.

## The Red Hat Firewall Configuration Tool

The basic functionality of the Red Hat Firewall Configuration tool was discussed in Chapter 4, with respect to RHCSA objectives. The Firewall Configuration tool can do more. Start it with the system-config-firewall command or by clicking System | Administration | Firewall. This is a tool with a number of capabilities, as shown in Figure 10-3. In general, you can immediately implement any changes made with the Apply button. But for that reason, you may want to back up the current version of the /etc/sysconfig/iptables file before doing anything with the Firewall Configuration tool.

FIGURE 10-3

The Firewall Configuration tool

![](img/9139201cfcaf4292284a0eed074928e5_576_0.png)

Similar functionality is available from the console version of the tool. You can open it with the `system-config-firewall-tui` command. Select Customize for access to the same options shown in Figure 10-3. The following sections address those options not previously discussed in Chapter 4.

## Trusted Interfaces

In the Firewall Configuration tool, click Trusted Interfaces to reveal the window shown in Figure 10-4. Routers and gateways have two or more network cards. Administrators who trust the systems on the internal network may choose to disable the firewall on that interface. However, it should not be necessary. Threats can come from within as well as from outside a network.

The options shown in Figure 10-4 would apply to all interfaces of each type, as listed in Table 10-1. They all end with a *, which is effectively like a wildcard. For example, eth+ is associated with device eth0, eth1, and so on.

In most cases, the gateway or router system will have two Ethernet devices. Assume those devices are eth0 and eth1, where eth0 is connected to an external network. If the local network is to be trusted, then you might set up device eth1 as the trusted device.

Sometimes wireless devices appear as other names. In some configurations, wireless hardware appear as Ethernet devices such as eth0 or eth1. In other cases, I've seen wireless devices appear as wlan0 or even ath0. So it's important to know the device files associated with each network device on a system.

Click Add to open the Interface window shown in Figure 10-5. Then enter the device name of the interface, in this case, eth1.

**TABLE 10-1**
Network Interface Types

| Device | Description |
|---|---|
| eth+ | Ethernet devices |
| ippp+ | Integrated Services Digital Network (ISDN) devices for Point to Point Protocol (PPP) communication |
| isdn+ | Regular ISDN devices |
| ppp+ | PPP devices, normally associated with telephone modems |
| tun+ | Tunneling devices, often associated with virtual private networks |
| wlan+ | Wireless LAN devices |
