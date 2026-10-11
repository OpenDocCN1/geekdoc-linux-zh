To add a server, enter the following information:

+   Public and private iFolder server names. If the DNS name or IP address of your iFolder server goes directly to the iFolder server without being routed through another device, meaning that your iFolder server is not behind a firewall, you are only required to fill in the information beneath the Public heading. If the DNS name or IP address of your iFolder server goes through another device, like an L4 switch or a firewall which redirects the request to the iFolder server, you need to fill in the information under both the Public and Private headings.

![](bbox=[0.38, 0.33, 0.4, 0.37])

> If you have Network Address Translation (NAT) functionality built into your routers or switches, enter both your iFolder public and private DNS names and IP addresses.

If your public DNS name or IP address redirects requests to a private iFolder IP address, specify a DNS name (not an IP address) as the public address of the iFolder server. Then, make sure you are using an internal DNS server to resolve the DNS name to the private address for internal users and use an external DNS server to resolve the DNS name to the public address of external users. The Private settings allow the iFolder servers to communicate directly with each other within the iFolder system. The Public settings allow you to access the iFolder server from outside the firewall.

+   iFolder ports. The ports that you enter into the iFolder Management console must match the ports that you specified during the iFolder installation. You can have multiple iFolder servers using the same port numbers if they all have a unique DNS name or IP address.