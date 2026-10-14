although any member of the cluster may take over this responsibility if the current master fails or is removed from the cluster.

When a new proxy ARP master is selected, the MAC address that will be sent back in the case of an ARP request from a network client will be different than it was prior to the proxy master change. The clients will not send out an ARP request if the IP address to MAC translation is already present in the client's ARP cache. The ARP cache of a client can potentially be holding the wrong MAC address for the ~20 minutes it takes for the ARP cache to decay. Therefore, a client could be sending datagrams to a non-existent MAC address for a relatively long time before it figures out that the MAC information in its cache is incorrect (see Figure 16-2). Not a good thing.

# 16.4.1 Gratuitous ARP

The cluster software tries to compensate for this by sending out a gratuitous ARP broadcast to inform all network nodes that they need to replace an entry in their ARP cache. This eliminates the potential havoc caused by the client ARP cache being behind the times.

The following example illustrates gratuitous ARP. All output is generated from a client node. Note how the hardware address associated with babylon5 changes as the current proxy ARP server in the cluster is shutdown.

Note that cluster member sheridan's tu0 interface MAC address ends in “3a:29”, while cluster member molari's tu0 interface MAC address ends in “12:31”.

```
```text
# rsh sheridan /usr/sbin/netstat -i tu0
Name  Mtu  Network       Address          Ipkts  Ierrs  Opkts  Oerrs  Coll
tu0   1500 <Link>        00:10:64:30:3a:29  452512  0  267120  2  0
tu0   1500 DLI           none              452512  0  267120  2  0
tu0   1500 192.168.0    sheridan          452512  0  267120  2  0
```
```

![](bbox=[0.212, 0.624, 0.781, 0.881])

Figure 16-2: Gratuitous ARP Ignored or Denied