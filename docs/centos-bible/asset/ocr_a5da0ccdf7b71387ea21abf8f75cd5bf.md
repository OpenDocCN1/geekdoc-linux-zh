# Chapter 14

Setting Up Network Connections and LANs

With computers becoming more mobile and wireless networks more common, setting up network connections is more diverse than in the days when most computers were at fixed locations and addresses. But, whether you are connecting to your own local area network (LAN) or a public wireless network, CentOS includes tools to set up the kind of network connections you want.

To allow you to manage your network connections interactively, CentOS includes NetworkManager. NetworkManager is described here for choosing and connecting to a wireless LAN because it includes an easy-to-use desktop applet that detects available wireless LANs and lets you choose the one you want to connect to.

In the home or in a small business, CentOS can help you connect to other Linux, Windows, and Mac computers so that you can share your computing equipment (files, printers, and devices). Add a connection to the Internet and routing among multiple LANs (described in Chapter 15), and CentOS can serve as a focal point for network computing in a larger enterprise. For times when you need more manual configuration for your LAN connections, this chapter describes how to use the Network Configuration window.

# **IN THIS CHAPTER**

+   - Using NetworkManager for network connections
+   - Understanding local area networks
+   - Connecting to a LAN with NetworkManager
+   - Setting up a wired Ethernet LAN
+   - Setting up a wireless LAN
+   - Troubleshooting your LAN

# Connecting to the Network with NetworkManager

NetworkManager is designed to make your network connections "just work." It finds your network interface cards, then connects to the network