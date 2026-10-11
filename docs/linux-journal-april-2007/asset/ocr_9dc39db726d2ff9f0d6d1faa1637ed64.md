# PacketFence

# How to set up and use the powerful open-source network access control solution.

LUDOVIC MARCOTTE AND DOMINIK GEHL

With the ever-increasing number of attacks on networks—either by people accessing them anonymously or generating illegal activities from them, having great security tools is essential. Although a good firewall and tools, such as Snort and Nessus, can increase security, network administrators are looking for solutions that complete those security tools by responding automatically to a violation of network usage policy. Such tools are called network access control (NAC) solutions. Many of those tools exist—especially proprietary ones from big vendors, such as Cisco—but an open-source solution, PacketFence, deserves attention.

PacketFence is a free and open-source solution that provides network access control functionalities, including the following standard features:

+   » Registration of network endpoints (desktops, laptops, printers and so on) and, optionally, acceptance of a network usage policy upon registration before gaining complete network access.
+   » Detection of network usage policy violations based on passive and active network scans on all connected nodes.
+   » Isolation of offending nodes.
+   » Notification (e-mail, pop-ups and so on) based on a network usage policy violation.
+   » Remediation so that network components can regain their network access after a violation.

PacketFence is written in Perl and makes use of common open-source components, such as MySQL, Apache, Snort and Nessus. It does not require a user agent to be installed on computers accessing the network. Its deployment is non-intrusive, and every interaction with users goes through a captive portal that can be accessed by every Web browser.

PacketFence currently supports ARP, DHCP/DNS and VLAN isolation techniques. Choosing the right isolation method depends on the size of your network and the networking equipment you possess. In this article, we cover ARP-based isolation, which works on any kind of networking equipment.

# ARP-Based Isolation

ARP-based isolation works by poisoning the ARP cache of any equipment connected to the network. As you know, ARP is a protocol used to map IP addresses to MAC addresses. Fundamentally, four basic types of messages exist in Ethernet ARP that are interesting for PacketFence:

+   1. ARP request: request for the destination MAC.
+   2. ARP reply: reply containing the MAC.
+   3. RARP request: request IP from MAC.
+   4. RARP reply: reply containing the IP.

The problem with ARP is that when a client issues an ARP request, it simply trusts the reply that comes in and stores it into its cache. Poisoning the ARP cache is as simple as sending ARP replies to the client, even if it hasn't asked for one. The operating system likely will update the cache upon reception of such packets, or it'll use the poisoned data we send when it decides to update the cache.

# Installation and Configuration

PacketFence has been developed on Red Hat Enterprise Linux 4, CentOS 4 and Fedora Core. Several people have succeeded in running it on different distributions, but to ease your first installation, it might be better to stick with one of the officially supported distributions. Because PacketFence is a NAC solution and installing it will act on your current LAN, make sure to coordinate your tests with your network administrator.

# Preparation

PacketFence uses a MySQL database to store the information about the nodes connected to the network, whom they belong to and whether there are any violations of the specified network policy. So, if you don't already have a dedicated MySQL server you want to use for this purpose, install MySQL server by running update -1 mysql-server.

As mentioned previously, PacketFence can use Snort and Nessus, and we describe below how you can integrate both tools with PacketFence.

Snort is an open-source network intrusion detection system that

![](bbox=[0.06, 0.65, 0.44, 0.94])