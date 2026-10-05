# 496 CHAPTER 12 FILES, DIRECTORIES, AND FILESYSTEMS

/etc/init.d Holds SysVinit initialization scripts. See page 440 for more information.

/etc/resolv.conf The resolver (page 824) configuration file, which is used to access DNS. By default, this file is rebuilt by resolvconf when you run the bind9 init script. “named options” on page 834, “resolconf and resolv.conf” on page 835, and the resolver and resolv.conf man pages for more information.

The following example shows the resolv.conf file for the example domain. resolv.conf file usually contains at two lines—a search line (optional) and a nameserver line:

```
# /etc/resolv.conf
search example.com
nameserver 10.0.0.50
nameserver 10.0.0.51
```

The search keyword may be followed by a maximum of six domain names. The first domain name is interpreted one at a time to all DNS queries, shortening the time needed to query local hosts. The domains are searched in order of the process of resolving hosts that are not fully qualified. See FQDN on page 1149.

When you search example.com in resolv.conf, any reference to a host within the example.com domain or a subdomain (such as marketing.example.com) can use the abbreviated form of the host. For example, instead of using the command speedy.marketing.example.com, you can use speedy.marketing.com. The following line in resolv.conf causes the marketing subdomain to be searched first, followed by sales, and finally the entire example domain:

```
search marketing.example.com samples.example.com
```

It is a good idea to put the most frequently used domain names first to try outguess possible conflicts. If both speedy.marketing.example.com and speedy.example.com exist, the order of the search determines which one is selected when you invoke DNS. The longer the search, the more work DNS requests generated, and the slower the response. Three or four names are typically sufficient.

The nameserver line(s) indicate which systems the local system should query to resolve hosts to IP addresses, and vice versa. These machines are consulted in the order they appear, with a timeout between queries. The first timeout is a few seconds; each subsequent timeout is twice as long as the previous. The preceding file sets this system to 10.0.0.50, followed by 10.0.0.51 when the first system does not answer within a few seconds. The resolv.conf file may be automatically updated when a PPP (Point-to-Point Protocol) or DHCP (Dynamic Host Configuration Protocol) controlled interface is activated. Refer to the resolv.conf and man pages for more information.

/etc/rpc Maps RPC services to RPC numbers. The three columns in this file show the name of the server for the RPC program, the RPC number, and any aliases.