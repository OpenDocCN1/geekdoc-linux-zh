
## Required Kernel Components

The Linux kernel that ships with most Linux distributions is precompiled with everything you need to utilize IP masquerading. All that needs to be done to implement it is to load some kernel modules and set up some simple firewall rules.

For those who want to compile their own kernels, following is the list of items that need to be compiled into the kernel for NAT and IP masquerading to work (the names are listed as they are seen during a `make config` or `make menuconfig` procedure):

- Code maturity options:
  - Prompt for development or incomplete code or drivers
- Loadable module support:
  - Enable loadable module support
  - Kernel module loader (optional)
- Networking options:
  - Network packet filtering
  - Network packet filtering debugging (optional)
  - TCP/IP networking
  - IP Netfilter configuration:
    - Connection tracking
    - FTP protocol support
    - IP tables support
    - Full NAT
    - MASQUERADE target support
  - The IPv6 protocol (optional)
  - IPv6 Netfilter configuration
    - IP6 tables support
    - Packet filtering

In addition to these modules (some of which are optional), others can be chosen, depending on your needs. Consult Chapter 36 for additional information about modules that you might want to select for additional packet filtering and logging.

> **Caution**
>
> Some kernel configuration options should never be selected. Particularly, don't select Fast Switching, because it bypasses the packet filter rules. Also never select any protocols that netfilter can't handle, such as IPX, Appletalk, and so forth, or IPv6 if you don't select IP6 filter modules.

## SETUP

IP masquerading is accomplished through the packet-filtering firewall capabilities of modern Linux kernels. When an outgoing network packet hits the firewall machine (the server with IP masquerading set up on it), the firewall rewrites elements of each packet to make them look as if they are emanating from the firewall and not the machine behind the firewall. The return packets are modified to go back to the machine that sent the original outgoing packets. To both ends of the transaction, nothing odd seems to be going on at all.

Some services, such as FTP, require special handling, thus the module to support FTP connection tracking. This is because an active FTP connection uses two separate ports, 21 for control, and 20 for data transfer. This complicates things because the connection to port 20 comes not from the client, but from the server in response to the client. This is not required for passive downloads, which use only the control channel (port 21), the default for Netscape and Internet Explorer. But for other FTP clients, you'll need the FTP connection tracking and the NAT FTP modules loaded (unless you started them in passive mode or like ncftp will automatically switch).

Chapter 19, "Kernel Modules," details how to automatically load modules every time your system boots. If you want to use any (or all) of these modules, refer to that chapter for details on how to load them. The following modules should probably be loaded for a Masquerading server:

- `ip_tables`
- `iptable_nat`
- `ip_conntrack`
- `ip_conntrack_ftp`
- `ip_nat_ftp`
- `ipt_MASQUERADE`

For the most part, the iptables commands you'll issue will tell you which modules should be loaded. (See Chapter 36 for a program which will load all available iptables modules.)

The first thing that you need to do to start masquerading is to create a network with bogus IP addresses. The blocks of IP addresses allocated for private networks as listed in RFC 1597 are shown in Table 35.1.

**Table 35.1. Private Network Address Blocks**

| Class | Address Start | Address End | Mask |
|---|---|---|---|
| A | 10.0.0.0 | 10.255.255.255 | 8 |
| B | 172.16.0.0 | 172.31.255.255 | 16 |
| C | 192.168.0.0 | 192.168.255.255 | 24 |

Unless literally hundreds of computers are to be set up on the network, odds are that one of the Class C blocks is what you'll want to use.

The iptables utility is used to set up the forwarding rules for IP masquerading. The following syntax is used:

```
iptables -t nat -A POSTROUTING -j MASQUERADE -o ppp+ -s private_IP_network/mask -d 0/0
```

In this command, replace private_IP_network with the beginning IP address from Table 35.1 for the class of address you are using, and replace mask with the corresponding mask value. The -o specifies the outgoing interface. The ppp+ means the ppp interface (usually ppp0, the + meaning any active ppp interface). You can substitute eth0, tr0, ippp0, and so on, for ppp+.

For example, if a Class C address block is being used by the computers on the network, the following command is used:

```
iptables -t nat -A POSTROUTING -j MASQUERADE -o ppp+ -s 192.168.0.0/24 -d 0/0
```

In most cases, this is all that needs to be done to set up the firewall rules. Combined with the modules listed earlier, most of the common Internet services are covered by this configuration.

> **Note**
>
> You must make sure your system has IP forwarding enabled. You can do this in Caldera by using COAS (coastool) and selecting Network Administration, TCP/IP Network Options, IP Forwarding, Enabled from the main menu. Or you can change the /etc/sysconfig/network file to read IPFORWARDING=yes. Debian has an ip_forward variable in /etc/network/options you can change. And in Red Hat, you can change the net.ipv4.ip_forward variable in /etc/sysctl.conf from 0 to 1. As a final option, you can include a line like the following in your /etc/rc.d/rc.local (or equivalent) file:
>
> ```sh
> echo 1 > /proc/sys/net/ipv4/ip_forward
> ```
>
> All accomplish the same thing: changing the /proc/sys/net/ipv4/ip_forward kernel variable to 1 to permit passing packets from one interface (IP address) to another.

It is important to note that IP masquerading is, for the most part, a one-way street. You can go from the machines on your network out to the Internet, but without special packet-forwarding rules, you cannot get into the systems behind the masquerading server from the Internet. This means that a machine that has a bogus IP address and is sitting behind a masquerading server cannot serve Web pages out on the Internet, nor can it accept direct FTP connections from the outside, nor telnet, nor ssh/secure transactions, and so on without some special rules. If you have routable addresses behind the firewall/NAT system, you might want to deny forwarding so that only masqueraded addresses are passed with this rule:

```
iptables -P FORWARD DENY
```

> **Note**
>
> If you want to see the rules you've input, it is not intuitively obvious from the usage message or the man page, but remember that you're working with the NAT table. To see the rules from this chapter, you'll need to use the following:
>
> ```sh
> iptables -t nat -L -n
> ```

## SNAT

Masquerading, as we have previously discussed it, is just a special case of source NAT. If you happen to have a public, static IP, you don't want masquerading—you want source network address translation (SNAT). You'll want to use SNAT instead of masquerading where possible for some of the features SNAT brings, including mapping your hosts to multiple IP addresses.

Looking at a few examples and their explanations might help your understanding:

```
iptables -t nat -A POSTROUTING -o eth0 -j SNAT --to 209.127.112.150
```

The preceding line says you want to use the NAT table (-t nat) and append to the POSTROUTING chain. You're going to use the outgoing interface eth0 (this is the Internet-connected interface) and change the source address of the originating system (-j SNAT) to the public IP 209.127.112.150 (--to 209.127.112.150).

This simple example performs exactly the same function as the previous MASQUERADE example, but you need to know the IP (so this won't work on a dynamically assigned address).

Now let's assume for argument's sake that you have six usable IPs, and you want to use four of them on your NAT firewall. The following example will show how to use iptables to make it look like you're coming from any one of four addresses:

```
iptables -t nat -A POSTROUTING -o eth0 -j SNAT --to 209.127.112.150-209.127.112.153
```

The difference between this example and the one earlier in this section is in the --to address. Each connection going out will pick up the next IP number. When the last IP number is reached, iptables will wrap the addresses back to the first IP number.

Let's also assume you have some rogue users on your network who have been connecting to non-standard ports on the outside, presumably for some unauthorized activities (like IRC chat). You want to permit them to use only standard ports. You can do this by specifying a range as well:

```
iptables -t nat -A POSTROUTING -p tcp -o eth0 -j SNAT --to 209.127.112.150:0-1023
```

Now, outgoing TCP connections destined for ports 0–1023 will pass through. You'll want to add a UDP rule because DNS uses UDP port 53 for most queries, but large queries and zone transfers will use TCP port 53. One set of upper ports includes 6000–6255 (but most commonly 6000–6010). So if you want to run X through your firewall, you'll need to add a rule that includes these ports. This text will not debate the sagacity of running X through a firewall, just remind administrators they should consider the inherent security risks.

## DNAT

Complementing source NAT is destination NAT (DNAT). This particular translation works in reverse. Under the older ipchains, you had to use ipmasqadm to achieve what was called port forwarding, and is now called DNAT. DNAT enables you to use the public IP addresses for functions such as FTP server, Web server, mail server, and so forth, without putting those systems at as high a risk. Behind a firewall, they are better protected.
