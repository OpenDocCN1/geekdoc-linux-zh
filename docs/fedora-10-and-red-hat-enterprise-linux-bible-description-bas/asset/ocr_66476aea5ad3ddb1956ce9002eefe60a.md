# Chapter 15: Setting Up Network Connections and LANs 637

you want instead of configure IP addressing, I recommend that you use the Network Configuration window, described later in this chapter.

Once a wired connection is working, however, you can use the NetworkManager applet to enable and disable the interface. To do that, right-click the NetworkManager applet and select Enable Networking. That will toggle the network interface on and off.

# Setting up a virtual private connection

NetworkManager applet offers some simple graphical tools for configuring your Fedora system to connect to a virtual private network (VPN). The following procedure describes how to configure NetworkManager to communicate with a remote openvpn server.

Sometimes the people and offices that have to work closely together are not physically close together. you may have:

+   - Two branch offices that need to constantly share sales databases, or
- An employee who needs to access office computers, printers, and files from home.

Rather than paying expensive medium, like the Internet, to want to use an inexpensive medium, the two sides communicate. The problem is that you don't want to open access to file sharing, print sharing, and other private services to the Internet. You also don't want communication between these sites to be exposed to anyone who is watching Internet traffic. One solution is to set up a virtual private network (VPN).

A VPN provides a way to set secure communications over an insecure network. With a VPN connection in place, the two sides of a connection can communicate as safely as they do on the same corporate LAN. To do this, a VPN usually offers the following features:

+   - **Authentication** — Using passwords or other techniques, two ends of a communication can prove that they are who they say they are before accepting a connection. After the connection is in place, communications can flow in both directions across.
- **Encryption** — By encrypting all data between two points on the public network, you can be assured that if someone could see the packets you send, they couldn't read them. Creating a connection between two public network addresses to use for exchanging encrypted data is known as tunneling.

Before you set a VPN connection with NetworkManager, the basic services need to be installed and running. Also, make sure the NetworkManager-openvpn and openvpn packages are installed. The following procedure assumes that NetworkManager is running and that you can reach a computer on your network that has an active openvpn service. (See Chapter 16 for information on setting up a VPN server with openvpn).

Click the NetworkManager applet icon, then select VPN Connections → Configure VPN. VPN Connections window appears.