The following parameters relate to the spanning-tree algorithm and are discussed in Section 12.4.5. As mentioned earlier, the ports of a bridge are managed in a linear list, starting from the net_bridge structure. Each port in this list is represented by a net_bridge_port structure:

+   - net serves for linear linking of the ports of a bridge.
- net_bridge_ points to the net_bridge structure of the specified bridge. This pointer allows you to find the appropriate bridge instance quickly.
- net_device is a pointer to the net_device structure of the network adapter located to that port.
- port_no stores the port number.

More parameters also relate to the spanning-tree algorithm and are discussed in Section 12.2.4.

# Using a Hash Table for Forwarding Information

The Forwarding Data Base (fdb), which is used for forwarding in a bridge, is stored in a hash table. The major benefit of hash tables is that they normally offer direct access to the desired data.
Each_bridge structure uses the forwarding table to point to the hash vector. The preprocessor variable BR_HASH_SIZE can be used to set the number of entries. If a large number of stations are connected in a LAN network, then the size of the hash vector should be selected accordingly.
If you want to check whether a MAC address is already known to the destination, then a complex hash function (br_mac_hash()) is used to select a row of the hash vector. This row links all entries linearly with the same hash value (linear collision resolution). Figure 12–13 shows how structures are linked.
An entry in the hash table consists of net_bridge_fdb_entry structure. The first two parameters of this structure serve to link a hash row. The other parameters store the MAC address of the destination station and a reference to the port used to reach that station. The variable aging_timer is used to delete an entry from the hash table after some time when it is no longer required.

# 12.3 The Path of a Packet Through the Kernel

This section describes the path of packets through the Linux kernel (i.e., through a transparent bridge in Linux). As packets entering a Linux router (see Chapter 6), the network adapter receives a packet, triggers an interrupt on the network adapter, and stores the packet in an input queue. Subsequently, the function net_rx_action() runs the net_rx tasklet. This function also includes the entry point for the bridge implementation (br_handle_frame_hook())

In contrast to a router implementation, the network layer is not accessed here. Instead, once a bridge is activated, the function br_handle_frame() is invoked, and a pointer points to this function. If no bridge has been activated—for instance, when the bridge functionality was created as a module—then the hook points to null. In this case, an attempt is made to forward the packet to the higher layers. If the kernel was created without bridge support, these functions are missing, and no valuable computing time is wasted on searching for an activated bridge.