
## Configuring a Firewall

Chapter 21

### In This Chapter

- Understanding Firewalls 490
- Setting Up a Packet Filter 499
- Setting Up a Proxy Server 504
- Firewall Care and Maintenance 510
- Summary 512

One of the most common computer networking buzzwords these days is firewall. Small companies and even individuals post to various newsgroups asking for advice on purchasing a firewall or configuring a computer as one. Employees gripe that their companies’ firewalls interfere with their use of the Internet. Companies seek out network administrators with experience configuring custom firewalls.

Ideally, a firewall goes unnoticed by legitimate users of a system while simultaneously blocking access by would-be crackers. Unfortunately, this ideal is difficult to attain. Like many aspects of computer security, it’s easy to configure a firewall to be transparent to users but not very secure, or secure but a major nuisance to users. Implementing security and ease of use is hard. The goal of this chapter is not to present everything you need to know about firewalls; entire books have been written about firewalls, and I can only present some basics in this chapter. After reading this chapter, though, you should know enough to determine what type of firewall you want, the general steps involved in configuring one, and where to go to find the details.

If you haven’t already done so, you may want to read Chapters 2, “Understanding TCP/IP,” and 3, “Networking Services.” Firewall technologies often interact with different layers of the TCP/IP stack, ports, and so on, so it’s important that you be familiar with these concepts when you learn about and configure a firewall.

## Understanding Firewalls

The first step on the road to firewall installation is to understand what a firewall is, what it can do, and when the use of a firewall may be useful to you. This section covers these issues.

### What Is a Firewall?

Most generally, a firewall is a network device that controls the flow of data between two networks. This may sound similar to a router (p. 87), but an ordinary router is a fairly passive device; it merely passes packets uncritically from one network to another. A firewall, by contrast, examines the packets to one extent or another and makes a decision about what to do with them.

In this chapter, I discuss two different types of firewalls: packet filters and proxy servers. These terms aren’t used universally; for instance, some people refer to them as chokes and gates, respectively. Others may consider packet filters in a class by themselves, separate from firewalls. If you do further reading on firewalls, you should be aware of these differences in terminology.

### Making Low-Level Decisions: Packet Filters

A packet filter firewall can be fairly unobtrusive. Such a filter makes decisions about what data to pass based on a fairly shallow analysis of the packets it is asked to relay. For instance, a packet filter can examine the source and destination addresses, port numbers, and the type of protocol involved (such as Telnet or HTTP). When you configure a packet filter, you set up a series of rules that define what type of traffic you allow and what to do with traffic that you don’t allow (ignore it, send a reject message to the originating host, log the rejection, and so on).

In fact, packet filters are closely related to several other networking technologies. The lines between some of these technologies are rather blurred:

- Routers—A conventional router passes IP packets from one network to another without paying them much attention. Many routers can be configured to perform packet filtering, though, so if you have a dedicated router, you may want to investigate whether it can be configured in this way. If so, you might save yourself some effort in configuring a Linux firewall.
- IP masquerading—Like packet filters, IP masquerading examines packets and makes forwarding decisions based on what it sees. IP masquerading also rewrites the packets’ headers, though, to make them appear as if they come from the IP masquerading computer. IP masquerading is an asymmetric technique in the sense that it allows one network to “hide” behind a single computer, but the outside world isn’t normally hidden from the private network.
- NAT—Like IP masquerading, network address translation (NAT) allows the router to alter the appearance of an internal network. NAT is somewhat more flexible than IP masquerading in the sense that it can selectively hide computers rather than hiding them all.

In practice, you may want to combine several of these functions. For instance, you could configure a system to use IP masquerading and to apply firewall rules to protect the network from outside probes.

To configure Linux for packet filtering, you compile assorted features into the kernel, as described shortly, and use the ipchains utility to set up rules for accepting, rejecting, and forwarding packets. This procedure is very similar to that used to configure IP masquerading, in fact, although you might use an entirely different rule set for packet filtering than for IP masquerading.
