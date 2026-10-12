+   - eth0 — the first Ethernet card. If you have more Ethernet cards, they get device names eth1, eth2, and so on.
+   - ppp0 — the first serial port configured for a point-to-point link to another computer, using Point-to-Point Protocol (PPP). If you have more serial ports configured for PPP networking, they are assigned device names ppp1, ppp2, and so on.
+   - sl0 — the first serial port configured for Serial Line Internet Protocol (SLIP) networking. SLIP establishes a point-to-point link to a TCP/IP network. If you use a second serial port for SLIP, it gets the device name sl1.

![](bbox=[0.08, 0.33, 0.2, 0.4])

You always have a loopback device (lo), whether or not you have any network. It passes data from one process to another without having to go out to a network. In fact, the loopback device allows network applications to work as long as the communicating processes are on the same system.

If you want to see the names of network devices installed on your system, log in as root and type the following command:

```
cat /proc/net/dev
```

This command shows the names of currently installed network devices, as well as statistics on the number of packets sent and received for a specific device.

# Running Red Hat’s network configuration tool

When you set up TCP/IP networking during Red Hat Linux installation, the installation program prepares all appropriate configuration files using the information you provide. However, Red Hat Linux comes with the netcfg graphical network configuration tool that you can use to add a new network interface or alter information such as name servers and host names.

To start the network configuration tool, log in as root and type netcfg in a terminal window to start that program. The network configuration tool displays a dialog box, as shown in Figure 12-3.