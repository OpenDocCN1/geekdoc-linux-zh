# Network Configuration on Other Unixes

Before we go too far into the topic of other Unixes, please make sure that you didn’t skip the last section because you aren’t running Linux. There’s lots of information that we won’t repeat in this later section that you’ll want to know.

The good news is that the basic concepts of DHCP client configuration and fixed IP configuration are the same regardless of which flavor of Unix the system you’re configuring is running. The location of the specific configuration files—well, that’s going to vary a bit as you might expect, but if you can identify all the critical values to feed into the configuration, it’s not too bad.

# Task 17.2: Configuring Solaris and Mac OS X

![](bbox=[0.15, 0.42, 0.18, 0.6])

Considering that Sun Microsystems widely touts its vision of the world as “The Network is the Computer,” it would be reasonable to expect that configuring a Solaris system to be a full member of the Internet would be a breeze. Similarly, Apple has always had a significant advantage in how easily Mac OS lets you add systems to your network, an advantage that you would expect to translate into a straightforward configuration in the Mac OS X world.

And you’d be wrong in both cases.

+   1. To start out, the network configuration for a Solaris 8 system resides in a sprawl of different files, including /etc/resolv.conf, /etc/hostname.ifname, /etc/dhcp.ifname, /etc/nodename, /etc/inet/hosts, and more. Let’s step through them, one by one, to see what’s what:

```
# cat /etc/resolv.conf
search dsldesigns.net
nameserver 192.216.138.10
nameserver 192.216.138.11
```

No big surprises—this file is fairly typical of DNS name server lists. The first line is worth mentioning because it’s the primary spot where Solaris is told the domain name of the current system for DNS lookup purposes.

Trying to figure out where to drop the proper hostname for this system is a bit more confusing, as it’s located in two configuration files:

```
# ls /etc/hostname.*
/etc/hostname.pcno
# cat /etc/hostname.pcno
solaris.dsldesigns.net
# cat /etc/nodename
solaris.dsldesigns.net
```