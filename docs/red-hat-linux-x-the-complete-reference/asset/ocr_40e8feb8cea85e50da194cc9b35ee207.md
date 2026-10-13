To configure a particular connection, double-click its entry in the Devices panel, which opens up a new window where you can modify or add settings for that connection. Here you would enter information specific to a particular connection, such as the gateway and netmask for an Ethernet connection, or the username and password for a DSL connection. Making entries here performs the same function as ifconfig. The Devices panel will list the configured network devices on your system (see Figure 5-2). An entry shows the device name and its type. Use the New, Edit, Copy, and Delete buttons to manage the device entries. For example, when you edit an Ethernet device, you open a tabbed panel for configuring it, enabling you to specify its IP address, hostname, gateway, and the hardware device it uses (see Figure 5-3). The configuration panels will differ depending on the device you edit. For example, a modem device will add panels for provider, compression, and modem options, whereas a DSL connection will have panels for provider, route (gateway), and hardware device. An Ethernet connection will have only general, route, and hardware device panels.

![](bbox=[0.2, 0.46, 0.55, 0.78])

Figure 5-3: Device configuration in redhat-config-network

When you finish and are ready to save your configuration, select the Save entry from the File menu. If you want to abandon the changes you made, you can close without saving. You can run redhat-config-network at any time to make changes in your network configuration.

# Profiles

The redhat-config-network tool also supports profiles. Profiles are commonly used for portable computers that may be moved from one environment to another. For example, at your office you could have an Office profile that uses an Ethernet card to connect to the office LAN. At home, you could use a Home profile that uses a modem to connect to the Internet. Profiles are integrated into the configuration process, with a Common profile functioning as the default configuration. The Common profile will be inherited by all other profiles, so make your basic configuration with that profile.

# Configuring Replaced or Unsupported Ethernet Cards

If you change your Ethernet card or if your card is not supported and you need to manually load a driver for it,