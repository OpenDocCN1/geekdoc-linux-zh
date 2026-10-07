
# Using Red Hat Linux Configuration Tools

If you add or replacing hardware after your initial Red Hat Linux installation, you must configure the new hardware. You can do so using either the command line or the graphical configuration tools. To configure a network client host using the Red Hat command line, you can use a combination of commands or edit specific files under the /etc/sysconfig directory. To configure the hardware through a graphical interface, you can use Red Hat's graphical tool for X11 called redhat-config-network or the console-based netconfig command. This section introduces command-line and graphical software tools you can use to configure a network interface and network settings on your Red Hat system. You'll see how to control your NIC and manage how system interacts with your network.

Using the command-line configuration tools can seem difficult if you're new to Linux. For anyone new to the network, the redhat-config-network graphical tool is the way to go.

Both manual and graphical methods require access to root. If you don't have access, get it before trying any of these actions.

> NOTE
> The network configuration process described in this section is for client hosts. You cannot perform server network configuration, such as Domain Name System (DNS) and DHCP during installation. (See Chapter 14, "Managing DNS," for more information on configuring DNS; see the "DHCP" section later in this chapter for more information on that item.)

# Command Line Network Interface Configuration

You can configure a network interface from the Red Hat Linux command line using the basic Linux networking utilities. You configure your network client hosts with the command line by using commands to change your current settings or by editing a number of system files. Two commands, ifconfig and route, are used for network configuration. The netstat command displays information about the network connections.

```
/sbin/ifconfig
config is used to configure your network interface. You can use it to
```

- Activate or deactivate your NIC
- Change your machine's IP address, netmask, or broadcast address
- Create an IP alias to allow more than one IP address on your NIC
- Set a destination address for a point-to-point connection

You can change as many or as few of these options as you'd like with a single command.
The basic structure for the command is as follows:

```
/sbin/ifconfig [network device] options
```

Table 13.1 shows the ifconfig options and examples of their uses.

# Table 13.1 ifconfig Options

| Use | Option | Example |
| --- | --- | --- |
| Create alias | [network device] :[number] | ifconfig eth0:10.10.10 |
| Change IP address | | ifconfig eth0 down 10.10.10.12 |
| Change the netmask | netmask [netmask] | ifconfig eth0 netmask 255.255.255 |
| Change the broadcast | broadcast [address] | ifconfig eth0 broadcast 10.10.255 |
| Take interface down | down (up IP address) | ifconfig eth0 up (ifconfig eth10.10.10) |
| Set NIC promiscuous mode on [off] | [-]promisc | ifconfig eth0 promiscu |
| Set multicasting mode on [off] | [-]allmulti | ifconfig eth0 -allmulti allmulti |
| Enable [disable] point-to-point address | [-]pointpoint [address] | ifconfig eth0 -pointpoint 10.10.20) |

The ifconfig man page shows other options that enable your machine to interface with a number of network types such as AppleTalk, Novell, IPv6, and others. Again, read the man page for details on these network types.

> Promiscuous mode causes the NIC to receive all packets on the network. It is often used to sniff a network. Multicasting enables the NIC to receive all multicast traffic on the network.

If no argument is given, ifconfig displays the status of active interfaces. For example, the output of ifconfig, without arguments and one active and configured NIC, looks similar to this:

```
# /sbin/ifconfig
```

```
eth0 Link encap:Ethernet HWaddr 00:30:1B:0B:07:0D
  inet addr:192.168.2.70 Bcast:192.168.2.255 Mask:255.255.255.0
  UP BROADCAST RUNNING MTU:1500 Metric:1
  RX packets:127948 errors:dropped:0 overflows:0 frame:0
  TX packets:172675 errors:dropped:0 overflows:0 carrier:0
  collisions:7874 txuelen:100
  RX bytes:1909830 (18.2 Mb) TX bytes:7376857 (70.3 Mb)
  Interrupt:0 Base:0
lo Link encap:Loopback
  inet addr:127.0.0.1 Mask:255.255.0
  UP LOOPBACK RUNNING MTU:16396 Metric:1
  RX packets:215214 errors:dropped:0 overflows:0 frame:0
  TX packets:215214 errors:dropped:0 overflows:0 carrier:0
  collisions:0 txuelen:0
  RX bytes:6873908 (65.5 Mb) TX bytes:0
```

The output is easily understood. The entry displays the IP address for the interface. UP signifies that the interface is ready for use, BROADCAST denotes that the interface is connected to a network, RUNNING means that the interface is operating, and LOOPBACK shows which device (lo) is the loopback address. The Maximum Transmission Unit (MTU) on eth0 is 1500. This determines the size of the largest packet that can be transmitted over this interface (and sometimes tuned to other values for performance). Metric is a number from 0 to 3 that relates to how much information is placed in the routing table. The lower the number, the smaller the amount of information. The ifconfig command can be used to deactivate a specific interface, like so:

```
# ifconfig eth0 down
```

You can also configure and activate the device by specifying a hostname or IP address and network information. For example to configure and activate the eth0 interface with a specific IP address, using the ifconfig command like this:

```
# ifconfig eth0 192.168.2.35 mask 255.255.255 up
```

# Using Red Hat Network Configuration

If you have a host defined in your system's /etc/hosts file (see the “Red Hat Network Configuration” later in this chapter), you can configure and activate the interface according to the hostname like:

```
# ifconfig eth0 home.org
```

Read the next section to see how to configure your system with your LAN.

```
/bin/route
```

The second command used to configure your network is the route command. route is used to build the routing tables (in memory) for routing packets as well as displaying the routing information. It is used after ifconfig has initialized the interface. route is normally used to set up static routes to other networks via the gateway or to other hosts. The command configuration is like this:

```
/bin/route [options] [commands] [parameters]
```

To display the routing table, use the route command with no options. The display will look similar to this:

```
# /bin/route
```

Kernel IP routing table

| Destination Gateway Genmask Flags Metric Ref Use Iface |
| --- | --- | --- | --- | --- | --- | --- |
| 149.112.50.64 * | 255.255.255.192 | U | 0 | | 0 | eth0 |
| 208.59.243.0 * | 255.255.255.192 | U | 0 | | 0 | eth0 |
| 127.0.0.0 | 255.0.0.0 | U | 0 | | 10 | |
| default | 149.112.50.64 | 0.0.0.0 | UG | 0 | | 0 | eth0 |

In the first column, Destination is the IP address (or, if the host is in /etc/hosts or /etc/networks, the hostname) of the receiving host. The default is the gateway for this destination. The Gateway column lists the gateway that packets must go through to reach their destination. An asterisk (*) means that packets go directly to the host. Genmask can have several possible entries. In our example, U verifies that the route is enabled and G that Destination requires the use of a gateway. The Metric column displays the distance to the Destination. The Ref column is used by some UNIX flavors to convey the references to the route. It isn't used by Linux. The Use column indicates the number of times it has been looked up. Finally, the Iface column is the name of the interface for the corresponding entry.

Using the -n option to the route command will give the same information substituting IP for names and asterisks (*) looks like this:

```
# /bin/route -n
```

| Kernel IP routing table Destination Gateway Genmask Flags Metric Ref Use Iface |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 149.112.50.64 * | 255.255.255.192 | U | 0 | | 0 | eth0 |
