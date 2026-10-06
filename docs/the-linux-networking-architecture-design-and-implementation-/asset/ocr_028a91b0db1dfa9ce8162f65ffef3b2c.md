# 5.1 The net_device interface 79

then the network adapter has to pass this packet to the upper layers. The driver method set_multicast_list is used to pass the addresses of the list to the network adapter. The hardware filter of this network adapter (if present) is responsible for passing to the kernel only those packets of interest to this computer.
mc_count contains the number of addresses in dev_mc_list.
watchdog_time and watchdog_timer are used to detect problems an adapter may incur when sending packets. For this reason, the watchdog_timer is initialized when a network device starts and always called after watchdog_timeout units (jiffies). The handling dev_watchdog() checks whether or not watchdog_timeout units have passed since the last transmission of a packet (stored in trans_start). If this is the case, then there were problems in the transmission of the last packet, and the network adapter has to be checked. To check the network adapter, the driver function tx_timeout() is called. If not much time has passed since the last start of a transmission, then nothing is

# Data on the Network Layer

ip_ptr, ip6_ptr, atalk_ptr, dn_ptr, and ec_ptr point to information of layer-3 protocols that use this device. If the network device is configured for the Internet protocol, among others, then ip_ptr points to a structure of the type in_device, which manages information and configuration parameters of the relevant IP instance. For example, the in_device structure manages a list with IP addresses of the network device, with active IP multicast groups, and the parameters for the ARP protocol.
family designates the address family of the network device. In the case of the Internet protocol (IP), this field takes the constant AF_INET.
pa_allen specifies the length of the addresses of the protocol used. IP addresses of the class AF_INET have the length four bytes.
pa_addr, pa_braddr, and pa_mask contains the addressing of a network device on the network layer. pa_baddr specifies the broadcast address, and pa_mask specifies the network mask. All three values are set by ifconfig when a network device is activated.
_dstaddr specifies the address of the other partner in a point-to-point connection (e.g., PPP or SLIP).
flags indicates different switches. Some describe properties of the network device (IFF_ARP, IFF_MULTICAST, ...); others output the current state (IFF_UP). Table 5–1 lists the meaning of these switches, which can be set by use of the ifconfig command.

Device-Driver Methods As mentioned earlier, one of the tasks of the network device is to abstract a network device from the underlying hardware. The set of methods available for network driver functions have to be mapped to a uniform interface so