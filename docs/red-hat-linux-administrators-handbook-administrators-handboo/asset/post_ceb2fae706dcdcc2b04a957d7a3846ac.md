
### Listing 7-4 The /etc/sysconfig/network File
```
NETWORKING=yes
FORWARD_IPV4=yes
HOSTNAME=gateway.nitec.com
DOMAINNAME=nitec.com
```

The most important setting here is FORWARD_IPV4=yes, which enables IP forwarding in the kernel.

![](img/c2419364ebb911c809b6a79991707c27_181_0.png)

### Tip
You must have IP forwarding support built into the kernel. You can use the cat /proc/sys/net/ipv4/ip_forward command to see whether IP forwarding is enabled in a running kernel. If the output is 1, then IP forwarding is set; a value of 0 signifies that IP forwarding is turned off. You can also turn it on or off by inserting a value of 1 or 0 using the echo n > /proc/sys/net/ipv4/ip_forward command, where n is either 1 or 0.

Listings 7-5 and 7-6 show the two interface (eth0 and eth1) files.

### Listing 7-5 The /etc/sysconfig/network-scripts/ifcfg-eth0 File
```
DEVICE=eth0
IPADDR=192.168.1.126
NETMASK=255.255.255.128
NETWORK=192.168.1.0
BROADCAST=192.168.1.127
ONBOOT=yes
```

### Listing 7-6 The /etc/sysconfig/network-scripts/ifcfg-eth1 File
```
DEVICE=eth1
IPADDR=192.168.1.254
NETMASK=255.255.255.128
NETWORK=192.168.1.128
BROADCAST=192.168.1.255
ONBOOT=yes
```

After these files are set and the interfaces are up and running (either via a reboot or by using the ifup command), you need to create two default routes for the two networks, using the following route commands:

```
route add -net 192.168.1.0 255.255.255.128 eth0
route add -net 192.168.1.128 255.255.255.128 eth1
```

Each of the preceding route commands makes sure that packets destined for the named network are transmitted via the named interface device.

### Host computer configuration
Each host computer on each of the subnets has to be configured so that each computer knows the network address, local subnet mask, and the gateway information. For example, assuming that all the host computers are also Linux workstations and each has a single Ethernet interface device (eth0), the /etc/sysconfig/network file on any of the host computers on the 192.168.1.0 network is shown in Listing 7-7.

### Listing 7-7 The /etc/sysconfig/network File
```
NETWORKING=yes
FORWARD_IPV4=yes
HOSTNAME=marketing-1.nitec.com
DOMAINNAME=nitec.com
GATEWAY=192.168.1.126
GATEWAYDEV=eth0
```

The interface file on this same computer will look like the example shown in Listing 7-8.

### Listing 7-8 The /etc/sysconfig/network-scripts/ifcfg-eth0 File
```
DEVICE=eth0
IPADDR=192.168.1.1
NETMASK=255.255.255.128
NETWORK=192.168.1.0
BROADCAST=192.168.1.127
ONBOOT=yes
```

In a similar fashion, the computers in the 192.168.1.128 network need to be set up. Each of the computers in this network will use the GATEWAY=192.168.1.254 line in the /etc/sysconfig/network file and use NETWORK=192.168.1.128 and BROADCAST=192.168.1.255 in their `/etc/sysconfig/network-scripts/ifcfg-eth0` files.

Of course, if any of these computers are non-Linux systems, such as Windows 9x/2000, you have to use the appropriate network configuration tool to set these values.

After you set up the gateway computer and at least one host in each network, you are ready to test the subnets. The easiest way to test is to use the ping program. Here are some simple test and troubleshooting guidelines,

- 1. Use the ping program to ping a host computer in the same subnet. For example, run `ping 192.168.1.2` from the 192.168.1.1 computer. If you do not get ping replies, check the network configuration files (`/etc/sysconfig/network` and `/etc/sysconfig/network-scripts/ifcfg-eth0`). Correct any problem you notice and restart the interface by first taking it down using `ifconfig eth0 down` and then bringing it up using `/etc/sysconfig/network-scripts/ifup eth0`. After you are able to ping a host in the same subnet, proceed to the next step.
- 2. Ping the gateway computer from each subnet. If you cannot perform this operation, check the gateway computer's network configuration files and correct any errors or typos. After you are able to ping the gateway computer from each subnet, proceed to the next step.
- 3. Try to ping a host in the other subnet. If you can't ping the host in the other subnet, try using `traceroute IP address` to determine whether the packets are even making it to the gateway machine. If traceroute shows that the packets are making it to the gateway but not being forwarded to the destination, the problem is at the gateway. You should ensure that IP forwarding is turned on for the computer. Run `cat /proc/sys/net/ipv4/ip_forward` on the gateway computer to see whether the returned value is 1 or 0. If it is not 1, IP forwarding is either turned off in the `/etc/sysconfig/network` file or not enabled in the kernel. In such a case, fix this problem and retry.

At this point, you should be able to send ping requests from any of the two subnets. If you can, then you have two working subnets.

## Chapter 8
### DNS Service
### Configuring a DNS Client (Resolver)
Typically, the Red Hat installation program asks you about your DNS server and automatically configures the necessary resolver configuration file. However, it is often necessary to change the resolver configuration to reflect any changes to the DNS server you use. For example, if you configure your resolver during Red Hat installation and later change ISPs, you need to manually configure it again. Here is how.

If you plan to use your ISP's DNS server to resolve names and IP addresses, ask your ISP to give you the host name and the IP address of its DNS servers. After you have the required information, you can configure the resolver as follows:

- 1. First, you need to modify the resolver configuration file called `/etc/resolv.conf`. Listing 8-1 shows a typical `/etc/resolv.conf` file for a domain called nitec.com.

### Listing 8-1 The Resolver Configuration File /etc/resolv.conf
```
# Default Domain
domain nitec.com

# Default search list
search nitec.com

# First name server
```

### Listing 8-1 Continued
```
nameserver 206.171.50.50
# Second name server
nameserver 206.171.50.55
```

2. Set the Domain directive to the domain name for your system. If you do not have this line set to the domain name of your system, the default domain name is automatically extracted from the fully qualified host name of your system.

3. Set the Search directive to the domain name of your system. This directive is used to influence how the resolver searches for host names that are not fully qualified. For example, if you want to enter the ping www command in a shell on the system with the preceding resolver configuration file, the ping program will use the resolver to resolve www. Because www is a partial host name, the resolver creates a full host name by using the search list (for instance, www.nitec.com) and tries to resolve an IP for that host. For example, if you set the search directive to integrationlogic.com in the preceding listing and make the same ping request, the resolver returns the IP address for www.integrationlogic.com. If you do not provide a search directive, the default domain name is automatically applied when partial host names need to be resolved.

4. Set the Nameserver directive to the DNS server that the resolver should use to perform DNS queries. You can (and should) specify multiple nameserver directives in the configuration file. Each domain name server is queried in order of appearance in the configuration file. For example, if a program requests the resolver to resolve a host name called www.ad-engine.com, the resolver first tries to resolve the name to an IP using the 206.171.50.50 domain name server. If the 206.171.50.50 domain name server fails to return a response (that is, if the query times out), then the second domain name server, 206.171.50.55, is contacted. Currently, you are allowed to list only three nameserver directives in the configuration file. It is generally a good idea to have at least two nameserver directives set to two different name servers.
