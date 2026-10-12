
Both types of firewalls have advantages and disadvantages, and many sites implement both. A proxy-based firewall is regarded as being more secure than a packet-filtering firewall, because it does not have complete knowledge of the protocol used by the application. Another advantage of proxies is that sometimes they may be used to reduce bandwidth usage. For example, an organization may implement a proxy on its firewall that stores the Web pages requested by users. If another user requests the same page again, the proxy can grab it from its local storage and send the page to the user without having to connect to the origin server again. If you multiply this by tens or hundreds of users, you can appreciate the bandwidth savings.

On the other hand, an application-level firewall must be built for each protocol. Thus, there are HTTP proxies, FTP proxies, Telnet proxies, SMTP proxies, and so on. This brings up the problem of *unsupported applications*—applications whose protocols don't have a proxy yet. There are *generic proxies* available, but applications must be modified and recompiled to use them. Since they work on single packets, packet filters are transparent to applications.

A packet-filtering firewall can use additional authentication measures, aside from using just the IP addresses. And a packet-filtering firewall may also do what is known as *network-address translation* or *masquerading*. This means that the firewall converts the source addresses on outgoing packets so the other host thinks it's connecting to the firewall itself, and to the destination addresses on incoming packets so they go to the host that requested the connection initially. This has several advantages. For example, a whole network may connect to the Internet using a single IP address. Also, because internal addresses aren't visible to the outside, hosts on the internal network are more secure against attacks from the outside. The downside to this is that any hosts that provide services to the outside must be outside the firewall; otherwise, the firewall must be specifically configured to pass some packets straight to a particular host.

## Linux Firewalling Concepts

The Linux kernel itself contains support for packet filtering and masquerading. This support is provided by the package called IP chains. Installing and configuring IP chains is highly recommended for reasons of security. There is always the danger of some unscrupulous individual breaking into your computer from the Internet or even from within your corporate network. If you take the time to install and configure IP chains properly, you can minimize the danger of this happening. It is widely argued that there is no such thing as a totally secure computer system or network. This may or may not be true. There are merits to each side of the case. Security experts will tell you, however, that the more protection you provide for your system, the more you reduce the chances of your system falling prey to crackers. Providing firewall protection for your system will significantly reduce the likelihood of your system being violated. It's like installing an alarm system on your car. This will not keep your car from being stolen by an individual who is a professional car thief and who has decided he is going to steal your car. What it will do is make the other unprotected cars in the parking lot much more attractive to the thief because they are unprotected and thus much easier to steal. There are also several packages available for proxy-based firewalls, such as the Squid HTTP/FTP proxy cache and the SOCKS proxy.

To determine whether your kernel supports IP chains, look for the file `/proc/net/ip_fwchains`. If the file exists, your current kernel has support for IP chains. If the file doesn’t exist, you need to enable the kernel firewall. To do this, you must configure the kernel and enable Network Firewalls and IP: Firewalling. You might also want to enable IP: Always Defragment, IP: Masquerading, and ICMP: Masquerading if you’re doing masquerading. After that, recompile and install the kernel and reboot.

Starting with version 2.2 of the Linux kernel, the packet filter is based on the concept of chains, which are configured using the `/usr/sbin/ipchains` utility. If your system doesn’t contain this utility, you have to install the `ipchains-1.3.9-1.9-rpm` from the CD-ROMs.

The `ipchains` tool inserts and deletes rules from the kernel’s packet filtering section. Every rule in the kernel’s packet filter belongs to a group of rules known as *chains*. Initially, the kernel contains three default chains:

- The *input chain*, which is applied to arriving packets, before passing them to the rest of the kernel or to applications.
- The *output chain*, which is applied to packets just before they leave the host.
- The *forwarding chain*, which is applied to packets that have passed the input chain but whose target host is a different host—for example, when the host is being used as a firewall or router.

When a packet enters a chain, it is tested to determine if it matches each of the rules on the chain. If it does, it is passed to the target of that rule. If it reaches the end of a chain, it is passed to the chain’s default target.

A *target* specifies what to do with a packet that matches a particular rule or, in the case of the default targets, what reaches the end of a chain. There are six system targets; they are presented in Table 20.6.

### TABLE 20.6 ipchains System Targets

| Name | Function |
|:-----------|:----------------------------------------|
| ACCEPT | Lets the package through. |
| DENY | Drops the package silently. |
| REJECT | Drops the package, notifying the sender. |
| MASQ | Valid only in the forward chain or chains called from it. Masquerades the package. |
| REDIRECT | Valid only in the input chain or chains called from it. Sends the package to a port on the firewall host itself, regardless of its real destination. May be followed by a port specification to redirect the package to a different port regardless of its destination port. |
| RETURN | Transfers immediately to the end of the current chain; the package will be handled according to the chain's default target. |

A target may also be another chain, including a user-defined chain. You may create your own chains at any time, and attach them to any of the predefined chains. The default target of a user-defined chain is always the rule following the one in which the chain is called, so a user-defined chain can be used as a sort of subroutine; you may reuse its rules in several chains. This is useful to reduce the total number of rules and to better document what is happening, since you may name chains after what they do. For example, if a firewall has different rules for two departments (call them the *bosses* and the *masses*), you might define different chains called *bosses* and *masses*, and then simply apply each chain depending on where the packet is coming from.

## Building a Firewall with ipchains

Consider the network shown in Figure 20.10. There is an internal network using private addresses connected to the public Internet. You want to allow all hosts in the internal network to access the Internet, while providing protection from external hackers. No one needs to access the internal hosts from the outside (thus, this kind of firewall is known as a *one-way firewall*).

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_724_0.png)

Listing 20.2 shows a shell script that sets up a basic one-way packet-filtering and masquerading firewall using ipchains.

### **LISTING 20.2 A Basic Firewall Using ipchains**

```bash
#!/bin/sh -x
# To enable logging if necessary
#LOG=-l

# Constants
ANYWHERE=0.0.0.0/0
EXT_IF=eth0
INT_IF=eth1

# Networks
INTERNAL_NET=10.0.1.0/24
EXTERNAL_ADDR=205.142.24.1/32

# Disable packet forwarding while we set up the firewall
echo 0 > /proc/sys/net/ipv4/ip_forward

# Flush all rules
/sbin/ipchains -F input
/sbin/ipchains -F output
/sbin/ipchains -F forward

# Deny all packets by default - this is a mostly-closed firewall
/sbin/ipchains -P input DENY
/sbin/ipchains -P output DENY
/sbin/ipchains -P forward DENY

# Accept anything to/from localhost
/sbin/ipchains -A input -j ACCEPT -p all -s localhost -d localhost -i lo $LOG
/sbin/ipchains -A output -j ACCEPT -p all -s localhost -d localhost -i lo $LOG

# Spoofing protection - deny anything coming from the outside with an internal address
/sbin/ipchains -A input -j RETURN -p all -s $INTERNAL_NET -d $ANYWHERE -i $EXT_IF $LOG

# Accept TCP packets belonging to already-established connections
/sbin/ipchains -A input -j ACCEPT -p tcp -s $ANYWHERE -d $ME -i $EXT_IF -y $LOG

# Accept and masquerade all packets from the inside going anywhere
/sbin/ipchains -A input -j ACCEPT -p all -s $INTERNAL_NET -d $ANYWHERE -i $INT_IF $LOG
```
