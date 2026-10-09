
## Chapter Summary

DNS maps domain names to IP addresses, and vice versa. It is implemented as a hierarchical, distributed, and replicated database on the Internet. You can improve the security of BIND, which implements DNS, by running it inside a chroot jail and using transaction signatures (TSIGs).

When a program on the local system needs to look up an IP address that corresponds to a domain name, it calls the resolver. The resolver queries the local DNS cache, if available, and then queries DNS servers on the LAN or Internet. There are two types of queries: iterative and recursive. When a server responds to an iterative query, it returns whatever information it has at hand; it does not query other servers. Recursive queries cause a server to query other servers if necessary to respond with an answer.

There are three types of servers. Master servers, which hold the master copy of zone data, are authoritative for a zone. Slave servers are also authoritative and copy their data from a master server or other slave servers. DNS caches are not authoritative and either answer queries from cache or forward queries to another server.

The DNS database holds resource records for domains. Many types of resource records exist, including A (address), MX (mail exchange), NS (nameserver), PTR (pointer for performing reverse name resolution), and SOA (start of authority, which describes the zone) records.

## Exercises

1. What kind of server responds to recursive queries? How does this server work?
2. What kind of DNS record is likely to be returned when a Web browser tries to resolve the domain part of a URI?
3. What are MX resource records for?
4. How would you find the IP address of example.com from the command line?
5. How would you instruct a Linux system to use the local network's DNS cache, located at 192.168.1.254, or the ISP's DNS cache, located at 1.2.3.4, if the LAN nameserver is unavailable?
6. How would you instruct a DNS server to respond only to queries from the 137.44.* IP range?
7. How might a resolver attempt to find the IP address of the example domain?

### Advanced Exercises

8. How would you set up a private domain name hierarchy that does not include any of the official InterNIC-assigned domain names?
9. Which part of DNS is most vulnerable to an attack from a malicious user and why?
10. It is often irritating to have to wait for DNS records to update around the world when you change DNS entries. You could prevent this delay by setting the TTL to a small number. Why is setting the TTL to a small number a bad idea?
11. Outline a method by which DNS could be used to support encryption.

## 25

### firestarter, gufw, AND iptables: Setting Up A FireWall

#### In This Chapter

- Introduction to firestarter . . . . . . . . . . . . 864
- firestarter: Setting Up and Maintaining a FireWall . . . . . . . . . . . . . . 866
- ufw: The Uncomplicated FireWall . . . . . . . . . . . . . . . . . . . . . . . . 874
- gufw: The Graphical Interface to ufw . . . . . . . . . . . . . . . . . . . . . 876
- Rules, matches, targets, and chains . . . . . . . . . . . . . . . . . . . . . . . . . . 880
- Anatomy of an iptables Command . . . . . . . . . . . . . . . . . . . . . . . 884
- Building a Set of Rules Using iptables . . . . . . . . . . . . . . . . . . . . 885
- Copying Rules to and from the Kernel . . . . . . . . . . . . . . . . . . . . 891
- Sharing an Internet Connection Using NAT . . . . . . . . . . . . . . . . . . 892

The gufw and firestarter utilities are user-friendly, graphical front-ends for iptables; iptables builds and manipulates network packet filtering (page 1164) rules in the Linux kernel. You can use firestarter, or iptables directly, to create a firewall that protects a system from malicious users and to set up NAT (Network Address Translation, page 1161), which can allow several systems to share a single Internet connection. In addition, firestarter can control a DHCP server.

The iptables utility is flexible and extensible, allowing you to set up both simple and complex network packet filtering solutions. It provides connection tracking (stateful packet filtering), allowing you to handle packets (page 1164) based on the state of their connection. For example, you can set up rules that reject inbound packets trying to open a new connection and accept inbound packets that are responses to locally initiated connections. Many features not included in the base iptables package are available as patches via the patch-o-matic program.

The firestarter utility is frequently sufficient to protect a single system or a small LAN but, because of its user-friendly nature, it does not provide access to the full complexity and power of iptables. Most of the concepts involving firestarter will probably be familiar, or easy to learn, for someone who is familiar with basic networking. Some of the concepts required to fully understand iptables are beyond the scope of this book. Although you can use iptables at different levels, this chapter presents only the fundamentals. There are, however, some sections of this chapter that delve into areas that may require additional understanding or explanation. If a concept is not clear, refer to one of the resources in "More Information" on page 883.

- **ufw and gufw**: Ubuntu has added ufw (uncomplicated firewall) and its graphical interface gufw to its security arsenal. As these products mature, you may want to consider experimenting with and using them in place of firestarter. See page 874 (ufw) and page 876 (gufw) for more information.

#### Routers have firewalls too

- **tip**: Many systems are already protected by a firewall located in a router. If you use a router that has a firewall, you may need to open ports on the router firewall in addition to opening ports on any firewall you set up on an Ubuntu system.

#### INTRODUCTION to firestarter

The firestarter utility is a sophisticated, graphical tool for building and maintaining a firewall. Although it works with GTK and is designed to run under GNOME, it is equally at home under KDE. This utility enables a system to share an Internet connection with other systems on a LAN. It can also set up and control a DHCP (page 470) server. It provides a real-time view of intrusion and other events and allows you to tune ICMP (page 1153) parameters to help stop DoS attacks (page 1146). As installed, firestarter allows outbound connections and blocks and displays information about inbound connections that originate outside the system or LAN it is protecting (that is, connections that originate on the Internet). As you view these events, you can set up rules to allow them, facilitating firewall customization.

The firestarter utility can protect the single system it runs on (the firewall host) or it can protect the system it runs on as well as other client systems on a LAN that connect to the Internet through the firewall host. Figure 25-1 shows a typical setup where all network traffic to and from a LAN must pass through the firewall, enabling the firewall to control access between the Internet and the LAN (including the firewall host). In this setup the firewall host acts as a router (page 377).

#### NOTES

- **Terminology**: This section explains what some of the words used to explain firestarter mean in this context. The terms *firewall* and *firestarter* are used interchangeably.
- **(Firewall) host (system)**—The system the firewall is running on.

![](img/2344fc4a798f29dca9e8b5ed7288171a_915_0.png)

Internet
Firewall host
(router)
LAN
(client systems)

**Figure 25-1** A typical firewall setup

- **Client systems**—Systems that are on the same LAN as the firewall host and whose packets to and from systems outside the LAN (specifically the Internet) pass through the firewall host.
- **Policy**—The set of rules that the firewall applies.
- **Rule**—A statement that specifies what the firewall does with specific types of packets it receives from specific systems on its network interface(s).
- **Connection**—Under TCP, the path through which two systems exchange data. A client system opens a connection with a server system by sending it a SYN (synchronization) packet. The server sends an ACK (acknowledge) packet back to the client and the two systems exchange data. The client closes the connection with a SYN packet. Although UDP works differently because it has no concept of a connection, for the purposes of this discussion the concept of a UDP connection is appropriate.
- **Inbound connections**—Include connections that originate from the Internet and client systems with the firewall host as the destination.
- **Outbound connections**—Include connections that originate from the firewall host and client systems with the Internet as the destination.

**Default policy** By default, firestarter implements a user-friendly policy that protects the firewall host and client systems. In general, it allows outbound traffic and blocks inbound traffic that is not sent in response to outbound traffic. Specifically, the default firestarter policy
- Blocks new inbound connections from the Internet that are destined for the firewall host or the client systems.
- Allows inbound packets that are sent in response to connections initiated by the firewall host or client systems to the Internet.
- Allows the firewall host to establish connections.
