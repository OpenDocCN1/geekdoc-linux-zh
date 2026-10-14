This dialog lets you enter the following:

+   - *Hostname*—Enter a name by which the computer can be addressed. This name should be unique within the network.

+   - *Domain Name*—This is the name of the DNS domain to which the computer belongs. Domains help to divide networks. All computers in a defined organizational area normally belong to the same domain.
+   
+     A computer can be addressed uniquely by giving its FQDN (Fully Qualified Domain Name). This consists of the hostname and the name of the domain, such as `da10.digitalairlines.com`. In this case, the domain would be `digitalairlines.com`.

+   - *List of name servers*—To address other computers in the network with their hostnames, identify the name servers that will be responsible for converting computer names to IP addresses and vice versa.
+   
+     You can specify a maximum of three name servers.

+   - *Domain search list*—In the local network, it is more convenient to address other hosts with their hostnames rather than their FQDNs. The domain search list specifies the domains with which the system can expand the hostname to the FQDN.
+   
+     This complete name is then passed to the name server to be resolved. For example, `da10` is expanded with the search list `digitalairlines.com` to the FQDN `da10.digitalairlines.com`. This name is then passed to the name server to be resolved.
+   
+     If the search list contains several domains, one after the other is used, and the resulting FQDN is passed to the name server until an entry returns an associated IP address.
+   
+     Separate the domains with commas or white space.

+   - *Routing*—If the computer is intended only to reach other computers in the same subnet, then it is not necessary to enter any routes.
+   
+     However, if you need to enter a default gateway or create a routing table, select **Routing** from the Network Address Setup dialog. The window shown in Figure 5-7 appears.

You can define the following:

+   - *Default Gateway*—If the network has a gateway (a computer that forwards information from a network to other networks), its address can be specified in the network configuration.
+   
+     All data not addressed to the local network is then forwarded directly to the gateway.

+   - *Routing Table*—You can create entries in the routing table of the system after selecting Expert Configuration.

+   - *Enable IP Forwarding*—If you have two network cards in your computer and you select this option, IP packets that are not addressed to your computer are routed from one network interface to the other as needed.

![](bbox=[0.969, 0.272, 1.0, 0.322])