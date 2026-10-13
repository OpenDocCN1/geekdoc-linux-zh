
Consider the following example:

```text
iptables -t nat -A PREROUTING -p tcp --dport 80 -i eth0 -j DNAT --to 192.168.0.2:80
```

This iptables rule will perform NAT prerouting. This allows the destination address change to be applied before the packet hits the kernel routing table. The only packets are TCP packets destined for port 80 (our http server) and coming in on eth0 (other interfaces are not affected by this rule). Our destination NAT (DNAT) rule says to redirect all traffic to this interface on port 80 to 192.168.0.2 on port 80 there.

The iptables rules can also provide some rudimentary load balancing. If a range of IPs is the target, netfilter will send the packet to the target with the fewest connections. So if you have several DNS servers behind your firewall, netfilter can help balance which DNS server is hit.

### Project: Building a NAT System

Let's take what you've learned and use it to build a NAT system for your network. The following are the parameters:

- You are assigned the `209.127.112.0/29` IP address block from your ISP. Your T1 router (CSU/DSU) is assigned `209.127.112.1`. You will use `209.127.112.2` and `209.127.112.3` on your NAT firewall.

- Your internal network is `192.168.10.0/24`, and your NAT system (gateway) is `192.168.10.1` (`eth0`). You have the following systems on your network:

  - `192.168.10.2` Web server
  - `192.168.10.3` mail server
  - `192.168.10.4` FTP server
  - `192.168.10.5` MySQL server on port 3306

  Each system runs Webmin w/SSL on port 10000, but you need to administer any internal system from outside.

- All incoming traffic comes in on `209.127.112.2` (`eth1`). You want to use `209.127.112.3` (`eth2`) for your outgoing connections.

- You want to allow outgoing connections to all privileged ports (0–1023) and port 3306.

- You want your road warriors to be able to POP mail from the mail server while traveling (their systems are already configured for sending and receiving mail while away from the office).

All of this is shown graphically in Figure 35.3.

Putting the rules together you might have something like the following:

- The following two rules enable connections to privileged ports (both TCP and UDP) to be masqueraded:

    ```text
    iptables -t nat -A POSTROUTING -o eth2 -p tcp -j SNAT --to 209.127.112.3:0-1023
    iptables -t nat -A POSTROUTING -o eth2 -p udp -j SNAT --to 209.127.112.3:0-1023
    ```

- This rule enables users to connect to a MySQL server (or any other server binding port 3306) to pass through the firewall and have it masqueraded:

  `iptables -t nat -A POSTROUTING -o eth2 -p tcp -j SNAT --to 209.127.112.3:3306`

- This rule masquerades ICMP traffic:

  `iptables -t nat -A POSTROUTING -i -p ICMP -j SNAT --to 209.127.112.3`

- The following five rules port traffic from port 80, port 25, POP3 (port 110), FTP (port 21), and MySQL (port 3306) to the appropriate systems:

    ```text
    iptables -t nat -A PREROUTING -i eth1 -p tcp --dport 80 -j DNAT --to 192.168.10.2:80
    iptables -t nat -A PREROUTING -i eth1 -p tcp --dport 25 -j DNAT --to 192.168.10.3:25
    iptables -t nat -A PREROUTING -i eth1 -p tcp --dport 110 -j DNAT --to 192.168.10.3:110
    iptables -t nat -A PREROUTING -i eth1 -p tcp --dport 21 -j DNAT --to 192.168.10.4:21
    iptables -t nat -A PREROUTING -i eth1 -p tcp --dport 3306 -j DNAT --to 192.168.10.5:3306
    ```

- The next four rules use a little ingenuity to port Webmin traffic through the firewall to the appropriate system on port 10000. Note the use of matching IPs to ports:

    ```text
    iptables -t nat -A PREROUTING -i eth1 -p tcp --dport 10002 -j DNAT --to 192.168.10.2:10000
    iptables -t nat -A PREROUTING -i eth1 -p tcp --dport 10003 -j DNAT --to 192.168.10.3:10000
    iptables -t nat -A PREROUTING -i eth1 -p tcp --dport 10004 -j DNAT --to 192.168.10.4:10000
    iptables -t nat -A PREROUTING -i eth1 -p tcp --dport 10005 -j DNAT --to 192.168.10.5:10000
    ```

![](img/c741b1b6b6eccaba2ad43454c979a7f8_710_0.png)

These rules should get you started and give you a good idea of how to manipulate rules and mangle IP:Port numbers. This is by no means complete. You'll want to read Chapter 36, particularly the section explaining established and related connections. Logging can also help you if you can't see where connections are refused or dropped.

## CHAPTER 36: IP FIREWALLING

In this chapter

- Introduction to Firewalls 694
- Physical Configurations 697
- The Firewall Kernel 697
- Software Considerations 705
- Other Considerations 705
- iptables General Information 705
- User-Defined Chains 713
- Simple Firewall Policies 714
- Monitoring 715
- Under Attack 715
- Network Security Policy 715
- Project: A Simple Packet-Filtering Firewall 716

### INTRODUCTION TO FIREWALLS

The term firewall comes from the firewall that is used in cars (and other motorized vehicles), which protects the occupants in the cabin in case of a fire in the engine compartment. A firewall on a network protects both users and the data that is behind it on the local network from the savagery of the Internet (or extranet). It can also be used to prevent users on the local network from connecting to prohibited sites, and to compartmentalize the internal network.

Some people learn too late that a firewall does not protect against insiders. Internal firewalls can be used to isolate departments so that damage is not widespread; for example, firewalls can be used to protect accounting from engineering, and engineering from sales, each of which likely has little or no business browsing through files that belong to the others.

Basically, two kinds of firewalls exist in Linux and each basic type has two subtypes. The two basic types are packet filters and proxy firewalls. The packet filter firewalls can be one of the following types:

- **Forwarding**—It is in this type of packet filter firewall that decisions are made whether to forward or not.
- **Masquerading**—These firewalls rewrite the source and destination addresses.

Proxy firewalls can be one of the following types:

- **Standard**—With this type of proxy firewall, a client connects to a special port and is redirected to get through another port.
- **Transparent**—With this firewall, the client doesn't use a special port, but the firewall software proxies the connection through transparently.

This chapter deals primarily with packet filtering firewalls. The information in this chapter is designed to complement and round out the information in Chapter 35, "IP Masquerading."

### PACKET FILTERS

Packet filtering firewalls work on the following principle: The information that is needed to make a decision about what to do with a packet is contained in the header. The header contains information regarding the source and destination addresses, time to live (TTL), protocol, and much more. It also contains a header checksum that helps identify whether the header has been corrupted. In all, some thirteen separate fields of information are contained in an IP header, many of which contain multiple pieces of information. For complete details, refer to RFC 791 (available from http://www.rfc-editor.org/rfc.html).

IP does not check the payload other than to tell whether the payload is the correct size. The Transmission Control Protocol (TCP) is responsible for ensuring the integrity of the data payload. UDP packets have no inherent error checking.

Linux, starting with the new 2.4.0 kernel, uses netfilter and the iptables userland utility to provide packet filtering. To implement a packet filtering firewall, decisions must be made regarding the types of packets to address specifically, and what to do with those packets when they are encountered.

The iptables software permits a number of different criteria to be applied to packets. The criteria can be applied to incoming packets, outgoing packets, or packets that will pass through the firewall. These decisions can be based on where the packets came from by address, where they are going by address, or where they are going by port. Different rules can be applied, depending on whether these are TCP packets, UDP packets, or ICMP packets. The netfilter framework also works on packet pre- and post-routing, and can filter connections based on new, established, or related connections, as well as address packets specifically based on set flags in the packet. Netfilter can also mangle packets, changing flags, which can then be used to prioritize packet queuing. Finally, for any packets that are not specifically addressed, the overall policy determines the fate of the packets.

The netfilter ability to handle packets associated with established or related connections makes netfilter "stateful." This is an overly abused marketing term that means the software can track connections. Actually, any packet filter software (like the older ipchains from Linux kernel version 2.2.x) that permits active FTP sessions is stateful. This also applies to any software capable of tracking masqueraded connections. Netfilter allows rules to be applied specifically to established or related connections. Netfilter also tracks those connections and subsequent (established or related) packets don't traverse the entire set of rules, but only use those that applied to the initial connection, making netfilter faster.

### Proxy Firewalls

Proxy firewalls work differently than packet filters do. All traffic is received on the firewall, whether it is incoming or outgoing. But proxies redirect permitted traffic through the firewall by rewriting the headers. To be redirected, the traffic must log in to the firewall. In fact, much of the discussion in the preceding section is applicable to a proxy. The difference is subtle; because packet filtering software is rewriting the headers when it is masquerading, it is difficult to explain that there is a difference between a transparent proxy and a masquerading (packet filter) firewall. But the main difference is that the proxy redirects (locally) the traffic that is arriving at one interface and leaving by another, and a packet filter normally does not redirect all traffic. Looking at it from a different perspective, proxies work higher up in the OSI model than packet filters.

> **Note**
>
> Any router, gateway, or host that transports a networking packet from one network to another rewrites the header. But this rewriting doesn't alter the source or destination addresses; it only alters the TTL and checksum, and—on occasion—the total length and fragment offset (among others). When header rewriting is discussed in this text, it refers mostly to address rewriting.
