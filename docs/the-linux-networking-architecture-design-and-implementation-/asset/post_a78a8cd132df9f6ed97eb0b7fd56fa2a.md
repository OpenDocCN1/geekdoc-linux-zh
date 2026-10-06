
## 14.2 Implementing the Internet Protocol

### Forwarding Packets
If a computer has several network adapters, and if packet forwarding is enabled (/proc/sys/net/ipv4/ip_forward 1), then packets addressed to other computers are handled by the ip_forward() function. This function does all the work necessary for forwarding a packet. The most important task—routing—was already done in ip_input(), because it is necessary to discover whether the packet is to be delivered locally or to be forwarded.

```
ip_forward() net/ipv4/ip_forward.c
```

The primary task of ip_forward(skb) is to process a few conditions of the Internet Protocol (e.g., a packet's lifetime) and packet options. Filters not marked with pkt_type = PACKET_HOST are deleted. Next, the reach of the packet is checked. If its value in TTL is 1 (before it is decremented), then the packet is deleted. RFC 791 specifies that, if such an action occurs, an ICMP packet has to be returned to the sender to inform the latter (ICMP_TIME_EXCEEDED). Once a redirect message has been checked, the socket buffer is checked to see if there is sufficient memory for the headroom. This means the function skb_cow(skb, headroom) is used to check whether there is sufficient space for the MAC header in the output network (outdev->header_len). If this is not the case, skb_alloc(headroom) creates sufficient space. Subsequently, the TTL header of the IP packet is decremented by one.

When the actual packet length (including the MAC header) is known, it is checked for whether it fits into the frame of the new output network device. If it is too long (skb->mtu), and no fragmentation is allowed the Don'Fragment bit is set in the IP header, the packet is discarded, and the ICMP message ICMP_FRAG_NEEDED is transmitted to the sender. In any case, the packet is not fragmented yet; fragmentation is delayed. The early test for such cases prevents Don'Fragment candidates from running through the entire IP protocol-handling process, only to be dropped eventually.

```
ip_forward_finish() net/ipv4/ip_forward.c
```

We can see in Figure 14–4 that the ip_forward() function is split into two parts by a netfilter hook. When the NF_IP_FORWARD hook has been processed, the procedure continues with ip_forward_finish(). This function actually has very little functionality (unless FASTROUTE is enabled). Once the IP options are, it has been processed in ip_forward_options(), the ip_send() function is invoked to check on whether the packet has to be fragmented and eventually to a fragmentation. (See Section 14.2.3).

```
ip_send() include/net/ip.h
```

ip_send(skb) decides whether the packet should be passed to ip_finish_output() immediately or if ip_fragment() should first adapt to the appropriate layer-2 frame size. (See Section 14.2.3.)

### ip_finish_output()

ip_finish_output(skb) initiates the last tasks of the Internet Protocol. First, the skb->dev pointer is set to the output network device dev, and the layer-2 packet type is set to ETH_P_IP. Subsequently, the netfilter hook NF_IP_POST_ROUTING is processed. The exact operation of netfilter and the set of different hooking points in the Internet Protocol are described in Section 19.3. It is common for netfilter hooks to continue with the inline function ip_finish_output2() after their invocation.

net/ipv4/ip_output.c

ip_finish_output2()

net/ipv4/ip_output.c

At this point, the packet leaves the Internet Protocol, and the Address Resolution Protocol (ARP) is used, if necessary. Chapter 15 describes the Address Resolution Protocol. For now, it is sufficient to understand the following:

- If the routing entry used (skb->dst) already includes a reference to the layer-2 header cache (dst->hh), then the layer-2 packet header is copied directly into the packet-data space of the socket header. The output() function used here is dev_queue_xmit(), which is invoked if the entry in the hardware header cache is valid. dev_queue_xmit() ensures that the socket is sent immediately over the network device dev.
- If there is no entry in the hard header cache yet, then the corresponding address resolution routing is invoked, which is normally the function neigh_resolve_output().

The procedure described above was optimized so that a packet can pass the router quickly without special options. However, it became clear that there are junctions to the corresponding handling routines (e.g., netfilter, multicasting, fragmentation, or IP packet options).

### Delivering Locally
The previous section describes the route packet travels when it has to be forwarded. If ip_route_input() is the selected route, then the packet is addressed to the local computer. In this case, branching is up to ip_local_deliver() rather than to ip forward(). This section describes the path of packets to be delivered locally.

At this point, instead of using a conditioned if instruction to distinguish the two options, a pointer (skb->dst->input()) is used, which points to ip_local_deliver() in this case. At the end of ip_input(), the procedure continues with the packet's local delivery.

ip_local_deliver()

net/ipv4/ip_input.c

The first (and only) task of ip_local_deliver(skb) is to reassemble fragmented packets, using ip_defrag(). Section 14.2.3 describes in detail how packets are fragmented and defragmented. For now, it is sufficient to understand that all fragments a packet collected over a certain period of time, until all fragments of an IP datap have arrived, so that they can be passed upwards as a whole.

Subsequently, it is almost mandatory to call a netfilter hook (NF_IP_LOCAL_IN) when the procedure continues with the ip_local_deliver_function().

```
ip_local_deliver_finish() net/ipv4/ip_input.c
```

The packet has now reached the end of the Internet Protocol processing. It is checked to see whether the packet is RAW-IP socket; otherwise, the transport protocol has to be determined for further processing (demultiplexing).

All transport protocols are managed in the ipport hash table on the IP layer in Linux. At the end of the IP processing, there is now a special structure, instead of simple structure. The complexity of the IP options necessitates more complex methods. The protocol ID of IP header (MAX_INET_PROT) is used to calculate the hash value. If the transport protocol is found, the appropriate handling routine (handler) is invoked. The following are:

- tcp_rcv(): Transmission Control Protocol (TCP)
- udp_rcv(): Datagram Protocol (UDP)
- icmp_rcv(): Internet Message Protocol (ICMP)
- igmp_rcv(): Internet Group Protocol (IGMP)

If no transport protocol can be found, the packet either is passed to a RAW socket (if there is one) or it is dropped and an ICMP Destination Unreachable message is returned to the sender.

The chapters dealing with TCP and UDP transport protocols describe how a packet is further handled. Chapter 17 describes IGMP, and ICMP packets are discussed in Section 14.4. The following section describes the path a packet takes as it passes from the transport layer to the Internet Protocol.

### 14.2 Transport-Layer Packets

This section considers only the ip_queue_xmit() function, because this is the one normally used for data packets; ip_build_and_send_pkt() is used for SYN or ACK packets that do not transport payload.

img/5a25b942ec3329b8799f2b5f0de564f6_263_0.png
FIGURE 14–5 Hash table used to multiplex transport protocols.

### ip_queue_xmit()

net/ipv4/ip_output.c

At the beginning, ip_queue_xmit(skb) checks for whether the socket structure sk->dst points to an entry in the routing cache and, if so, whether this pointer is actually valid. The route for a packet is stored in the skb->sk socket structure, because all packets of a socket go to the same destination. Storing a reference means that expensive searches for routes can be avoided.

If no route is present yet (e.g., when the first packet of a socket is ready), then the ip_route_output() function is used to choose a route. Once this route has been entered in the routing cache, its use counter is incremented to ensure that the route is not inadvertently deleted as there is still a socket buffer referencing it.

Subsequently, the fields of the IP packet are filled (version, header length, TOS field, fragment offset, TTL, addresses, and protocol). Next, ip_options_build() handles options, prefix, and the netfilter hook NF_LOCAL_OUTPUT is invoked.

### ip_queue_xmit2()

net/ipv4/ip_output.c

The next function, ip_queue_xmit2(dev) of the netfilter hook NF_LOCAL_OUTPUT, sets the output device as specified in the routing cache entry. Now it is necessary to check how much header is available in the socket buffer, although buffer reservation is already complete.
