**[-]allmulti** This option enables or disables the reception of all hardware multicast packets. Hardware multicast enables groups of hosts to receive packets addressed to special destinations. This may be of importance if you are using applications like desktop videoconferencing that are normally not used.

**mtu N** This parameter allows you to set the *MTU* of this device.

**netmask <addr>** This parameter allows you to set the net-mask mask of the network this device belongs to.

**irq <addr>** This parameter only works on certain types of hardware and allows you to set the IRQ of the hardware of this device.

**broadcast addr** This parameter allows you to enable and set the accepting of datagrams destined to the broadcast address, or to disable reception of these datagrams.

**pointopoint addr** This parameter allows you to set the address of the machine at the remote end of a point-to-point link, such as for *SLIP* or *PPP*.

**hw <type> <addr>** This parameter allows you to set the hard-ware address of certain types of network devices. This is not often useful for Ethernet, but is useful for other network types such as *AX.25*.

You may use the *ifconfifg* command on any network interface. Some user programs such as *pppd* and *dip* automatically configure the network devices as they create them, so manual use of *ifconfig* is unnecessary.

# # Configuring Your Name Resolver

The “*Name Resolver*” is a part of the Linux standard library. Its prime function is to provide a service to convert human-friendly hostnames like “*ftp.funet.fi*” into machine friendly IP addresses such as *128.214.248.6*.

# ## What's In a Name?

You will probably be familiar with the appearance of Internet host names, but may not understand how they are constructed, or deconstructed. Internet domain names are hierarchical in nature, that is, they have a tree-like

Part iii