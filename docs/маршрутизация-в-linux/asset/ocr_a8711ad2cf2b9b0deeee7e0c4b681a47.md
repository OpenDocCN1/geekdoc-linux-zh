# -d Host

Sometimes it is necessary to delete the arp entry of a host to troubleshoot networking problems where address resolution is not working correctly, such as when two nodes are misconfigured with the same IP address or where a network interface card might seem to be misbehaving. The -d entry can be used to remove specific entries. The -d is followed by the host, which can be the IP address or the hostname of the node. To remove speedy’s MAC address from the arp cache, the following is typed:

```
[root@lefty /root]# arp -d speedy
```

And to see that it has been removed:

```
[root@lefty /root]# arp
Address          HWtype  HWaddress       Flags Mask Iface
192.168.1.1      ether   00:20:78:CF:30:66 C       eth0
```

Oftentimes when troubleshooting ARP-related problems, there is a need to clear the complete ARP cache. The following script, darpcache, uses the -d parameter to parse through the cache and remove all entries:

```
#!/bin/bash
# darpcache
# This script deletes all arp entries from the arp cache

for host in `arp -n | awk '{print $1}' | grep -v Address`
do
    echo "Deleted entry for host: $host"
    arp -d $host*
done
```

It’s output looks similar to this:

```
[root@lefty /root]# ./darpcache
Deleted entry for host: 192.168.1.1
Deleted entry for host: 192.168.1.101
```

A related protocol, RARP, works similarly to ARP; however, its purpose is to allow a host to determine its IP address by broadcasting its MAC address as an RARP request. A node then responds with the mapped IP address. The RARP protocol has all but been replaced with dynamic host control protocol (DHCP) for several reasons, including RARP’s tendency to be statically mapped on a particular node and DHCP’s ability to provide additional information beyond the IP address (including DNS configuration like name servers and domain suffixes). DHCP is also widely supported on non-UNIX systems.

RARP support must be configured in the Linux kernel, and the RARP table is managed using the rarp command.

# traceroute

traceroute is likely only second to the ping command as the most often used network troubleshooting tool. traceroute shows the path between the source (the Linux node where the command is executed) and the destination.