
The default Red Hat Linux 6.0 kernel ships with these options enabled, but if you want to recompile your kernel, you should ensure that you select the following options:

- Network firewalls—This option lets the Linux kernel filter packets based on low-level information. You need this functionality, so select Y to this option.
- IP: firewalling—This option provides kernel services vital to IP masquerading, fire-walling, and other features. Select Y to this option.
- IP: always defragment—This option causes the Linux box to reassemble fragmented packets before passing them on. IP masquerading may be unreliable without this feature, so select Y.
- IP: masquerading—This option builds the kernel-level IP masquerading features, which rely upon the preceding three options. Select Y here.
- Protocol-specific modules—When you select IP: masquerading, you'll be able to select several modules that are specific to certain protocols, including IP: ICMP masquerading and some experimental support for forwarding protocols not understood by the main IP masquerading support. You may want to select Y for IP: ICMP masquerading, in order to let ping and other ICMP-based programs work. If you use a networking program that doesn't seem to work with standard masquerading, you can try the other options to see if they might help matters.
- IP: optimize as router not host—If your system will be used primarily as an IP masquerading router, and not itself as a server or client, you may want to select Y to this option to slightly improve performance. If the system will also function as a server or as a client system, you should probably say N to this option.
- IP: aliasing support—Linux supports the use of two IP addresses on a single NIC if you select Y to this option. Doing so allows you to perform IP masquerading using a single NIC. You place the private network on the same physical cabling as the broader network, but using addresses that the broader network won't try to use. This approach can be useful if your hardware is limited, but it's less efficient than the traditional two-NIC approach, and may be less secure as well. When you reboot, you can use aliases for the various networks connected to a single device; for instance, eth0 and eth0:1 for two networks both connected to the same Ethernet board.

Of course, your kernel also needs support for whatever network interface device you're using, for TCP/IP in general, and so on. You can use IP masquerading to masquerade across network technologies. For instance, if you've got a local Ethernet network and want to masquerade this network over a dialup PPP link, you can do so, but you need both Ethernet and PPP support in your kernel. The same is true if you have a local Token Ring network and want to masquerade this over Ethernet, in which case you need both Token Ring and Ethernet in your kernel. See Chapter 6, "Compiling a Kernel for Networking," for more information on networking kernel options.

## Configuring IP Masquerading

Once you’ve recompiled your kernel to include IP masquerading support and rebooted, you can configure your system to use this facility. One of the trickier aspects of getting IP masquerading working is properly configuring more than one network interface. Particularly if you’re using two interfaces of the same type (such as two Ethernet boards), getting the two to coexist can sometimes pose unusual challenges. The second component of activating IP masquerading is to use the ipchains utility to set up the masquerading rules that the kernel will then follow. This aspect of the job is comparatively simple.

## Configuring Multiple Network Interfaces

Before reading this section, you should be familiar with the basics of configuring a network interface. If you’ve not already configured your system to use at least one network, read Chapter 7, “Setting Ethernet Options.” If you intend to use IP masquerading in conjunction with a PPP dialup connection, you should also read Chapter 8, “Using PPP for Dialup Connections.”

## Configuring Two NICs

The simplest way to configure two or more network interfaces is often to use Red Hat’s linuxconf or whatever configuration tool comes with your distribution. Figure 20.2 shows the linuxconf NIC configuration screen (Config, Networking, Client tasks, Basic host information). Note that this configuration screen includes tabs for several network interfaces. Figure 20.2 shows the tab for Adapter 1, but in a multiple-NIC configuration, you can click the 2 tab to set the same options for the second interface, the 3 tab for the third NIC, and so on.

![](img/5d4d3092919d1d16884788127447cc6d_493_0.png)

FIGURE 20.2
You can configure each NIC independently using linuxconf.
