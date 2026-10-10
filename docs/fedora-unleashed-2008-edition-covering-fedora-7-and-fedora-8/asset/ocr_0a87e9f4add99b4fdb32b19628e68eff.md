You need to make sure that the check box is marked next to both NetworkManager and NetworkManagerDispatcher; as you check the boxes, click the Start button directly above them to start the services immediately. Finally, click the Save button in the toolbar, and close the Service Configuration tool by going to File, Quit. When you've done this, the NetworkManager icon appears in the notification area of your top panel (see Figure 2.9). This is the applet that handles and monitors network connections.

![](bbox=[0.07, 0.23, 0.9, 0.46])

When you are ready, click the NetworkManager icon in the toolbar to connect to a wireless network. If your wireless access point broadcasts its SSID, it should appear in the list under wireless networks (similar to Figure 2.9). Simply click the required network and NetworkManager detects what encryption (if any) is in use and asks you for the passkey. Enter this and NetworkManager starts the wireless connection. The passkey is then stored in the default keyring (essentially a central way of managing security in Fedora); so if you have not yet used the keyring, you are asked to create a password. From now on, whenever you log in to Fedora, you will be asked for the key to unlock the keyring.

If for some reason your wireless network does not appear (you might have your SSID hidden), you have to use the Connect to Other Wireless Network option, which brings up the screen shown in Figure 2.10.

NetworkManager can handle WEP and WPA encryption, as well as enterprise variations of WPA. You are advised to use WPA encryption as it is the stronger of the two.

NetworkManager can also connect to Cisco VPN connections. You are able to specify connection settings as appropriate, or if you have access to a predefined configuration (PCF file) you can import it directly into NetworkManager.