# Is the checksum correct?

Does the packet have a wrong length?

If the actual packet size does not match the information maintained in the socket buffer (skb->len), then the current packet data range is adapted by skb_trim(skb, ip->tot1_len). (See Section 4.1.) Now that the packet is adapted, the netfilter header NF_IP_PRE_ROUTING is invoked. Netfilter allows you to extend the variety of protocols by specific functions, if desired. Netfilter always allows desired re-routing in strategic points of certain protocols and are used, for firewall. Qos and address-translation functions. These examples will be discussed in later chapters. A netfilter hook is invoked by a macro, and the function following the handling of the netfilter tension is passed to this macro in the form of a function pointer. If netfilter was not configured, the macro ensures that there is a direct jump to this follow+up function. We can see in Figure 14-4 that the procedure continues with ip_rcv_finish().

```
ip_rcv_finish()
```

```
net/ipv4/ip_input.c
```

The function ip_route_input() is invoked within ip_rcv_finish(skb) to determine the route of the packet. The skb->dst pointer of the socket buffer is set to an entry in the routing cache, which stores not only the destination of the IP level, but also a pointer to an entry in the header cache (cache for layer-2 packet headers). If ip_route_input() cannot find a route, then the packet is discarded.

In the next step, ip_rcv_finish() checks whether the IP header includes options. If this is the case, the options are analyzed, and an ip_options structure is created. All options are set in this structure in an efficient form. Section 14.3 describes how IP options are handled.

Finally in ip_rcv_finish(), the procedure of the IP protocol reaches the junction between packets addressed to the local computer and packets to be forwarded. The information about the further path of an IP packet is stored in the routing cache skb->dst. Notice that a trick often used in the Linux kernel is used here. If a switch (variable value) is used to select different functions, then we simply insert a pointer to each of these functions. This saves us if or switch instruction for each decision of how the program should continue. In the example used here, the pointer skb->dst->input() points to the function that used should handle a packet further:

+   ip_local_deliver() is entered in the case of unicast and multicast packets that should be delivered to the local computer.
* ip_forward() handles all unicast packets that should be forwarded.
* ip_mr_input() is used for multicast packets that should be forwarded.

We can see from the above discussion that a packet can take different paths. The following section describes how packets to be forwarded are handled (skb->dst->input = ip_forward). Subsequently, we will see how skb->dst->input = ip_local_deliver handles packets to delivery locally.