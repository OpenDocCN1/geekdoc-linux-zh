
## Table 17-2 netstat Options

| netstat Option | Description |
| :--- | :--- |
| -a | Lists all listening and nonlistening sockets. |
| -i | Displays statistics for your network interfaces. |
| -I | Lists listening sockets. |
| -s | Displays summary information for each protocol. |
| -r | Displays your routing table. |

In addition to the nmap utility, you can also use the netstat utility to scan for open ports. The netstat utility is another powerful tool in your virtual toolbox. The syntax for using netstat is to enter **netstat option** at the shell prompt of the system you want to scan. You can use the options listed in Table 17-2.

An example of using netstat with the -l option to view a list of listening sockets on a Linux host is shown in Figure 17-12.

In addition to unloading unneeded services, you should also install operating system updates. Let’s discuss how this is done next.

# Installing Updates

One of the most important things you can do to defend against network attacks is to regularly install operating system updates. A simple fact of life that we have to deal with in the IT world is that software isn’t written perfectly. Most programs and services have some defects. Even your Linux kernel has defects in it. Some of these defects are inconsequential, some are just annoying, and others represent serious security risks.

As software is released and used, these defects are discovered by system administrators, users, and (unfortunately) hackers. As they are discovered, updates are written and released that fix the defects. With most distributions, you can configure the operating system to automatically go out on the Internet and periodically check for the availability of updates. For example, with SUSE Linux, you can use the YAST Online Update module, shown in Figure 17-13, to do this. You can configure the system to either automatically install them for you or prompt you to install them. The tool you use to update your system will vary depending upon which Linux distribution you are using.

> **TIP** Another thing you should do to protect network communications is use OpenSSH to encrypt sensitive data being transferred from system to system. Using OpenSSH is a big topic, so we’ll address it in more detail in the next chapter.

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_714_0.png)

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_715_0.png)

### Figure 17-13 Updating the system

You should also implement a host-based firewall to protect your Linux system. Let’s discuss how this is done next.

# Implementing a Firewall with iptables

Today, most organizations connect their corporate networks to the Internet. Doing so enhances communications and provides access to a wealth of information. Unfortunately, it also exposes your network to a serious security threat. If your users can go out on the Internet, then an uninvited person from the Internet can also get into your network unless you take measures to keep this from happening. To do this, you need to implement a network firewall as well as host-based firewalls on each system.

A network firewall is very different from a host-based firewall. A host-based firewall controls traffic in and out of a single computer system. A network firewall, on the other hand, is used to control traffic in and out of a network segment or an entire network.

In this part of the chapter, we’re going to spend some time learning how to use Linux in both capacities. We’ll discuss the following topics:

- How firewalls work
- Implementing a packet-filtering firewall

Let’s begin by discussing how firewalls work.

# How Firewalls Work

So what exactly is a firewall? A firewall is a combination of hardware and software that acts like a gatekeeper between your network and another network. Usually, a firewall has two or more network interfaces installed. One is connected to the internal network; the other, connected to the public network, acts much like a router. However, a firewall is not a router (although it may be implemented in conjunction with one).

The job of a firewall is to monitor the traffic that flows between the networks, both inbound and outbound. You configure the firewall with rules that define the type of traffic that is allowed through. Any traffic that violates the rules is not allowed, as shown in Figure 17-14.

Firewalls can be implemented in a variety of ways. One of the most common types is a *packet-filtering firewall*. In a packet-filtering firewall, all traffic moving between the private and public networks must go through the firewall. As it does, the firewall captures all incoming and outgoing packets and compares them against the rules you’ve configured.

The firewall can filter traffic based on the origin address, the destination address, the origin port, the destination port, the protocol used, or the type of packet. If a packet abides by the rules, it is forwarded on to the next network. If it doesn’t, it is dropped, as shown in Figure 17-15.

Packet-filtering firewalls don’t necessarily have to be implemented between your network and the Internet. They can also be implemented between a network segment and a backbone segment to increase your internal network security.

To use a packet-filtering firewall, you must be familiar with which port numbers are used by default by specific services. IP ports 0 through 1023 are assigned by the IANA organization to network services and are called *well-known* ports. Some of the more common port assignments that you need to be familiar with are shown in Table 17-3.

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_716_0.png)

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_717_0.png)

### Figure 17-15 Using a packet-filtering firewall

Packet-filtering firewalls are widely used. They cost less than other types of firewalls. They also require relatively little processing. Data moves through very quickly, making them much faster than other firewalls.

> **TIP** You can also implement stateful firewalls as well as application-level gateways, both of which operate higher up in the OSI model. Unfortunately, we don’t have time or space to address how they work here.

## Table 17-3 Common Port Assignments

| Port | Service |
| --- | --- |
| 20, 21 | FTP |
| 22 | OpenSSH |
| 23 | Telnet |
| 25 | SMTP |
| 53 | DNS |
| 80, 443 | HTTP and HTTPS |
| 110 | POP3 |
| 119 | NNTP |
| 137, 138, and 139 | SMB and NetBIOS (used by Samba) |
| 143 | IMAP |
| 161 and 162 | SNMP |
| 177 | X Display Manager Control Protocol (xdmcp) |
| 389, 636 | LDAP (insecure and secure) |
| 631 | IPP |

With this background in mind, let's review how to implement a packet-filtering firewall on Linux.

# Implementing a Packet-Filtering Firewall

Just as Linux can act as a router, it can also be configured to function as a firewall. In fact, it can be used to configure a very robust, very powerful firewall.

The first step in setting up a packet-filtering firewall on a Linux system is to design your implementation. You should answer the following questions in your firewall design:

- Will you allow all incoming traffic by default, establishing rules for specific types of traffic that you don't want to allow in?
- Will your firewall deny all incoming traffic except for specific types of traffic that you want to allow?
- Will you allow all outgoing traffic by default, blocking only specific types or destinations?
- Will you block all outgoing traffic except for specific types or destinations?
- What ports must be opened on the firewall to allow traffic through from the outside? For example, are you going to implement a web server that needs to be publicly accessible behind the firewall? If so, then you will need to open up port 80 and probably 443 on your boundary firewall.

How you decide to configure your firewall depends on your organization's security policy. However, I recommend that you err on the side of caution. Given a choice, I'd rather deal with a user who's upset because the firewall won't let him share bootlegged music files over the Internet than deal with a major attack that has worked its way deep into my network.

Once your firewall has been designed, you're ready to implement it. After installing and configuring the required network boards, you can configure a firewall on your Linux system using the iptables utility. Many Linux distributions include graphical front ends for iptables that you can use to build your firewall. These front ends are usually not as flexible as the command-line utility, but they make the setup process much faster and easier!

The heart of the Linux firewall is the iptables package. Most distributions include it. If yours didn't, it can be downloaded from www.netfilter.org. Versions of the Linux kernel prior to 2.4 used ipchains instead of iptables. If you visit the Linux Documentation Project at www.tldp.org, you'll see that many of the firewall HOWTOs are still written to help with these older packages.

The Linux kernel itself completes packet-filtering tasks on Linux. In order to use iptables, your kernel must comply with the netfilter infrastructure. The netfilter infrastructure is included by default when installing most distributions.

The netfilter infrastructure uses the concept of tables and chains to create firewall rules. A chain is simply a rule that you implement to determine what the firewall will do with an incoming packet. The netfilter infrastructure uses the filter table to create packet-filtering rules. Within the filter table are three default chains:

- **FORWARD** The FORWARD chain contains rules for packets being transferred between networks through the Linux system.
