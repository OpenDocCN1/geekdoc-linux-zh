
2. The default setup for dhclient is fine for 99% of the situations that you're likely to encounter as a Unix system administrator. The program has a variety of options that can be specified in the ifcfg file. These are alluded to in the following fragment of the important /sbin/ifup script, which brings up a specified interface:

```
if [ -n "${DYNCONFIG}" ]; then
PUMPARGS=$PUMPARGS
DHCPDARGS="${DHCPDARGS} -n"
if [ -n "${DHCP_HOSTNAME}" ]; then
PUMPARGS="${PUMPARGS} -h ${DHCP_HOSTNAME}"
DHCPDARGS="${DHCPDARGS} -h ${DHCP_HOSTNAME}"
fi
if [ -n "${NEEDHOSTNAME}" ]; then
PUMPARGS="${PUMPARGS} -lookup-hostname"
DHCPDARGS="${DHCPDARGS} -H"
fi
if [ "${PEERDNS}" = "no" ]; then
PUMPARGS="${PUMPARGS} -d"
DHCPDARGS="${DHCPDARGS} -R"
fi
```

If you ignore the pump options (pump is an older alternative to dhclient in Linux, and most sites ignore it except for historical reasons), you can see that the arguments given to dhclient are the initial value of DHCPDARGS plus -n, -h dhcp hostname if specified as DHCP_HOSTNAME, -H if the system hostname should be set by the DHCP server (controlled by the presence of NEEDHOSTNAME in the config file), and -R if the existing /etc/resolv.conf DNS server list file should not be replaced by the information given by the DHCP server.

That's a bit confusing, so let's look again at the stock DHCP configuration. The variables that can affect how dhclient is invoked are DHCP_HOSTNAME, NEEDHOSTNAME, and PEERDNS. You'll notice that in /etc/sysconfig/network-scripts/ifcfg-eth0 the variable PEERDNS is set to "no," but the others are not referenced. This means that dhclient is invoked as

dhclient -n -R

which, as expected, prevents dhclient from overwriting the /etc/resolv.conf file, but otherwise assumes that the system is properly set up with its correct hostname.

That's the -R flag explained. What about the -n that's used regardless of configuration? Well, recall that DHCP is the Dynamic Host Configuration Protocol. One subtle ramification of the "dynamic" part of this is that while a DHCP server will assign an IP address to a specific workstation on request, it doesn't guarantee that IP address will stick with that workstation forever. Instead, systems are given a lease on their DHCP information, and have to renew the lease (for example, confirm that they're still up and online) with the DHCP server every so often. It’s a lease renewal that is triggered by the -n flag to dhcpc; though if the system is just starting up from scratch a renewal will have the effect of requesting a new IP address.

The internals of the DHCP protocol are quite interesting, but a bit beyond the focus of this particular book. If you’d like to learn more, a great place to start is at the Internet Software Consortium, where they also have a good alternative DHCP client protocol implementation that’s freely available: http://www.isc.org/products/DHCP/.

3. To see what information the DHCP server has handed the client program, peek at the information file in /etc/dhcpc:

```
# cd /etc/dhcpc
# ls
dhcpc-eth0.cache  dhcpc-eth0.info
# cat *info
IPADDR=192.168.131.67
NETMASK=255.255.255.0
NETWORK=192.168.131.0
BROADCAST=192.168.131.255
GATEWAY=192.168.131.254
DNS=192.216.138.10
DHCP_SID=192.168.131.254
DHCP_GIADDR=0.0.0.0
DHCP_SIADDR=0.0.0.0
DHCP_CHADDR=00:03:FF:FF:FF:FC
DHCP_SHADDR=00:03:FF:FF:FF:FF
DHCP_SNAME=
LEASETIME=4294987295
RENEWALTIME=536870911
REBINDTIME=536878911
```

The time values are in seconds since January 1, 1970, and you can see by the significant difference between LEASETIME and RENEWALTIME that this particular DHCP server hands out (virtual) IP addresses until a point far into the future, without any renewal of lease required. Many DHCP configurations will differ in this regard, and it’s a policy setting accessible within the DHCP server itself.

![](img/5ced0c78d748bd190e9027e5549a3622_347_0.png)

> The time value of seconds-since January 1, 1970 is a typical Unix-ism, but not one you can count on definitively. Each Unix flavor has the option of defining its own “epoch” for the seconds-since date format. Check your ctime(3) man page for a likely spot where it’s defined for your OS.

4. By contrast with the DHCP client, consider the same two configuration files on a Linux system with fixed IP addresses, on a completely different network:

```
# cd /etc/sysconfig
# cat network
NETWORKING=yes
HOSTNAME=staging.intuitive.com
# cat network-scripts/ifcfg-eth0
DEVICE=eth0
BOOTPROTO=static
ONBOOT=yes
IPADDR=10.10.2.200
GATEWAY=10.10.2.1
TYPE=Ethernet
USERCTL=no
NETMASK=255.255.255.0
NETWORK=10.10.2.0
BROADCAST=10.10.2.255
PEERDNS=no
```

Clearly, having a fixed IP address requires that other information be included, so let's spend a few minutes talking about the different values required and how to calculate them.

The first value is the IP address itself, of course, and that should be easy to ascertain based on your network. If you're using fixed IPs, you have a block of them and should have a master allocation table (perhaps just a sheet of paper in your desk drawer—a not-uncommon solution) that has IP address and host pairs for each of the IP addresses in the block. Those that haven't yet been assigned are blank and available.

In our office, we have a nonadjacent block of five IP addresses, one of which is used by the gateway itself, so our IP allocation table looks like Table 17.1.

### Table 17.1 Typical Fixed IP Allocation Table

| IP Address | Assigned To |
|---|---|
| 198.76.82.129 | Gateway |
| 198.76.82.131 | Laptop |
| 198.76.82.132 | G4 Mac |
| 198.76.82.150 | Win2K and iMac (shared, ugh!) |
| 198.76.82.151 | HP LAN printer |

As you can see, we have fewer IP addresses than we need, which is why the PC and iMac system are sharing one IP. This is not a good configuration¹. The solution is for us to set up one of the systems as a DHCP server, but we'll get to that a bit later in this hour.

In total, our ISP gave us the following information when we first gained network connectivity, as shown in Table 17.2.

### Table 17.2 Information from our ISP

| Field Name | Value |
|---|---|
| IP Range | 198.76.82.131, 132, 150, 151 |
| Gateway | 198.76.82.129 |
| Subnet Mask | 255.255.255.128 |
| DNS Servers | 192.216.138.10 and .11 |

> By convention, if you see two IP addresses and the latter only has a single value prefaced by a dot, it means that the first three "octets" are the same, so the two DNS servers are 192.216.138.10 and 192.216.138.11.

These values can be directly dropped into the /etc/sysconfig/network-scripts/ifcfg-eth0 file as IPADDR, GATEWAY, and NETMASK. In the earlier example, the values differed because that particular Linux server is on a different network (just in case you're trying to puzzle out why they're different values).

So where do NETWORK and BROADCAST come from? Unless you've been given specific values by your connectivity provider, most often those values are simply the first three octets of the IP address with a trailing 0 or 255. In the case of the configuration details given by our ISP, we'd specify a NETWORK=198.76.82.0 and a BROADCAST=198.76.82.255.

The only other file to create is /etc/resolv.conf, a list of the DNS servers available to the system. The format is quite straightforward:

```
# cat /etc/resolv.conf
dns1.dsldesigns.net 192.216.138.10
dns2.dsldesigns.net 192.216.138.11
```

You can add as many name servers as you'd like to this file, and if you opt to have a DNS cache server (a topic we'll discuss in depth in Hour 18, "Running Your Own Name Server"), you'd add the IP address of the cache server here as well.

²Among other things, this means that they can't both be on the Internet at the same time, a situation that often causes frustration in our office!

5. Whether your network uses DHCP or fixed IP, this should be sufficient information to get things properly configured and on the network. To actually bring the system online, you can reboot (usually the preferred strategy), or you can use the ifup or init.d/network scripts.

I prefer using the init.d/network script because it allows status queries, too:

```
# ./network status
Configured devices:
lo eth0
Currently active devices:
eth0 lo
```

More importantly, you can easily restart all the networking services on a Red Hat Linux system with a single command:

```
# ./network restart
Shutting down interface eth0:      [ OK ]
Setting network parameters:      [ OK ]
Bringing up interface lo:         [ OK ]
Bringing up interface eth0:       [ OK ]
```

If you'd prefer working with just the Ethernet interface and not touching the loopback mechanism (lo), you can use the ifup and ifdown commands in /sbin:

```
# /sbin/ifdown eth0
# /sbin/ifup eth0
Determining IP information for eth0... done.
#
```

Typically, bringing down the interface has no output, and bringing up the interface offers only minimal feedback on success.

6. Another common task in the DHCP world is to set up a DHCP server. Although there are many nuances to this task, the basics are easy to explain. The DHCP server daemon is called dhcpd, probably the most confusing part of configuring the service.

The configuration for dhcpd is stored in /etc/dhcpd.conf:

```
# cat /etc/dhcpd.conf
subnet 199.76.82.0 netmask 255.255.255.128 {
option routers 198.76.82.129;
option subnet-mask 255.255.255.128;
option domain-name "intuitive.com";
option domain-name-servers dns1.dsldesigns.net, dns2.dsldesigns.net;

option time-offset -8;   # Pacific Standard Time

host imac {
option host-name "imac.intuitive.com";
```
