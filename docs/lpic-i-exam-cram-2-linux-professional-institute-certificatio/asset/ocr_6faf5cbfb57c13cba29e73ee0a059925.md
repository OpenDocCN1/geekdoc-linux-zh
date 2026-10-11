A good example of viewing the ARP cache information is
arp -a

Here is the output:
(192.168.1.2) at 00:40:CA:38:DB:0B [ether] on eth0
(192.168.1.1) at 00:04:5A:D0:C5:CD [ether] on eth0
(192.168.1.103) at 00:0B:74:E3:E5:9D [ether] on eth0

In the previous example, the IP is shown because it's included in the packets on the network, but it can be shown as the remote host's name if it's resolvable either through the /etc/hosts or DNS or NIS sources. This is automatically done if DNS is configured properly for the hosts involved.

The at 00:... section shows the MAC of the remote host, followed by the type (ether) and the actual interface (eth0) used.

> If the remote host is not on the same logical subnet or network, the entries shown might not match what you think you've pinged or connected to. For example, if a remote host is reached through a gateway and you look at the ARP table, you'll see only the gateway address listed, not the remote address.

Finally, if you need to, a static entry that will never time out can be set in the ARP cache. This might be a good idea for the default gateway or a server that is accessed constantly and is not going to change its IP or NIC device anytime soon.

For example, say your ARP cache entry for a gateway device presently shows the following:
(192.168.1.1) at 00:04:5A:D0:C5:CD [ether] on eth0

You can therefore set that device to always be in the ARP cache with that exact match between the IP and MAC addresses with this command:
arp -s 192.168.1.1 00:04:5A:D0:C5:CD

Check the entry again with this command:
arp -a 192.168.1.1

Typical output would be
(192.168.1.1) at 00:04:5A:D0:C5:CD [ether] PERM on eth0

The entry is in the ARP cache until it's unconfigured with this command:
arp -d 192.168.1.1