In Module 4.10 we said there are two different broadcast addresses, but Stevens Chapter 12 explains that there are in fact four: limited broadcast address, network-directed broadcast address, sub-net-directed broadcast address, and all-sub-nets-directed broadcast address. These distinctions don't matter any more, partly because nobody implements them, and partly because the distinction between “network-directed” and “sub-net-directed” only made sense in the pre-CIDR days. Then, as now, an IP address had a network part and a host part. But the host part could be divided further into a sub-net-ID part and a host-ID part. The idea was that your “network” described the view of your site from the Internet, e.g. “we have a class-B network”. Then, within your site, you used sub-netting to arrange you internal routing, using the sub-net part. However, with CIDR, we can have network parts of any number of bits (not just 8, 16, or 24) and so we no longer distinguish between network part and sub-net part. (And consequently, throughout the book we use “subnet-directed” and “network-directed” broadcast synonymously to refer to the broadcast address derived from the netmask on this machine.) We explain in more detail how “old” sub-netting was done in the Notes to Chapter 6.

> Warning: on many versions of Linux, the subnet-directed broadcast address is set incorrectly if your netmask is not the default for your IP address’s “class”. Instead, when you configure your IP address, the broadcast address defaults to the broadcast address for the address class. For example, if your IP address is 10.1.2.3, netmask 255.255.255.0, the broadcast address ought to be 10.1.2.255, but it defaults to 10.255.255.255, because 10.1.2.3 is a class-A address.
> 
> To correct this you must define the broadcast address explicitly using **ifconfig**. You can do it when defining the IP address, as in:
> `ifconfig eth0 10.1.2.3 netmask 255.255.255.0 broadcast 10.1.2.255`
> 
> or you can do it separately afterwards:
> `ifconfig eth0 broadcast 10.1.2.255`
> 
> Windows-NT sets the broadcast address correctly, based on the actual IP address and not the address class.

# ### Multicasting

Stevens Chapters 12 and 13, and Perlman Chapter 15 cover multicasting. See also

+   - http://www.internet2.edu/html/multicast.html/
+   - http://www.abilene.iu.edu/advanced.html

although the latter URL may change so you’ll have to rummage around the site to find the multicast information.

# ## Appendices

+   Web Appendix 2: more about bitmasks
+   Web Appendix 3: more netmask examples
+   Web Appendix 4: IP version 6
+   Inside back cover: decimal/binary, and hex conversion table