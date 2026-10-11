```
```
dhcp-range=192.168.100.25,192.168.100.50,2h

dhcp-host=52:54:00:57:d0:9f,192.168.100.222

dhcp-option=option:router,192.168.100.1

dhcp-option=option:dns-server,1.1.1.1
```
```

Once the service is started, the log will appear in the journalctl when a request is received. The following excerpt shows the IP assignment for the host configured with a specific IP:

```
```
ubuntu dnsmasq-dhcp[1889]: DHCPDISCOVER(enp8s0) 192.168.100.222
52:54:00:57:d0:9f
ubuntu dnsmasq-dhcp[1889]: DHCPOFFER(enp8s0) 192.168.100.222
52:54:00:57:d0:9f
ubuntu dnsmasq-dhcp[1889]: DHCPREQUEST(enp8s0) 192.168.100.222
52:54:00:57:d0:9f
ubuntu dnsmasq-dhcp[1889]: DHCPACK(enp8s0) 192.168.100.222
52:54:00:57:d0:9f
```
```

The file containing the leases for dnsmasq is /var/lib/misc/dnsmasq.leases.

# DNS service and clients

The Domain Name System (DNS) is a service to convert domain names to IP addresses and vice versa. The structure is based on a hierarchy, where the top level contains the root nameservers. Currently, these root nameservers are 13 servers geolocated in different parts of the world. These servers have the syntax letter.root-servers.org, where the letter currently is going from the letters a to m. The first query to the root nameservers is to obtain the servers for the top-level domain (TLD), responsible for the second level in the hierarchy. These servers are associated with the top-level domain, such as .com, .net, and .org, the country code TLDs (for example, .in, .es, and .jp), and new TLDs (for example, .tech and .space). These top-level domain servers would provide the domain servers for the domain specified. These domains are responsible to provide the answer for the domain or subdomain queried. DNS can contain complex configurations indicating other nameservers for subdomains. Figure 9.7 shows the hierarchy with two domain examples: