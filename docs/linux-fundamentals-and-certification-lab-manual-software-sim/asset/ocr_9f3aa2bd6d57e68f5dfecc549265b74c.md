![](bbox=[0.04, 0.08, 0.27, 0.23])

# Figure 7-1
Hubs and hosts.

+   hub A connection point to a network. Hubs (Figure 7-1) are layer 1 devices, meaning that they don't care about logical or physical addressing schemes, they just transmit the data received out all connection points. A hub is just an extension to the network cable. When a PC connected to a hub transmits information all connected devices see the information. Before hubs were used, a cable was run from machine to machine to make the connection.

+   switch A switch (Figure 7-2) routes information based on the physical (MAC) address provided in a frame of data. Each NIC of a network has a unique MAC address. A switch will use the MAC address to route transmissions only to the host referenced. In other words, if pc1 sends a transmission intended for pc4, only pc4 will see the transmission. Switches are layer 2 devices.

# Figure 7-2
Switched network.

![](bbox=[0.3, 0.28, 0.85, 0.43])

+   router A router's (Figure 7-3) job is path determination and switching. Routers look at the packets coming in and use the logical addressing embedded within the packets to determine where the information needs to go. Without routers, large networks would not be possible. Consider that the Internet has millions of devices connected. If all these devices were to broadcast information at the same time, the network would become overwhelmed with transmissions and the data would be unusable. Routers act as stop points for broadcast data, allowing only packets that are addressed to outside locations to pass through.

# Figure 7-3
Routed network.

![](bbox=[0.28, 0.58, 0.97, 0.98])