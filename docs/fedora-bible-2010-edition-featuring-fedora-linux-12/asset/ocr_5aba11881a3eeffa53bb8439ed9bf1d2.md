choices to let you choose your network connection. If you change network connections, NetworkManager will likewise try to change attributes of your connection, such as IP addresses, DNS servers, and routes.

Although NetworkManager has been included in the past several releases of Fedora, it is just becoming mature enough that you should consider using it as the facility for managing your network interfaces. In most cases with NetworkManager, connecting to an existing network is simple:

+   * **Wired network** — If a wired network interface is available and a DHCP server is found, Fedora will automatically connect to that interface and use it as your default route.
+   * **Wireless network** — If a wireless network interface is available, the NetworkManager applet menu shows all wireless networks that your wireless card can find. You simply choose the network you want and authenticate as needed.

> **NOTE:** The NetworkManager also allows you to share connections. For example, if you have a wireless broadband card, you can share the connection with other computers on your network, wired or wireless.

If the NetworkManager service is enabled on your Fedora system, you should see a two-computer-screen icon on the desktop top panel, as shown in Figure 14-1.

![](bbox=[0.13, 0.46, 0.45, 0.55])

Figure 14-1: The NetworkManager applet icon (upper left) shows NetworkManager is running.

If you see the NetworkManager applet icon, you can immediately start using NetworkManager. If it is not displayed, check that NetworkManager is installed and start the service, as follows:

1. **Check for NetworkManager** — Type the following from a Terminal window to see if NetworkManager packages are installed:

```
$ rpm -qa "NetworkManager*"
NetworkManager-gnome-0.7.996-6.git20091021.fc12.i686
NetworkManager-openvpn-0.7.996-4.git20090923.fc12.i686
NetworkManager-openconnect-0.7.996-4.git20090921.fc12.i686
NetworkManager-glib-0.7.996-6.git20091021.fc12.i686
NetworkManager-0.7.996-6.git20091021.fc12.i686
NetworkManager-vpnc-0.7.996-4.git20090921.fc12.i686
NetworkManager-pptp-0.7.996-4.git20090921.fc12.i686
```

2. **Install NetworkManager** — If NetworkManager packages are not installed, type the following as root user from a Terminal window:

```
# yum install "NetworkManager*"
```