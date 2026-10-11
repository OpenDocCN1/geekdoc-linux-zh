less-fortunate network administrators must suffer. The reality, however, is that firewalls do not ensure instant protection from an ever-changing array of threats. Furthermore, even the simplest of firewalls can be complicated to configure. Because of this, many fire- walls in use today are misconfigured, and the overwhelming majority of them are under- configured.

Unlike the bricks-and-mortar version, a network firewall must not only protect the inside network from intrusion, but it must also allow users to reach outside resources while allowing certain connections back to those users. This sounds like a simple concept, but its implementation is often challenging.

The good news, however, is that Linux itself easily serves as an efficient firewall device. The Linux kernel has the native ability to inspect the headers of packets received by the system. The iptables tool provides full control of packet filtering, network address translation, and even stateful inspection, where the decision of whether to accept or reject a packet is made in the context of a previously established flow (like an outgoing telnet request).

The classic example of the stateful inspection capability is what allows a firewall to permit an incoming ftp-data connection (TCP port 20) only when a local host has initiated an ftp-control connection (TCP port 21). By remembering the state of the outgoing connec- tion from a given internal IP address, the firewall allows the incoming ftp-data connection only while the outgoing ftp-control connection is still in the ESTABLISHED state.

The combination of iptables/ip6tables and kernel support makes Linux a very solid platform on which to protect your network perimeter.

# # Linux as a Firewall Platform

So why should you choose the Linux platform over the competing offerings, both open source and commercial? Ultimately, you are seeking the best protection for your network perimeter. So, before jumping into the discussion of how you go about setting up a Linux firewall, let's talk briefly about the reason why you would want to do this. These are the major advantages of a Linux platform over its competition:

+   * **Uniform Administration** There is nothing magical about using a Linux server to act as a firewall device, except for the fact that you'll be running a number of com- mands that affect kernel packet filtering and perhaps network address translation (NAT). Your training and experience as a Linux administrator can be applied toward the administration of your firewall. You know Linux and you understand it, which is your best protection when something goes wrong.
+   * **Commodity Hardware** Unlike some of the commercial firewall appliances that employ proprietary (i.e., expensive) and sometimes obscure hardware, the Linux