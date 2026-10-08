# 464 LINUX IN A HETEROGENEOUS NETWORK

| Network | Node_Address | Primary | Device | Frame_Type |
|---|---|---|---|--|
| 00000030 | 1005AD2813C | No | tr0 | 802.2TR |
| 10000106 | 000000000001 | Yes | Internal | None |

**Listing 19.2** The file /proc/net/ipx.interface.

The external network interface tr0, a Token Ring network card, is connected to the network 30, using frame type 802.2TR. The node address is the hardware address of the network card which is automatically inserted by the kernel. The first is not primary.
Each NetWare server has its own (internal) network. The number assigned to this must be unique and should therefore be centrally managed. If you are in doubt, please ask your network administrator. In this network, the server has the node address 1. In the above example, the internal interface is also the primary one.

Listing 19.3 shows an example of the file /proc/net/ipx. As soon as your computer participates in the IPX network, this file fills up automatically.

| Local_Address | Remote_Address | Tx_Queue | Rx_Queue | State Uid |
|---|---|---|---|--|
| 10000106:4000 | Not_Connected | 000000000 | 000000000 | 07 | 000 |
| 10000106:0452 | Not_Connected | 000000000 | 000000000 | 07 | 000 |
| 10000106:0453 | Not_Connected | 000000000 | 000000000 | 07 | 000 |
| 10000106:4001 | Not_Connected | 000000000 | 000000000 | 07 | 000 |
| 10000106:4002 | Not_Connected | 000000000 | 000000000 | 07 | 000 |
| 10000106:0451 | Not_Connected | 000000000 | 000000000 | 07 | 000 |
| 10000106:4003 | Not_Connected | 000000000 | 000000000 | 07 | 000 |
| 10000106:4004 | Not_Connected | 000000000 | 000000000 | 07 | 000 |

**Listing 19.3** The file /proc/net/ipx.

Listing 19.4 shows an excerpt from the file /proc/net/ipx. In this file, the routing table for IPX packets is shown in a readable format. For each reachable network, the table indicates the network through which the routing takes place and which computer acts as a router. Since IPX servers also function as routers and publish this information periodically in the network, this table fills up quickly. If you have many NetWare servers, this (pseudo) file will contain lots of entries.