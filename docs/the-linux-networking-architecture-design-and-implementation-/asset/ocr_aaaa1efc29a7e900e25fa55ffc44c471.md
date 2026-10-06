# 17.5 Multicasting in Today's Internet 359

# ipmr_ioctl1()

ipmr_ioctl1(sk, cmd, arg) can be used to poll various status information. If cmd has the value SIOCGETVIFCNT, a pointer to a sioc_vif_req structure (see below) in arg is expected. It includes the index of the virtual device for which information is to be queried (e.g., how many packets and what data values have been received and sent over this device). The result is added to the passed sioc_vif_req structure.

If cmd is equal to SIOCGETSCNT, a pointer to a sioc_sg_req structure in arg is expected. The corresponding information about the matching entry in the multicast forwarding cache is deleted.

ipmr_ioctl1() is entered in inet_create() (in net/ipv4/af_inet.c) as ioctl1() handling routing in the proto structure for raw sockets.

# ip_mr_init()

ip_mr_init(void) initializes the multicast functions in the kernel: it is invoked when inet_proto_init() (in net/ipv4/af_inet.c) starts.

# ipmr_get_route()

ipmr_get_route(skm, rtm, nowait) determines the route for a packet from a specific source for a specific group. This function is used for informative purposes only. The result is packed into a packet to send it to other routers (e.g. so that these routers exchange routing information). The route for the actual routing of multicast packets is specified in ip_mr_forward().

# ipmr_cache_find()

ipmr_cache_find(origin, mcastgrp) searches the multicast forwarding cache (see Section 17.4.2) for a specific entry. The packet's source address and multicast group address serve as search keys. An MFC entry is found, it includes all virtual network devices (VIFs) that can be used to forward the packet. The result is returned in the form of a pointer to an mfc_cache structure.

# ipmr_new_tunnel()

ipmr_new_tunnel(v) is responsible for creating a new tunnel. All information required this end is passed, together with the victfl structure (v). The function gets the tunnel network device, tun10, and tries to create a tunnel to the destination specified in v. If it is successful, then this virtual network device is returned; otherwise an error message (null) is returned.

# ipmr_cache_unresolved()

ipmr_cache_unresolved(cache, vifi, skb) is invoked by ip_mr_input() and ipmr_get_route(). if a specific entry was polled from the multicast forwarding cache.