# Chapter 17: Network Configuration

This document covers TCP/IP networking, network administration and system configuration basics. Linux can support multiple network devices. The device names are numbered and begin at zero and count upwards. For example, a computer with two NICs will have two devices labeled eth0 and eth1.

# Section 17.1: Local DNS resolution

File: */etc/hosts* contains a list of hosts that are to be resolved locally(not by DNS)

Sample contents of the file:

```
127.0.0.1       your-node-name.your-domain.com  localhost.localdomain  localhost
XXX.XXX.XXX.XXX node-name
```

The file format for the hosts file is specified by RFC 952

# Section 17.2: Configure DNS servers for domain name resolution

File: */etc/resolv.conf* contains a list of DNS servers for domain name resolution

Sample contents of the file:

```
nameserver 8.8.8.8 # IP address of the primary name server
nameserver 8.8.4.4 # IP address of the secondary name server
```

In case internal DNS server you can validate if this server resolve DNS names properly using `dig` command:

```
$ dig google.com @your.dns.server.com +short
```

# Section 17.3: See and manipulate routes

Manipulate the IP routing table using `route`

# Display routing table

```
$ route # Displays list or routes and also resolves host names
$ route -n # Displays list of routes without resolving host names for faster results
```

# Add/Delete route

| Option | Description |
|:--- |:--- |
| add or del | Add or delete a route |
| -host x.x.x.x | Add route to a single host identified by the IP address |
| -net x.x.x.x | Add route to a network identified by the network address |
| gw x.x.x.x | Specify the network gateway |
| netmask x.x.x.x | Specify the network netmask |
| default | Add a default route |

Examples: