# Chapter 15: Building Your Own Private Network

✔ **Allow all internal traffic**: You must allow all network traffic on the Internet gateway's internal loopback (lo) interface. The loopback interface is used by the Linux operating system for its own, internal communication. Many internal processes communicate over this virtual network.

✔ **Allow all internal NIC traffic**: You reap greater convenience if you allow the computers on the private network to communicate with the gateway. For example, you may want to administer the gateway via Secure Shell (SSH). Take a lenient approach and allow any external machine to communicate with the gateway; this strategy makes constructing the firewall easier. You may decide to limit internal access if your security needs demand it.

✔ **Allow all outgoing traffic from the firewall**: Allow all outgoing connections from within the firewall. The firewall needs to perform its own internal processes, such as making DNS queries.

✔ **Forward all traffic from the private network**: A gateway has to pass traffic from one interface to another. You change the forwarding policy to permit communication from the private network to pass through the firewall to the Internet. The downside is that traffic from the Internet can pass right through the firewall to the private network — not a good idea. You fix that problem by adding NAT, which effectively prevents external access through the firewall.

You can set up specific forwarding rules to provide more protection to your private network. We believe that using NAT to effectively block connections that originate externally is adequate for your needs.

✔ **Use NAT for outgoing connections**: Create a NAT rule to make all connections originating on the private network appear to be coming from the Internet gateway. All private-network machines have their source addresses and port numbers changed to that of the gateway.

Network-address translation isn't necessary if your Internet connection device (telephone, DSL, or cable modem) performs NAT. By providing a NAT filtering rule, however, you ensure that your Internet gateway works with any connection device — whether or not it performs NAT. NAT also prevents external access to your private network.

✔ **Allow incoming SSH connections**: The Secure Shell (SSH) protocol encrypts network connections. SSH provides a reasonably secure system for connecting to your private network from the Internet. We configure the firewall to allow SSH connections into our firewall.

The firewall on the Internet gateway is similar to the firewall we describe in Chapter 8, except you add IP forwarding and NAT. IP forwarding allows packets from the private network to pass outward through the firewall and on to the Internet. In this case, NAT makes all Internet-bound traffic appear to be coming from the firewall or gateway — and prevents incoming packets from being forwarded inward to your private network.