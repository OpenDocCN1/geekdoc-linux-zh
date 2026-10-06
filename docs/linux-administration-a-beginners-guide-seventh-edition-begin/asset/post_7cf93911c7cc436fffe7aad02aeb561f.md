
# 362 Linux Administration: A Beginner's Guide

![](img/9f6657924397c33f088db5321b751a83_382_0.png)

Figure 13-3 The relationship between the predefined chains in Netfilter

Administrators can add more chains to the system if they want. A packet matching a rule can then, in turn, invoke another administrator-defined chain of rules. This makes it easy to repeat a list of rules multiple times from different chains. You will see examples of this kind of configuration later in the chapter.

All of the predefined chains are of the mangle table. This means that at any point along the path, it is possible to mark or detail the packet in an arbitrary way. The relationship among other tables and each chain, however, varies by chain. A visual representation of all of the relationships is shown in Figure 13-4.

We'll cover each of these chains in detail to help you understand these relationships.

There are no predefined chains in the nftables Netfilter implementation, but you have the convenience of being able to select from so-called base chains, which are chains that are registered in the iptables Netfilter hooks (PREROUTING, INPUT, FORWARD, OUTPUT, and POSTROUTING).

# CHAPTER 13 Linux Firewall (Netfilter) 363

| NAT Table | Filter Table | Mangle Table |
| --- | --- | --- |
| PREROUTING | FORWARD | PREROUTING |
| POSTROUTING | INPUT | POSTROUTING |
| OUTPUT | OUTPUT | FORWARD |
| | | OUTPUT |

Figure 13-4 The relationship among predefined chains and predefined tables

## PREROUTING

The PREROUTING chain is the first packet hits when entering the system. This chain can invoke rules in one of three tables: NAT, raw, and mangle. From a NAT perspective, this is the ideal point at which to perform a Destination NAT (DNAT), which changes the destination IP address of a packet.

Administrators looking to track connections for the purpose of a firewall should start the tracking here, since it is important to track the original IP addresses along with any NAT address from a DNAT operation.

## FORWARD

The FORWARD chain is invoked only in the case when IP forwarding is enabled and the packet is destined for a system other than the itself. For example, if the Linux system has the IP address 172.16.1.1 and is configured to route packets between the Internet and the 172.16.1.0/24 network, and a packet from 1.1.1.1 is destined to 172.16.1.10, the packet will traverse the FORWARD chain.

The FORWARD chain calls rules in the filter and mangle tables. This means that the administrator can define packet-filtering rules at this point that will apply to any packets to or from the routed network.

## INPUT

The INPUT chain is invoked only when a packet is destined for the host itself. The rules that run against a packet happen before the packet goes up the stack and arrives at the application. For example, if the Linux system has the IP address 172.16.1.12, packet has to be destined to 172.16.1.1 for any of the rules in the INPUT chain to apply. If a rule drops all packets destined to port 80, any application listening for port 80 will never see such packets.

The INPUT chain calls on rules in filter and mangle tables.

## OUTPUT

The OUTPUT chain is invoked when packets are sent from applications running on the host itself. For example, if an administrator tries to use Secure Shell (SSH) on the command-line interface (CLI) to connect to a remote system, the OUTPUT chain will see the first packet of the connection. The packets that return from the remote host will come through PREROUTING and INPUT.

In addition to filter and mangle tables, the OUTPUT chain can call on rules in the NAT table. This allows administrators to configure NAT transformations on outgoing packets that are generated from the host itself. Although this is atypical, the feature enables administrators to PREROUTING-style NAT operations on packets. (Remember: if the packet originates from the host, it never has a chance to go through the PREROUTING chain.)

## POSTROUTING

The POSTROUTING chain can call on the NAT and mangle tables. In this chain, administrators can alter source IP addresses for the purposes of Source NAT (SNAT). This is also another point at which connection tracking can happen for the purpose of building a firewall.

## Installing Netfilter

The good news is that if you have a modern distribution of Linux, you should already have iptables installed, compiled, and working. A quick check is to try running the iptables command, like so:

```
[root@server ~]# iptables -L
```

On an Ubuntu system, you would run this command instead:

```bash
master@ubuntu-server:~$ sudo iptables -L
```

A quick check to see the IPv6 equivalent is by using this command:

```bash
[root@server ~]# iptables -L
```

Note that some distributions do not include the /sbin directory in the default path, and there is a good chance that the iptables program lives there. If you're unsure, try one of the following paths: /sbin/iptables, /usr/sbin/iptables, /usr/local/bin/iptables, or /usr/local/sbin/iptables. The /bin and /sbin directories should already be in path.

# 364 Linux Administration: A Beginner's Guide

# CHAPTER 13 Linux Firewall (Netfilter) 365

If the command gave you a list of chains and tables, you know that Netfilter is installed. In fact, there is a good chance the OS installation enabled some filters. Some distros provide an option to configure or customize a basic firewall at installation time.

With Netfilter present, you don't have much to do besides

The following sections offer some useful information about the options that can be used when setting up a vanilla kernel

## Enabling Netfilter in the Kernel

Most of Netfilter's code actually lives inside the kernel and ships with the standard distribution of Linux. In the fact that Netfilter isn't already enabled in your distribution, you can enable it by turning on the right options during the kernel configuration. If you are not familiar with the process of compiling a kernel, see Chapter 9 for details.

Netfilter has a lot of options. In this section, we cover some of the more pertinent options that you will want to select in case you are building your kernel from scratch.

## Required Kernel Options

For iptables, the following should be supported: Network Packet Filtering, IP Tables, and Connection Tracking.

The first is found under the -> Networking Support -> Networking Options -> Network Packet Filtering Framework (Netfilter) menu when configuring the kernel before compiling. Providing this Netfilter framework functionality in the kernel. Without this option enabled, none of the other listed options will work. Note that this feature cannot be compiled as a kernel module; it is either in or out.

The second, IP Tables, is found under the -> Networking Support -> Networking Options -> Network Packet Filtering Framework (Netfilter) -> IP: IP Configuration -> The purpose of this is to provide the IP Tables interface and management to the Netfilter system. Technically, this module is optional, as it is possible to use the other iptables or ipfwadm or the new nftables; however, unless you have a specific reason to stick to the old interface, you should stick with iptables or nftables. If you are in the process of migrating from your very old iptables/ipfwadm configuration to IP Tables, you will definitely want all of the modules compiled and available to you.

Then comes the Connection tracking option. This can be found under -> Networking Support -> Networking Options -> Network Packet Filtering Framework (Netfilter) -> IP: Netfilter Configuration IPv4 Connection Tracking Support. It offers the ability to add support for intelligent TCP/IP connection tracking and specific support for key protocols as FTP; The IP Tables option, this can be compiled as a module.
