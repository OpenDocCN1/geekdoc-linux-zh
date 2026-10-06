# Chapter 5 Network Devices

do_ioctl(): This method is generally not used by higher protocols, because they have no generic functions. It is normally used to pass adapter-specific ioctl() commands to the network driver.

set_config() is used to change the configuration of a network adapter at runtime. The method lets you change system parameters, such as the interrupt or the memory location of the network adapter.

The methods for a device described above depend on the network adapter used, which means they have to be provided by the driver, if their functionality is required. The methods described below less depend on the hardware of a network adapter, rather than on the layer-2 protocol used. For this reason, they don't necessarily have to be implemented by driver-specific methods, but can run on top of existing methods (e.g., for Ethernet and FDDI).

hard_header() creates a layer-2 packet header from layer-2 addresses for source and destination.

rebuild_header() is responsible for rebuilding the layer-2 packet header before it is transmitted. This function was the entry point to the ARP protocol in earlier versions of the Linux kernel. The conversion to the neighbour cache should create a stored layer-2 packet header, so that rebuild_header() is called only when the hard header cache contains wrong information.

hard_header_cache() fills a layer-2 packet header in the hard header cache with passed data. This means that transmission processes can access a prepared layer-2 packet header.

hard_header_update() changes the layer-2 destination address in a stored layer-2 packet header in the hard header cache.

hard_header_parse() reads the layer-2 sender address from the layer-2 packet header in the packet data space of a socket buffer and copies it to the passed address, haddr.

set_mac_address() can be used to change the layer-2 address of a network adapter, if it supports alternative MAC addresses.

change_mtu() changes the MTU (Maximum Transfer Unit) of a network device and implements all necessary changes.

# MANAGING NETWORK DEVICES

Now that we know how a network device can be represented by the net_device structure in the Linux kernel, this section discusses the management of network devices. First, we will describe how network devices can be linked, and we will introduce methods that can be used to manage and manipulate network devices. As mentioned earlier, this section will look at network devices only from the “top”—their uniform interface for protocol instances of the higher-order layers.

All network devices in the Linux kernel are connected in a linear list (Figure 5-3). The kernel variable dev_base represents the entry point to the list of registered network