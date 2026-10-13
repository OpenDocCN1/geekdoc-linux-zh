
![](img/32a48d8db4c23e6e2eb70d1e5034c976_89_0.png)

## Figure 5-2: The redhat-config-network DNS panel

You use the Hosts panel to associate static IP addresses with certain hosts. The panel has a single pane with New, Edit, Copy, and Delete buttons. This panel lists entries that associate hostnames with static IP addresses. You can also add aliases (nicknames). The Hosts panel actually displays the contents of the /etc/hosts file and saves any entries you make to that file. To add an entry, click New. A window opens with boxes for the hostname, IP address, and nicknames. When you finish, the entry is added to the Hosts list. To edit an entry, click Edit and a similar window opens, enabling you to change any of the fields. To delete an entry, select it and click Delete.

### Note

If you are having trouble connecting with an Ethernet device using a static network connection, make sure that the Hosts panel lists your hostname and IP address, not just localhost

To configure a particular connection, double-click its entry in the Devices panel, which opens up a new window where you can modify or add settings for that connection. Here you would enter information specific to a particular connection, such as the gateway and netmask for an Ethernet connection, or the username and password for a DSL connection. Making entries here performs the same function as ifconfig. The Devices panel will list the configured network devices on your system (see Figure 5-2). An entry shows the device name and its type. Use the New, Edit, Copy, and Delete buttons to manage the device entries. For example, when you edit an Ethernet device, you open a tabbed panel for configuring it, enabling you to specify its IP address, hostname, gateway, and the hardware device it uses (see Figure 5-3). The configuration panels will differ depending on the device you edit. For example, a modem device will add panels for provider, compression, and modem options, whereas a DSL connection will have panels for provider, route (gateway), and hardware device. An Ethernet connection will have only general, route, and hardware device panels.

![](img/32a48d8db4c23e6e2eb70d1e5034c976_91_0.png)

Figure 5-3: Device configuration in redhat-config-network

When you finish and are ready to save your configuration, select the Save entry from the File menu. If you want to abandon the changes you made, you can close without saving. You can run redhat-config-network at any time to make changes in your network configuration.

## Profiles

The redhat-config-network tool also supports profiles. Profiles are commonly used for portable computers that may be moved from one environment to another. For example, at your office you could have an Office profile that uses an Ethernet card to connect to the office LAN. At home, you could use a Home profile that uses a modem to connect to the Internet. Profiles are integrated into the configuration process, with a Common profile functioning as the default configuration. The Common profile will be inherited by all other profiles, so make your basic configuration with that profile.

## Configuring Replaced or Unsupported Ethernet Cards

If you change your Ethernet card or if your card is not supported and you need to manually load a driver for it, you will have to manually configure the card. For supported cards, Kudzu will automatically detect the card when your system starts up and prompt you to configure it. For dynamic connections, simply select DHCP to automatically determine your network configuration. For static connections, enter the required network information, such as your IP address and DNS servers.

If the device is not supported or if you elected not to configure it with Kudzu, you can use redhat-config-network to manually create a new device for the card. For unsupported devices, make sure you have first obtained the required Linux kernel module for it and have installed that module using modprobe as described in the preceding chapter. Then, start up redhat-config-network and click the New button in the Device panel. Select Ethernet as the type of device and then select the Ethernet card from the list provided. On the Configure Network Setting panel, click Automatically Obtain IP Address, and select the method from the drop-down menu, usually DHCP. Also click Automatically Obtain DNS Information. For static connections, enter the required information, such as your IP and DNS server addresses. Your new device will now appear in the Devices panel. To activate it, select it and then click Activate.

## Network Device Control

With the Network Device Control tool, you can activate or deactivate configured network connections. A pop-up menu will also let you select available profiles, automatically activating network connections associated with each profile, and deactivating those that are not. The Network Device Control tool is accessible in the System Tools menu. Selecting a device and clicking the Configure button will open the redhat-config-network tool. You can then select and configure any network device, as well as add new ones.

## The Internet Configuration Wizard

To configure a new network connection, you use the Internet Connection Wizard, accessible from the System Tools menu. If you already have redhat-config-network open and want to add a new network connection, clicking New will also start the Internet Connection Wizard. The wizard initially displays a list of all possible network connections (see Figure 5-4). When you select an entry, panels will prompt you to enter basic information about a connection; this will include phone number, username, and password for modem, DSL, and ISDN connections, whereas Ethernet connections will prompt only for IP addresses. The types of connections and devices currently supported are Ethernet (eth), ISDN (isdn), Modem (ppp), xDSL (ppp), Token Ring (tr), Crypto IP Encapsulation for Virtual Private Networks (cipcb), and wireless connections (eth). After completing your entries, the wizard will configure your connection setting and the new connection will be ready for use.

![](img/32a48d8db4c23e6e2eb70d1e5034c976_92_0.png)

Figure 5-4: Internet Connection Wizard

## Modem Configuration

You can also use a modem with telephone lines to connect to a network. For a modem connection, the Internet Configuration Wizard will probe and detect your modem. A window will then display entries for the serial device, baud rate, hardware control, and modem volume, which you can modify. You are then prompted to enter the phone number, provider, username, and password for your ISP account. The redhat-config-network tool is then started up, listing your modem device as a ppp connection (ppp stands for the Point-to-Point Protocol [PPP] protocol that transmits IP communications across telephone lines). You can then edit the ppp device to modify your settings and enter any other settings; for instance, you can enter IP addresses for static connections, specify compression methods, or list your DNS servers.

## DSL and ISDN Configuration

To configure DSL, you will need to provide login and password information for DSL (Digital Subscriber Line) and ISDN. In other respects, DSL and ISDN connections operate much like a local area network (LAN), treating a host as an integrated part of a network. On Red Hat, you can use the Internet Configuration Wizard to set up a DSL or ISDN connection. For DSL, the Internet Configuration Wizard will display a dialog box with entries for entering your login name, your password, and the Ethernet interface your DSL modem is attached to. You will also need to enter the IP addresses for the DNS servers provided by your ISP. You can elect to have the connection automatically made up when your system starts up (depending upon your selected network profile).

## Wireless Configuration

A wireless connection operates much like a standard Ethernet connection, requiring only an IP address and DNS server information to connect to the Internet. In addition, you will have to specify wireless connection information such as the network name and channel used. To add a new wireless connection, you start the Internet Configuration Wizard (from the System Tools menu) and select the wireless connection. If redhat-config-network is open, you can click the Add button on the Devices panel to start the Internet Connection Wizard. You are prompted to select your wireless card.

On the Configure Wireless Connection panel, you then configure your wireless connection, selecting the mode, network name, channel, transmit, and key information.

- **Mode** Normally, you can leave this on Auto. For a simple network, one that does not require roaming, the mode is usually Ad Hoc. Managed networks allow roaming among different access points.
- **Network Name (SSID)** Can be left on Auto for a simple network. The Network Name is used to identify a cell as part of a virtual network.
- **Channel** Starting from 1, choose one with least interference.
- **Transmit Rate** Usually set to Auto to adjust automatically to degraded transmissions. But you can set a specific rate such as 11M or 1M from the pop-up menu.
- **Key** This is the encryption key for your wireless network. It must be the same for each cell on your network.

On the Configure Network Settings panel, you specify your IP address, whether it is obtained automatically with DHCP or one you enter yourself. For most company wireless networks, the IP address will be obtained automatically. Normally, the DNS servers are also provided. You can, if you wish, also specify a host name.

If you are setting up a local or home network, you will most likely use static IP addresses you select yourself from the private IP pool, beginning with 192.168, such as 192.168.0.1. The static subnet mask for a small local network is usually 255.255.255.0. The Gateway is the IP address for the computer on your network that connects to the Internet, or to a larger network.

You can later edit a wireless connection, making changes. Wireless configuration has the same General and Hardware Device panels as an Ethernet or DSL connection, but instead of a Route panel, it has a Wireless Settings panel, where you can set your mode and network name along with channel, transmit, and key information.

Your configuration setting will be saved in an Ethernet configuration file in the /etc/sysconfig/network-scripts directory. For example, if your wireless card is designated eth1, then its configuration information is saved in the ifcfg-eth1 file. Here you will find the standard Ethernet connection parameters such as the IP address and gateway, as well as wireless parameters such as the channel used, the mode specified, and the encryption key. The standard setting can be modified using redhat-config-network on that device. You could also modify this file directly to enter additional parameters, like the frequency (FREQ) or sensitivity level (SENS). You can also specify any of the iwconfig parameters using the IWCONFIG option. Enter IWCONFIG followed by an assignment of the option and any value. For example, the following option sets the fragment threshold for packets:

```
IWCONFIG="frag 512"
```
