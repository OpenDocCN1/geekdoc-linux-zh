
## FIGURE 2.1

Firewall placement in the TCP/IP reference model.

![](img/d1359a287d9d43cd5ed19f3a7b55d40d_53_0.png)

![](img/d1359a287d9d43cd5ed19f3a7b55d40d_53_1.png)

![](img/d1359a287d9d43cd5ed19f3a7b55d40d_53_2.png)

![](img/d1359a287d9d43cd5ed19f3a7b55d40d_53_3.png)

This sounds pretty powerful, and it is; but it isn't a surefire security mechanism. It's only part of the story, just one layer in the multilayered approach to data security. Not all application communication protocols lend themselves to packet filtering. This type of filtering is too low-level to allow fine-grained authentication and access control. These security services must be furnished at higher levels. IP doesn't have the capability to verify that the sender is who he or she claims to be. The only identifying information available at this level is the source address in the IP packet header. The source address can be modified with little difficulty. One level up, neither the network layer nor the transport layer can verify that the application data is correct. Nevertheless, the packet level allows greater, simpler control over direct port access, packet contents, and correct communication protocols than can easily or conveniently be done at higher levels.

Without packet-level filtering, higher-level filtering and proxy security measures are either crippled or potentially ineffective. To some extent, at least, they must rely on the correctness of the underlying communication protocol. Each layer in the security protocol stack adds another piece that other layers can't easily provide.

## FIGURE 2.2

Input and output chains.

![](img/d1359a287d9d43cd5ed19f3a7b55d40d_54_0.png)

### Choosing a Default Packet-Filtering Policy

As stated earlier in this chapter, a firewall is a device to implement an access control policy. A large part of this policy is the decision on a default firewall policy.

There are two basic approaches to a default firewall policy:

- Deny everything by default, and explicitly allow selected packets through.
- Accept everything by default, and explicitly deny selected packets from passing through.

Without question, the deny-everything policy is the recommended approach. This approach makes it easier to set up a secure firewall, but each service and related protocol transaction that you want must be enabled explicitly (see Figure 2.3). This means that you must understand the communication protocol for each service you enable. The deny-everything approach requires more work up front to enable Internet access. Some commercial firewall products support only the deny-everything policy.

#### FIGURE 2.3

The deny-everything-by-default policy.

![](img/d1359a287d9d43cd5ed19f3a7b55d40d_55_0.png)

The accept-everything policy makes it much easier to get up and running right away, but it forces you to anticipate every conceivable access type that you might want to disable (see Figure 2.4). The danger is that you won't anticipate a dangerous access type until it's too late, or you'll later enable an insecure service without first blocking external access to it. In the end, developing a secure accept-everything firewall is much more work, much more difficult, almost always much less secure, and, therefore, much more error-prone.

#### FIGURE 2.4

The accept-everything-by-default policy.

![](img/d1359a287d9d43cd5ed19f3a7b55d40d_56_0.png)

### Rejecting Versus Denying a Packet

The Netfilter firewall mechanism in iptables gives you the option of either rejecting or dropping packets. What's the difference? As shown in Figure 2.5, when a packet is rejected, the packet is thrown away and an ICMP error message is returned to the sender. When a packet is dropped, the packet is simply thrown away without any notification to the sender.

#### FIGURE 2.5

Rejecting versus denying a packet.

![](img/d1359a287d9d43cd5ed19f3a7b55d40d_57_0.png)

Silently dropping the packet is almost always the better choice, for three reasons. First, sending an error response doubles the network traffic. The majority of dropped packets are dropped because they are malevolent, not because they represent an innocent attempt to access a service you don't happen to offer. Second, a packet that you respond to can be used in a denial-of-service (DoS) attack. Third, any response, even an error message, gives the would-be attacker potentially useful information.

### Filtering Incoming Packets

The input side of the external interface I/O pair, the input chain, is the more interesting in terms of securing your site. As mentioned earlier, you can filter based on source address, destination address, source port, destination port, and TCP status flags. You'll learn about all these pieces of information at one point or another in the following sections.

### Remote Source Address Filtering

At the packet level, the only means of identifying the IP packet's sender is the source address in the packet header. This fact allows for the possibility of source address spoofing, in which the sender places an incorrect address rather than his or her own address in the source field. The address might be a nonexistent address, or it might be a legitimate address belonging to someone else. This can allow unsavory types to break into your system by appearing as local, trusted traffic; appearing to be you while attacking other sites; pretending to be someone else while attacking you; keeping your system bogged down responding to nonexistent addresses; or otherwise misleading you as to the source of incoming messages.

It’s important to remember that you usually can’t detect spoofed addresses. The address might be legitimate and routable but might not belong to the packet’s sender. The next section describes the spoofed addresses you can detect.

## SOURCE ADDRESS SPOOFING AND ILLEGAL ADDRESSES

There are 10 major classes of source addresses you should deny on your external interface in all cases. These are incoming packets claiming to be from the following:

1. **Your IP address** —You will never see legal incoming packets claiming to be from your machine. Because the source address is the only information available and it can be modified, this is one of the forms of legitimate address spoofing you can detect at the packet-filtering level. Incoming packets claiming to be from your machine are spoofed. You can’t be certain whether other incoming packets are coming from where they claim to be. (Note that some operating systems crash if they receive a packet in which both the source and the destination addresses belong to the host’s network interface.)

2. **Your LAN addresses** —You will rarely see legal incoming packets on the external, Internet interface claiming to be from your LAN. It’s possible to see such packets if the LAN has multiple access points to the Internet, but it would probably be a sign of a misconfigured local network. In most cases, such a packet would be part of an attempt to gain access to your site by exploiting your local trust relationships.

3. **Class A, B, and C private IP addresses** —These three sets of addresses in the historical Class A, B, and C ranges are reserved for use in private LANs. They aren’t intended for use on the Internet. As such, these addresses can be used by any site internally without the need to purchase registered IP addresses. Your machine should never see incoming packets from these source addresses:
    - Class A private addresses are assigned the range from 10.0.0.0 to 10.255.255.255.
    - Class B private addresses are assigned the range from 172.16.0.0 to 172.31.255.255.
    - Class C private addresses are assigned the range from 192.168.0.0 to 192.168.255.255.

CHAPTER 2: Packet-Filtering Concepts

4. **Class D multicast IP addresses**—IP addresses in the Class D range are set aside for use as destination addresses when participating in a multicast network broadcast, such as an audiocast or a videocast. They range from 224.0.0.0 to 239.255.255.255. Your machine should never see packets from these source addresses.

5. **Class E reserved IP addresses**—IP addresses in the Class E range were set aside for future and experimental use and are not assigned publicly. They range from 240.0.0.0 to 247.255.255.255. Your machine should never see packets from these source addresses—and mostly likely won't. (Because the entire address range is permanently reserved up through 255.255.255.255, the Class E range can realistically be defined as 240.0.0.0 to 255.255.255.255. In fact, some sources define the Class E address range to be exactly that.)

6. **Loopback interface addresses**—The loopback interface is a private network interface used by the Linux system for local, network-based services. Rather than sending local traffic through the network interface driver, the operating system takes a shortcut through the loopback interface as a performance improvement. By definition, loopback traffic is targeted for the system generating it. It doesn't go out on the network. The loopback address range is 127.0.0.0 to 127.255.255.255. You'll usually see it referred to as 127.0.0.1, localhost, or the loopback interface, lo.

7. **Malformed broadcast addresses**—Broadcast addresses are special addresses applying to all machines on a network. Address 0.0.0.0 is a special broadcast source address. A legitimate broadcast source address will be either 0.0.0.0 or a regular IP address. DHCP clients and servers will see incoming broadcast packets from source address 0.0.0.0. This is the only legal use of this source address. It is not a legitimate point-to-point, unicast source address. When seen as the source address in a regular, point-to-point, nonbroadcast packet, the address is forged, or the sender isn't fully configured.

8. **Class A network 0 addresses**—As suggested previously, any source address in the 0.0.0.0 through 0.255.255.255 range is illegal as a unicast address.

9. **Link local network addresses**—DHCP clients sometimes assign themselves a link local address when they can't get an address from a server. These addresses range from 169.254.0.0 to 169.254.255.255.

10. **TEST-NET addresses**—The address space from 192.0.2.0 to 192.0.2.255 is reserved for test networks.

A number of other address blocks are reserved by IANA and are not in use. In my experience, it's good to filter out these additional blocks. There's a danger in doing so, however: As the IPv4 address space gets tighter and the number of Internet sites grows, IANA has been
