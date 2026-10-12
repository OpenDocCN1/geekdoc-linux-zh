![](bbox=[0.18, 0.11, 0.76, 0.44])

**FIGURE 3.13** Select or enter networking configuration information.

# ## Network Configuration

If you have an installed network adapter, you are asked for network configuration details, as shown in Figure 3.13. Fedora can be set to automatically configure networking upon booting. Note that you can also configure networking following installation using Fedora’s `system-config-network` graphical network administration tool (see Chapter 14, “Managing Users,” for details about using these tools).

> > **NOTE**
> >
> > If the Linux kernel finds more than one network interface installed on your computer, you might be asked to configure a second ethernet device. This might be the case, for example, if you are installing Fedora on a computer that serves as a gateway or firewall. If you configure more than one ethernet device, the device named `eth0` will be the first active interface when you start Fedora.

You can choose to have your interface information automatically set using DHCP. Otherwise, especially if you are configuring a DHCP server, manually enter an IP address, hostname, or gateway address (such as for a router), along with DNS information if you click the Edit button listed by the interface (such as `eth0` in the example). After making your selection, click Next to continue.