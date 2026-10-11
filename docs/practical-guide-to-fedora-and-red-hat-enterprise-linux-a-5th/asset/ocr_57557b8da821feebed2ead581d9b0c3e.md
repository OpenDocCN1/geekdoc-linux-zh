![](bbox=[0.39, 0.09, 0.8, 0.51])

**Figure 17-4** The Editing window (wireless connection)

**Hidden Wireless Networks**, and **Create New Wireless Network** (if the system has a wireless connection), **Wired Network**, **Disconnect**, and **VPN Connections**. In Figure 17-5 (on the next page), **Auto eth0** appears below **Wired Network** and **disconnected** appears below **Wireless Networks**, meaning that the system is using the **eth0** wired connection and is not using a wireless connection.
Click the name of the wired network (e.g., **Auto eth0**) or the name of a wireless network (under the word **Available**) to connect to a network. The **NetworkManager** applet changes to two dots with a tail going around them in circles while it connects to the new network. It then displays a connecting or wired icon, as is appropriate (Figure 17-2, page 599). To disable a network, click **Disconnect** below the name of a connection you want to disable.

# THE NETWORK CONFIGURATION WINDOW
(system-config-network)

To display the **Network Configuration window** (Figure 17-6, next page), select **Main menu: System**↠**Administration**↠**Network** or give the command **system-config-network** from a terminal emulator or **Run Application window** (ALT+F2). The **system-config-network** utility (projects.gnome.org/NetworkManager; part of the package named **system-config-network**) configures network hardware. The