
# Chapter 17 IP Multicast for Group Communication

![](img/5a25b942ec3329b8799f2b5f0de564f6_371_0.png)

FIGURE 17-10
Managing multicast groups or addresses in an IP instance and a network device.

```
dev->mc_list	include/linux/netdevice.h
```

next points to the next entry in the list.
dmi_addr[MAX_ADDR_LEN]: This is the layer-2 address of the group packets of which should be received.
dmi_addrlen specifies the length of the layer-2 address in dmi_addr.

## 17.4.2 Multicast Data Path in the Internet Protocol

Now that we have described how multicasting is supported on the MAC layer, this section explains how IP multicast packets are processed in the Linux implementation of the Internet Protocol. We will first look at end systems and multicast routers.

However, before we discuss the details of the processes involved, we want to introduce two important components of the multicast implementation: virtual network devices, which abstract from the two possible transmission types for multicast packets (i.e., LAN adapter card or IP tunnel), and the multicast routing table (multicast forwarding cache).

**Virtual Network Devices** Multicast packets can be received and sent in either of two different ways: either directly over the network adapter in a LAN, or packed inside a unicast IP packet and transported through a tunnel. To prevent distinguishing these two cases in the entire multicast implementation, an abstraction—the-called virtual network device or virtual interface (VIF)—was introduced for both cases.

## 17.4 Multicast Data Path in the Linux Kernel 349

```
struct vif_device include/linux/mroute.h
```

In the Linux kernel, virtual network devices are represented by the vif_device structure. A virtual interface describes either a physical network device of the type net_device or an IP-IP tunnel. A flag is used to distinguish these two methods.

```c
struct vif_device {
    struct net_device *dev;             /* Device we are using */
    unsigned long bytes_in,bytes_out;   /* Statistics */
    unsigned long pkt_in,pkt_out;       /* Traffic shaping (NI) */
    unsigned long rate_limit;           /* / */
    unsigned char threshold;           /* TTL threshold */
    unsigned short flags;              /* Control flags */
    u32 local,remote;                  /* Addresses(remote for tunnels) */
    int link;                           /* Physical interface index */
};
```

- dev: a pointer to the network device (net_device), may be used bytes_in, bytes_out: statistical information about the transported bytes pkt_in, pkt_out: number of packets handled threshold: value for packets that should be sent over this virtual network device (as in Section 17.2.3) flags: flags to specify, for example, whether the VIF represents a tunnel (IFF_TUNNEL). local and remote: either (a) the IP addresses of the tunnel starting point and the tunnel end point, or (b) the IP address of the network device link: Index of the physical network device.

Figure 17-1 shows how the vif_device structure is structured and embedded in its environment. Virtual network devices are stored in the (array) vif_table. It can maintain a maximum of MAXVIFS entries for each computer. The maximum number is 32, and this number cannot be increased in personal computers, to fit the variable vif_map (in ipv4/ip.c). Each bit of vif_map marks whether the virtual device corresponding to the bit index has been created. The maximum number, 32 VIFs for a 32-bit architecture, results in this number can be limited (but not extended) by MAXVIFS. This limitation results in the fact that a multicast router can be directly connected to a maximum of MAXVIFS other routers.

Each entry in the array represents either a physical network device or a tunnel. The entries are set and removed by the multicast daemon (e.g., routed) by use of the socket options MRT_ADD_VIF and MRT_DEL_VIF. The parameters of the vif_device structure are passed in a vifctl structure (VIF control). Section 17.5.2 discusses how virtual network devices are configured.

## Multicast Forwarding Cache

The multicast forwarding cache (MFC) is the central structure used to store information about how often incoming multicast packets have replicated and where they have to be forwarded to. This means that the MFC implements the multicast routing table. The MFC is built in the form of a hash table, as we can easily see from the mfc_cache structure. All entries with the same hash value are linearly linked with the respective cache rows (ingly linked list). All cache rows are grouped in the field mfc_cache_array to form an MFC hash table with a size specified by MFC_LINES (include/linux/moute.h). By standard, the MFC comprises 64 rows.

| vif_table[MAXVIFS] | () | net_device |
|---|---|---|
| | | vif_device dev |
| | bytes_in, bytes_out | |
| | pkt_in, pkt_out | |
| | rate_limit | |
| | threshold | |
| | flags | |
| | local, remote | |
| | link | |
| | 1 | vif_device | |
| | 2 | vif_device | |

FIGURE 17–11
The vif_table of a virtual network device.

When additional routes should be found for an incoming packet, the mfc_hash is initially used to determine the correct cache line. The network device and the multicast group are used as parameters. Next, the linked list in the cache line is processed until a matching entry is found.

| mfc_cache_array[MFC_LINES] | mfc_cache |
|---|---|
| | mfc_mcastgrp |
| | mfc_origin |
| | mfc_parent |
| | mfc_flags |
| | unres |
| | res |

FIGURE 17–12
Structure of the multicast cache (mfc_cache).

## 17.4 Multicast Data Path in the Linux Kernel 351

The tls field includes information about virtual network devices that can be used to forward the packet. A TTL entry smaller than 255 means the virtual device with an identical index to the array should forward these packets. The tls array is processed sequentially. To optimize this, minif and maxif store the minimum and maximum VIF indexes that should receive the packet.

```
struct mfc_cache include/linux/mroute.h
```

```c
struct mfc_cache {
    struct mfc_cache *next;        /* Next entry on cache line */
    u32             mfc_mcastgrp;   /* Group, entry belongs to */
    u32             mfc_origin;     /* Source of packet */
    vif_t           mfc_parent;     /* Source interface */
    int             mfc_flags;      /* Flags on line */

    union {
        struct {
            unsigned long expires;
            struct sk_buff_head unresolved; /* Unres. buffers */
        } unres;
        struct {
            unsigned long last_assert;
            int minif, maxif;
            unsigned long bytes;
            unsigned long pkt;
            unsigned long wrong_if;
            unsigned char ttls[MAXVIFS]; /* TTL thresholds */
        } res;
    } mfc_un;
};
```

- * next points to the next entry in the multicast forwarding cache. The cache lines are organized in singly linked lists. A NULL pointer in this field marks the end of a cache line.
- * mfc_mcastgrp and mfc_origin together form the key for an entry in the multicast forwarding cache. mfc_origin is the IP address of the sending computer, and mfc_mcastgrp specifies the multicast group for a multicast packet, the route of which is represented by this entry.
- * mfc_parent is the index of the virtual network device in the vif_table, over which packets of this Mfc should arrive.
- * The mfc_un structure is a union structure: It is either an unres structure or a res structure. The two structures are defined per union, because either one structure or the other is required, but never both.
