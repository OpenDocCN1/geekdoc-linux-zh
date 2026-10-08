# CHAPTER 7 | Networks, Firewalls, and More

# A Firewall for the Demilitarized Zone (DMZ)

If you have bastion servers that provide services such as Web sites and FTP-based file sharing, considering them in a DMZ. A DMZ network is separate from but bits between the Internet and an otherwise private network, as shown in Figure 7-5.

The networks described in Figure 7-5 require additional explanation. Figure 7-5 depicts three distinct networks. The wide area network (WAN) may be a corporate network or the Internet. The DMZ is an internal network with one private IP network address. The protected internal network has a distinct and separate IP network address. To translate between networks, both routers are configured to masquerade IP addresses. The network addresses shown are just two possible examples. Traffic between the WAN (Internet) and the protected internal network is filtered through two different firewall routers.

Each firewall router has two network devices. The eth0 on the external firewall router is connected to the WAN (Internet). The second Ethernet device (eth1) on that same router is connected to the DMZ network. All traffic directed to and from the DMZ and the protected internal network is filtered through a firewall on this router.

![](bbox=[0.052, 0.439, 0.943, 0.936])