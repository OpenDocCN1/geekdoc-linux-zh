
## 352 Chapter 17 IP Multicast for Group Communication

unresolved is used for entries in the multicast forwarding cache; the multicast routing daemon has not yet finalized the routing selection. The entry for the mfc_cache structure is created in the MFC as a packet arrives.

unresolved is a queue for socket buffers that stores packets for this routing until the multicast routing daemon has selected a route.

expires is the time by which the daemon should have selected a route.

res is used in the mfc union when the multicast routing daemon has specified the routes for this entry.

minvf and maxvif are indices to elements in the ttl1 list of the MFC entry. They limit the range currently used by virtual network devices which are used to send packets of this MFC entry. Stating this index saves computing time required to duplicate multicast packets. The maxvif index is limited by the MAXVIFS constant.

ttl1 is an array with MAXVIFS entries where each entry specifies whether a packet should be forwarded over the virtual network device in the vif_table list with the corresponding index. This is the case when a value less than 255 exists. The value 0 cannot occur, because it is mapped to the value 255 when the table is built. However, an entry less than 255 is not sufficient for forwarding a packet; the TTL value of a packet has to be at least equal to the TTL value in the ttl1 array. The method used to create the threshold value for multicast packets is described in Section 17.2.3.

**Paths of a Multicast Packet Through the Linux Kernel** Figure 17–13 shows the paths a multicast packet can take to travel through the Linux kernel. Like any other IP packet.

![](img/5a25b942ec3329b8799f2b5f0de564f6_375_0.png)

FIGURE 17–13 Overview of how a multicast packet can travel through the Linux kernel.

## 17.4 Multicast Data Path in the Linux Kernel 353

a multicast packet is received by ip_recv(). The routing cache is normally as for other packet-forwarding instructions in ip_route_input() (see Chapter 16), and multicast packets are no exception. In the case of an end system, ip_check_mc() checks on whether the multicast group is required in the computer all. This means that undesired multicast packets (i.e., packets passed upwards by the network card, either because of an unclear mapping of IP addresses to MAC addresses, or because of an adapter without hardware filter, or by the promiscuous mode) are discarded. If a socket drops it, the flag RTF_LOCAL is attached to the packet at this point. In general, the flag RTF_MULTICAST is also set in multicast packets.

If the packet is cached (i.e., if the group is desired or the station is a multicast router, which accepts all packets), then the multicast packet continues its path in ip_route_input_mc(), where paths go in different directions depending on whether the station is an end system or a multicast router. In end systems, local packets are passed to the function ip_local_deliver(), which forwards to the application layer.

In multicast routers, all packets (including local packets) are first handled by ip_mr_input(). The most important task of this function is to use ipmr_cache_find() to find the entry in the MFC. Local packets are passed to ip_local_deliver(), and packets with other destinations are transported to ip_mr_forward() where they will eventually be replicated. The details of each of these functions are described next.

```
ip_route_input_mc()                               net/ipv4/route.c
```

ip_route_input() invokes ip_route_input_mc(skb, daddr, saddr, tos, dev,) if the incoming packet is a multicast packet. First, the function checks the source and destination addresses (saddr, daddr) and returns an error, if present. Also, packets originating from the same computer should not arrive over this input route for several reasons, including protection against spoofing. Once the source address has been checked in the forwarding information base, memory space is allocated for a new route in the routing cache. The route is entered in the cache, and the flag RTF_MULTICAST is added. Subsequently, the packet is handled in ip_local_deliver() (for end systems) or ip_mr_input() (for multicast routers), and the computed hash is returned.

```
ip_mr_input()                                       net/ipv4/ipmr.c
```

ip_recv_finish() invokes ip_mr_input(skb) by the function dst->input(), which is set to ip_route_input_mc(), if the computer was configured as a multicast router. The first thing to be checked is whether the packet is an IGMP packet for the multicast daemon. If so, the packet is delivered to this daemon over the raw socket. Subsequently, the function ipmr_cache_find finds the multicast forwarding cache for a matching entry for the cache. If no matching entry can be found, then a local packet (RTF_LOCAL) is passed to ip_local_deliver(), and packets that have to be forwarded to the queue for incomplete entries (unresolved queue in the mfc_cache structure). As soon as the routing daemon has determined the route, these packets are forwarded by ip_mr_forward(). If a valid entry was found in the multicast forwarding cache, then ip_mr_input() passes a pointer to this routing entry to the function ip_mr_forward, which duplicates and forwards the packet. Finally, packets marked local (RTF_LOCAL) are passed upwards by ip_local_deliver.

```
ip_mr_forward()                                     net/ipv4/ipmr.c
```

ipmr_cache_find(origin, mgrp) searches the multicast forwarding cache (see above) for a specific entry. The source address of the packet and the multicast group address together are used as search key. An MFC entry found includes all virtual network devices (VIFs), which should be used to forward packets. The result is returned in an mfc_cache structure (see above).

```
ip_mr_forward()                                     net/ipv4/ipmr.c
```

ip_mr_input(skb, cache, local) obtains the mfc pointer from ip_mr_input(). points to the entry of the skb in the multicast forwarding cache and then duplicates the packet for each virtual network device that should be used to forward:

for (ct = cache->mfc_un.res.maxvif-1; ct >= cache->mfc_un.res.minvif; ct--)
{
  if (skb->iph->ttl > cache->mfc_un.res.ttl[ct])
  {
    if (psend != -1)
      ipmr_queue_xmit(skb, cache, psend, 0);
    psend = ct;
  }
}

The actual replication of multicast packets is done in the loop, which checks all array entries in the ttl field of the mfc_structure from maxvif-1 to minvif. However, the copies of socket buffers are not directly created by ip_mr_forward(). They are created later by the function ipmr_queue_xmit(), which is invoked if the multicast packet has sufficient lifetime (TTL) to be sent over the current network device. It passes the entire mfc_structure and an index to each VIF that should receive the packet to ipmr_queue_xmit for each VIF.

Before a packet is replicated, ip_mr_forward() checks on whether the packet arrived in the expected network device and whether it was discarded, if applicable. Reason for this check will be discussed in Section 17.5.3. A conflict situation occurs if a computer acts as multicast router and runs multicast applications at the same time. If multicast packets are transported across the loopback network device, then the input network device can deviate from the default multicast route for these packets, and these packets will be discarded.

```
ipmr_queue_xmit()                                    net/ipv4/ipmr.c
```

ip_mr_forward invokes ipmr_queue_xmit(skb, mfc, vifi, last) to transmit multicast packet skb. If the packet is not exclusively available (for example, because there are several references to the packet payload (cloned), or if the packet is not the last of all replicas, then a clone of the socket buffer is created. In addition, a decision has be made for the packet as to whether it should be transported through a tunnel or through a regular network device. In either case, ip_route_output with the respective parameters invoked. For a tunneled packet, the variables local and remote from the pertaining VIF structure are passed; otherwise, the destination address from the socket's buffer is sufficient. In both cases, the variable link from the VIF structure passes an index to the relevant physical network device. Subsequently, the filter hook NF_IP_FORWARD is invoked. If it does not fragment, the packet is sent over the function pointer dst->output(); otherwise it is sent over ip_fragment(skb, dst->output).

## 17.5 MULTICASTING IN TODAY'S INTERNET

Multicasting was a thing unheard of at the advent of the Internet, and neither group addresses nor protocols to manage groups or multicast routing were available. In fact, the most important prerequisites for implementing an efficient group communication service were missing. The Internet was a pure unicast network.

Several proposals in this field were made [Deer99] when the Internet community had started to think that such a service was necessary, at the beginning of the nineties. Eventually, IP multicast was born when the Internet Group Management Protocol and the address class D were standardized. In addition, multicast routing protocols were proposed, so that nothing was actually introducing the new communication form. However, although the Internet had evolved into an enormous global network during the last twenty years, it was a unicast network, and gradually each system connected to the Internet would have to be extended.

### 17.5.1 The Multicast Backbone (MBone)

The Internet Engineering Task Force (IETF) ran a pilot session to officially introduce MBone in March 1992. Since then, more than 10,000 subnetworks have been connected to this network world. MBone enabled the connected-enhanced subnetworks to run IP multicast over the existing Internet.

The solution offered by MBone is relatively simple: It builds a virtual network over the conventional Internet, which understands only unicasting, and connected systems multicast-capable routers (multicast routers).
