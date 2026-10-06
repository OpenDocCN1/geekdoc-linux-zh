# Chapter 17 IP Multicast for Group Communication

| vif_table[MAXVIFS] | () | net_device |
|---|---|---|n| | | vif_device dev |
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

replicated and where they have to be forwarded to. This means that the MFC implements the multicast routing table. The MFC is built in the form of a hash table, as we can easily see from the mfc_cache structure. All entries with the same hash value are linearly linked with the respective cache rows (ingly linked list). All cache rows are grouped in the field mfc_cache_array to form an MFC hash table with a size specified by MFC_LINES (include/linux/moute.h). By standard, the multicast forwarding cache comprises 64 rows or lines. Figure 17–12 shows schematically how the MFC packet is structured.

When additional routes should be found for an incoming multicast packet, then the multicast forwarding cache has to be searched for a matching entry. To find a matching entry, mfc_hash is initially used to determine the correct cache line. The input network device and the multicast group address are used as parameters. Next, the linked list in the cache line is processed until a matching entry is found. The entries in the MFC are of mfc_cache data type.

| mfc_cache_array[MFC_LINES] | mfc_cache |
|---|---|n| | mfc_mcastgrp |
| | mfc_origin |
| | mfc_parent vif_device |
| | mfc_flags vif_device |
| unres |
_ expires |unres |
res |
| min_vif max_vif vif_device |
| [0,MAXVIFS) |
| 1 | mfc_cache |
| | mfc_cache vif_device |
| MFC_LINES-1

FIGURE 17–12
Structure of the multicast forwarding cache (mfc_cache).