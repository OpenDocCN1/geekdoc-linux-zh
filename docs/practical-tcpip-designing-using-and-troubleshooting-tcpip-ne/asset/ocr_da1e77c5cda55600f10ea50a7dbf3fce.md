# **Using multiple addresses and an internal router together**

In Module 6.5 we mentioned that in some special circumstances it's useful to have extra IP addresses on a tester's PC, to access internal test networks. You can combine this approach with using an internal router, as shown in the figure below. The tester's PC uses its extra addresses to access non-standard devices directly, and uses the internal router for easy access to any extra test networks that may be added temporarily.

![](bbox=[0.05, 0.19, 0.86, 0.47])

# **Sub-netting**

For readable background on how and why sub-netting came about, see:

+   □ **RFC-917 October 1984** *Internet Subnets*

For information on using DHCP with CIDR (i.e. not class-ful) routes, see:

+   □ **http://www.ietf.org/internet-drafts/draft-ietf-dhc-csr-06.txt** (Expires April-2002)
+   IETF draft on DHCP and CIDR sub-nets

An interesting consequence of how ranges work is that if two networks overlap at all, they are either identical or one is completely contained in the other. It's impossible to have two ranges as below:

![](bbox=[0.32, 0.69, 0.6, 0.78])

# **Sub-net mask as opposed to netmask**

We mention this not because it's useful nowadays, but out of historical interest and also in case you're reading older documents and get confused with “network IDs” and “sub-net IDs.”

Before CIDR was invented, sub-netting was “different” and quite separate from basic inter-networking technology. Every site on the Internet had a class A, B, or C set of addresses and the address classes were used for routing between sites over the Internet backbone. Sub-netting was used within your site to divide up your class A, B, or C range and this is what the “sub-net mask” was invented for. It worked as follows. For simplicity, let's assume your Internet site has been allocated the class B range of addresses, 192.0.2.0.–192.0.2.255: