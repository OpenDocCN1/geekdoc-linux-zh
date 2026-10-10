tries to open up a connection to the private network, the FreeBSD machine will have a permanent route (the VPN tunnel) into which to send the connection. Normal requests to the Internet will be passed upstream to the regular ISP's router, unaltered. The machines on the local network do not need to undergo any special configuration in order to inter-operate seamlessly with the machines at the corporate site. This topology enables large companies to maintain multiple branch offices in widely separate locations around the country or the world, while at the same time allowing employees at any location to access the resources at any other location as though they are all plugged into the same switch at the central office.

![](bbox=[0.34, 0.29, 0.62, 0.34])

![](bbox=[0.45, 0.37, 0.6, 0.42])

![](bbox=[0.45, 0.46, 0.58, 0.49])

![](bbox=[0.38, 0.52, 0.58, 0.6])

![](bbox=[0.52, 0.61, 0.6, 0.72])

**FIGURE 30.3** A single machine connects to the Internet and communicates directly with the corporate VPN server to set up a tunnel.

The same principles underlie both the simple and the more complex topology just described. Next in this chapter, you learn the techniques for putting these principles into action. First, we look at how to configure FreeBSD as a VPN client to connect to a remote VPN server, regardless of whether your topology involves a local network. Afterward, you learn how to create a VPN server so other machines can tunnel into your own private network.