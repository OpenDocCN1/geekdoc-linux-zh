
## Device Configuration: Automatic or Static

![](img/ab68ea377332b50bf70ef1316c8175b6_161_0.png)

file. To add an entry, click New. A window opens with boxes for the hostname, IP address, and nicknames. When you finish, the entry is added to the Hosts list. To edit an entry, click Edit and a similar window opens, enabling you to change any of the fields. To delete an entry, select it and click Delete.

> *NOTE If you are having trouble connecting with an Ethernet device using a static network connection, make sure that the Hosts panel lists your hostname and IP address, not just localhost. If your hostname is not there, add it.*

The Devices panel will list the configured network devices on your system. An entry shows the device name and its type. Use the New, Edit, Copy, and Delete buttons to manage the device entries. To edit a device, you can just double-click its entry. For example, when you edit an Ethernet device, you open a tabbed panel for configuring it, enabling you to specify whether it is dynamic or static (see Figure 5-3). There is an entry for automatically activating it when the system starts. You can choose to use IPv6 for automatic addressing. For DHCP you can automatically obtain DNS information. For a static connection you will be able to enter an IP address, netmask, and gateway. A Hardware panel will let you choose the actual hardware device to use. The configuration panels will differ, depending on the device you edit. For example, a modem device will add panels for provider, compression, and modem options, whereas a DSL connection will have panels for provider, route (gateway), and hardware device. An Ethernet connection will have only general, route, and hardware device panels. Making entries here performs the same function as if config.

![](img/ab68ea377332b50bf70ef1316c8175b6_162_0.png)

When you finish and are ready to save your configuration, select the Save entry from the File menu. If you want to abandon the changes you made, you can close without saving. You can run system-config-network at any time to make changes in your network configuration.

## Profiles

The system-config-network tool also supports profiles. Profiles are commonly used for portable computers that may be moved from one environment to another. For example, at your office you could have an Office profile that uses an Ethernet card to connect to the office LAN. At home, you could use a Home profile that uses a modem to connect to the Internet. Profiles are integrated into the configuration process, with a Common profile functioning as the default configuration. The Common profile will be inherited by all other profiles, so make your basic configuration with that profile.

Profiles are accessed from the Profile menu. Select the profile you want, or select New to create a new profile. The name of the currently selected profile will be displayed at the bottom of the Network Configuration screen. The Delete entry in the Profile menu will delete the current profile. By default, the Common profile will be selected. To create a profile, click the New entry and enter the name of the profile. It will be added to the Profile menu. You can also remove or rename a profile. The new profile will inherit the setting of the common profile. Once you have selected a profile, you can then select devices or change DNS or host information. On the Devices panel of system-config-network, each device entry will have a check box. Selecting this check box selects the device for the current profiles. To select a device for a given profile, first be sure to select the profile you are configuring, and then click the device’s check box. For other profiles, the device will be unchecked. Select the Save entry from the File menu when you are finished. The changes you make will be part of that profile, and not of any other.

## Configuring Replaced or Unsupported Ethernet Cards

If you change your Ethernet card or if your card is not supported and you need to manually load a driver for it, you will have to manually configure the card. For supported cards, Kudzu will automatically detect the card when your system starts up and prompt you to configure it. For dynamic connections, simply select DHCP to automatically determine your network configuration. For static connections, enter the required network information, such as your IP address and DNS servers.

If the device is not supported or if you elected not to configure it with Kudzu, you can use system-network-config to manually create a new device for the card. For unsupported devices, make sure you have first obtained the required Linux kernel module for it and have installed that module using `modprobe` as described in the preceding chapter. Then, start up system-config-network and click the New button in the Device panel. Select Ethernet as the type of device and then select the Ethernet card from the list provided. On the Configure Network Setting panel, click Automatically Obtain IP Address, and select the method from the drop-down menu, usually DHCP. Also click Automatically Obtain DNS Information. For static connections, enter the required information, such as your IP and DNS server addresses. Your new device will now appear in the Devices panel. To activate it, select it and then click Activate.

If your network hardware was not detected and did not show up in the Hardware panel after loading its module, you can try manually adding it, specifying its parameters and identification yourself. Click the Hardware panel and then click New. This opens a Choose Hardware Type dialog with a pop-up menu for different types of network cards. Choosing one opens a Network Adapter Configuration screen, where you select the kind of adapter, its device name, and resources used, such as IRQ.

## Configuring New Network Devices Manually

If the device was detected but not configured, you will need to configure it manually. In this case the Hardware device will appear in the Hardware panel, but not in the Devices panel. To configure a new network connection manually, first open system-config-network to the Devices panel and click New. The Add New Device Type window opens and displays a list of all possible network connections (see Figure 5-4). When you select an entry, panels will

![](img/ab68ea377332b50bf70ef1316c8175b6_163_0.png)

![](img/ab68ea377332b50bf70ef1316c8175b6_163_1.png)

prompt you to enter basic information about a connection; this will include phone number, username, and password for modem, DSL, and ISDN connections, whereas Ethernet connections will prompt only for IP addresses. The types of connections and devices currently supported are Ethernet (**eth**), ISDN (**isp**), Modem (**ppp**), xDSL (**ppp**), Token Ring (**tr**), and wireless connections (**eth**). After you complete your entries, your connection setting is configured and the new connection will be ready for use.

## Modem Configuration

You can also use a modem with telephone lines to connect to a network. For a modem connection, your modem will be probed and detected. A window will then display entries for the serial device, baud rate, hardware control, and modem volume, which you can modify. You are then prompted to enter the phone number, username, and password for your ISP account. The system-config-network tool is then started up, listing your modem device as a **ppp** connection (**ppp** stands for the *Point-to-Point Protocol* [*PPP*]) protocol that transmits IP communications across telephone lines. You can then edit the **ppp** device to modify your settings and enter any other settings; for instance, you can enter IP addresses for static connections, specify compression methods, or list your DNS servers.

## DSL and ISDN Configuration

To configure DSL, you will need to provide login and password information for DSL (Digital Subscriber Line) and ISDN. In other respects, DSL and ISDN connections operate much like a local area network (LAN), treating a host as an integrated part of a network. On Fedora, you can set up a DSL or ISDN connection. For DSL, a dialog box displays for entering your login name, your password, and the Ethernet interface your DSL modem is attached to. You will also need to enter the IP addresses for the DNS servers provided by your ISP. You can elect to have the connection automatically made up when your system starts up (depending upon your selected network profile).

## Wireless Configuration

Wireless connections are now detected and configured by Network Manager. Should you need to, you can also configure a wireless connection manually as shown here. A wireless connection operates much like a standard Ethernet connection, requiring only an IP address and DNS server information to connect to the Internet. In addition, you will have to specify wireless connection information such as the network name and channel used. To add a new wireless connection, you start system-config-network, click New, and then select the wireless connection. If system-config-network is open, you can click Add on the Devices panel to start the configuration. You are prompted to select your wireless card.

On the Configure Wireless Connection panel, you then configure your wireless connection, selecting the mode, network name, channel, transmit, and key information.

- **Mode** Normally, you can leave this on Auto. For a simple network, one that does not require roaming, the mode is usually Ad Hoc. Managed networks allow roaming among different access points.
- **Network Name (SSID)** Can be left on Auto for a simple network. The Network Name is used to identify a cell as part of a virtual network.
- **Channel** Starting from 1, choose one with least interference.
