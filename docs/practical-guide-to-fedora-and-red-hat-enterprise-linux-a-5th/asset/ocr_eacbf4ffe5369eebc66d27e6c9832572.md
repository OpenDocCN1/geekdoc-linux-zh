![](bbox=[0.39, 0.1, 0.79, 0.38])

Figure 17-7 The Select Device Type window

# Adding a device

Normally the NetworkManager daemon identifies and adds new hardware to the system. You can then use system-config-network to edit the configuration information. If you need to add a NIC to the system manually, click the Devices tab, then click New on the toolbar. The utility displays the Select Device Type window (Figure 17-7).

The Select Device Type window can set up six types of connections (most of which do not pertain to setting up a LAN): Ethernet (page 361), ISDN (page 1089), modem, token ring (page 1111), wireless, and xDSL (page 1116). ISDN, modem, wireless, and xDSL are PPP (Point-to-Point Protocol) connections. PPP is a serial line protocol that establishes a connection between two systems, putting them on the same network. It is capable of handling several protocols, the most common of which is TCP/IP, which provides compression for increased efficiency. The two systems can then run ssh, X, or any other network application between them. Ethernet and token ring are used to connect to LANs.

Choose the type of connection you want to establish and click Forward. Some selections probe for information at this point. You can accept entries in the filled-in text boxes in the following window; fill in blank text boxes as appropriate. When you have finished setting up the device, click Apply. The Select Device Type window closes, and the Network Configuration window displays the device you just added. Follow the instructions in the next paragraph to edit the configuration information. If you are finished, click the Devices tab, highlight the new device, click Menu bar: File->Save, and click Activate to bring the new device online.

# Editing a device

To modify the device name of network hardware, such as a NIC, click the Hardware tab of the Network Configuration window, highlight the description of the