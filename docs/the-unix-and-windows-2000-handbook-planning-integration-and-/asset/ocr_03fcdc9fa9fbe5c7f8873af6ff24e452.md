```text
10000010.11001111.11101001.X        (130.207.233)
11111111.11111111.11111111.00000000
00000000.00000000.00000001.X
```

> Incorrect subnet masks are a common mistake that is difficult to debug. If you are experiencing strange and unexplained network problems on a system, always make sure to check the subnet masks.

Make sure you have the correct subnet mask for your network. Never assume that your network uses a common netmask like `255.255.255.0` (or a fully subnetted class B network). Using the work subnet mask can cause unexpected results, and while your system may be able to perform some operations on the network, if you don't identify the netmask as the problem, you may spend hours looking for problems in other areas.

# DOMAIN NAME

Your domain name is simply the extension that, when concatenated with the hostname, gives you the fully-qualified system name. For instance, if your system is `rover.yourdomain.edu`, then your domain is `your-domain.edu`. This is important for DNS and NIS+.

> Do not confuse this with your NIS+ domain name and the output of the `domainname` command.

# DOMAIN NAME SERVERS

If you plan to use DNS to resolve hostnames, you'll need to know the proper name servers to put into your `/etc/resolv.conf`. This file defines the servers and the order in which they should be contacted.

```
```text
mars:> cat /etc/resolv.conf

domain yourdomain.edu

nameserver 192.168.3.49

nameserver 192.168.3.74
```
```