# Chapter 8 • Configuring Basic Networking

versions of netstat return information in the same format, but others display the information differently.)

Routing Information You can use the --route or -r parameter to obtain a routing table listing similar to what the route command displays.

Masquerade Information Pass netstat the --masquerade or -M parameter to obtain information about connections mediated by Linux's NAT features, which often go by the name IP masquerading. NAT enables a Linux router to “hide” a network behind a single IP address. This can be a good way to stretch limited IPv4 addresses.

Program Use Some versions of netstat support the --program or (-p) parameter, which attempts to provide information about the programs that are using network connections. This attempt isn't always successful, but it is often, so you can see what programs are making outside connections.

Open Ports When used with other parameters, or without any parameters at all, netstat returns information about open ports and the systems to which they connect.

All Connections The --all or -o option is used in conjunction with others. It causes netstat to display information about the ports that serve network connections, in addition to already-open connections. This use of netstat is described in more detail in Chapter 10, “Securing Your System.”

Keep in mind that netstat is a very powerful tool, and its options and output aren't entirely consistent from one distribution to another. You may want to peruse its man page and experiment with it to learn what it can do.

# Examining Raw Network Traffic

One network troubleshooting tool is tcpdump. This utility is a packet sniffer, which is a program that can intercept network packets and log or display them on the screen. Packet sniffers are useful diagnostic tools because they enable you to verify that a computer is actively receiving data from other computers. They also enable you to examine the data in its raw form, which can be useful if you understand enough of the protocol’s implementation details to spot problems.

![](bbox=[0.137, 0.735, 0.225, 0.775])

Although packet sniffers are useful diagnostic tools, they can also be abused. For instance, unscrupulous individuals can run packet sniffers to capture passwords that others send over the network. Depending on your network configuration, this trick can work if the packet sniffer isn't running on either the sending or the receiving computer. For this reason, many organizations have policies forbidding the use of packet sniffers except under limited circumstances. Thus, before running a packet sniffer, you should obtain written permission to use such a program from an individual who is authorized to grant such permission. Failure to do so can lead you into serious trouble, possibly up losing your job or even being sued.