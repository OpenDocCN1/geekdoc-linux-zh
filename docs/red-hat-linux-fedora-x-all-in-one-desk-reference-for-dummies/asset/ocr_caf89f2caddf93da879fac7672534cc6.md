# Configuring TCP/IP Networking 303

information you provide. However, Fedora Core comes with the graphical network configuration tool that you can use to add a new network interface or alter information such as name servers and hostnames.

Use the Fedora network-configuration tool to set up networking if you're adding a new Ethernet card (or if your Ethernet card was not configured during installation).

Start the network-configuration tool, log in root and from the GNOME desktop, choose Main Menu>System Settings>Network. If you are not logged in as root, you're prompted for the root password.

The network-configuration tool displays a tabbed dialog box, as shown in Figure 2-3.

![](bbox=[0.13, 0.185, 0.84, 0.645])

You can configure your network through the four tabs that appear along the top of the dialog box. Here's what each of the tabs does:

+   **Devices**: Here you find options for a new network interface (for example, an Ethernet card). You can set the IP address of the interface and activate it. Information that you enter about a device is stored in various files in the `/etc/sysconfig` directory.

+   **Hardware**: Here you add a new hardware device, such as an Ethernet card, modem, or an ISDN device. You can then provide information such as interrupt request (IRQ), I/o port numbers, and DMA channels for the device.