+   - Real Audio—Real Networks' audio (and video) transfer protocol works when appropriate support is included in the kernel.
+   - Miscellaneous A/V protocols—Assorted audio/video transfer programs are supported.
+   - Assorted games—Games such as Battle.net, Diablo, Quake, and StarCraft work with IP masquerading. Many of these require that the generic ipportfw IP masquerading support be compiled into the kernel.
+   - PC-Anywhere—This program allows remote control of a Windows system. The client program works, but you can't run a server from within a private network for access from the outside.

# Unsupported Applications

The list of supported protocols is quite large. By contrast, the list of unsupported protocols is relatively small, although the server side doesn't work well from within a masqueraded network. The list of unsupported tools includes

+   - Servers—Because IP masquerading reveals only the IP masquerading machine's ports (see Figure 20.6), it's difficult to run a server within the private network. You can run a server on the IP masquerading machine itself, though. More sophisticated configurations permit the running of servers for the outside world within an IP masqueraded network, by forwarding access to specific ports. (One way to do this is to write additional ipchains rules. Another is to use the xinetd program's redirect feature, as described briefly in Chapter 24 [p. 559].) Of course, you can run a server within the network if you only want the computers on the private network to have access to the internal server. This feature can be very useful for hiding a file or print server from the outside world.

![](bbox=[0.18, 0.82, 0.72, 0.95])

FIGURE 20.6
A request for services comes to the IP masquerading computer, but that request is not passed on to a private network machine without special configuration.