
The variable names are self-documenting. The GATEWAY variable specifies the default router.

## Configuration Programs

The files detailed in the preceding section serve to configure many general network parameters. Most of these networking options can be modified dynamically just by editing the proper file. `linuxconf` can be used to do this editing for you. However, `linuxconf` does not always make the changes dynamically so that changes will take effect immediately. Configuring the host's IP address and routing table dynamically may require special commands.

### Configure the Host's Network Interfaces: ifconfig

The `/sbin/ifconfig` program is used to configure a host's network interfaces. This includes basic configuration such as IP address, netmask and broadcast address, as well as advanced options such as setting the remote address for a point-to-point link (such as a PPP link).

Under Linux, all network interfaces have names composed of the driver name followed by a number. These are some of the network driver names supported by Linux:

| Driver Name | Device Type |
| :--- | :--- |
| eth | Ethernet |
| tr | Token Ring |
| ppp | Point-to-Point Protocol |
| slip | Serial Line IP |
| plip | Parallel Line IP |

Interfaces are numbered starting from 0 in the order the kernel finds them, and the devices are created in memory. By default, the Linux kernel will only find one network interface. If you have several network cards, you need to add a line like the following to the `/etc/lilo.conf` file and then re-run the `/sbin/lilo` command:

```
append="ether=IRQ,I/O,eth1 ether=IRQ,I/O,eth2"
```

This tells the kernel to add two more Ethernet devices—eth1 and eth2—whose cards are at the IRQ and I/O address specified. If you want the kernel to autoprobe the cards' I/O addresses and IRQs, you can use 0 for IRQ and I/O.

#### Basic Interface Configuration

This is the basic form of the `ifconfig` command:

```
ifconfig interface IP-address [netmask netmask] \
       broadcast broadcast-address
```

This form of the `ifconfig` command can only be used by root. The netmask and broadcast parameters are optional. If they are omitted, `ifconfig` gets their values from the default class for the IP address (see “Netmasks and Network Classes” in this chapter for more details). They should be included if subnetting is being used.

This command will load the proper network driver and configure the interface.

**Caution**

The command will do exactly as it’s told: It won’t check whether the broadcast address corresponds to the IP address and netmask supplied, so be careful!

**Tip**

It’s not enough to configure the interface. You need to tell the kernel how to get to the hosts on the network connected to that interface using the route add command (see “Manipulating the Routing Table” later in this chapter). You can avoid using the command line by using `ixxnxconf`. Click on the Adapter 1 tab and you will see the information used by your NIC (Network Interface Card). On this screen you can enable or disable your NIC. You can set the configuration mode of the NIC for Manual (static), Dhcp, or Bootp mode. You can set your hostname, your IP address and mask, specify the name of the network device, and specify the kernel module required for your particular device. If you should require it, you can specify the I/O port number and IRQ setting as well. Once the desired changes have been made, click Accept.

**Enabling and Disabling an Interface**

An interface can also be temporarily brought down (*deactivated*) and brought back up without having to be reconfigured. This is useful for temporarily disabling a server’s network connection (such as when reconfiguring a critical service). This is done with the following commands:

```
ifconfig interface down
ifconfig interface up
```

These forms of the `ifconfig` command can be used only by root.

**Checking Interface Status**

If you want to know the status of a network interface, just issue the command `ifconfig interface`. If you want to know the status of all active interfaces, use `ifconfig -a`.

## Network Aliasing—One Interface, Several Addresses

It is sometimes useful for a single network interface to have multiple IP addresses. For example, a server may be running several services, but you may want clients to access different IP addresses for each service to make reconfiguration easier in the future (if you need to split some services off to another server, for example).

Linux, like most other UNIX flavors, provides a feature called *network aliasing*, which does just what its name implies. To be able to use network aliasing, you must have reconfigured and recompiled your kernel and enabled the Network Aliasing and IP: Aliasing Support options in the Networking Options configuration section. The options can be either compiled into the kernel or compiled as modules.

Once you are running a kernel with aliasing enabled, creating an alias is as easy as issuing a standard *ifconfig* command. All you need to do is append a colon and an alias number to the interface name. Here is an example:

```
ifconfig eth0:0 10.1.1.1 netmask 255.255.255.0 broadcast 10.1.1.255
```

This creates an alias eth0:0 for Ethernet interface eth0, with the provided parameters. To automate the creation of an alias each time the host boots, you can add the command to create it to /etc/init.d/network.

## Other ifconfig Options

There are other options to ifconfig for some special circumstances:

`ifconfig interface local-address pointtopoint remote-address` will enable a Point-to-Point interface--one that connects only to a single other host, not to a network. The interface must also be enabled in the remote host, switching the local-address and remote-address parameters.

`ifconfig interface local-address tunnel remote-address` will create an IPv4 tunnel between two IPv6 networks. IPv4 is the current TCP/IP standard on the Internet. IPv6 is the next-generation IP standard. If there are two IPv6 networks that need to be connected via the Internet, a tunnel that uses the IPv4 protocol must be made.

## Manipulating the Routing Table: route

The /sbin/route command manipulates the kernel's routing table. This table is used by the kernel to see what needs to be done to each packet that leaves the host--whether to send it directly to the destination host or to a gateway, and on which network interface to send it.

The general form of the route command follows:

```
route options command parameters
```

### Viewing the Routing Table

The simplest form of the command (with no options and no command) simply outputs the routing table. This form of the command can be used by any user:

```
$ /sbin/route
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
localnet        *               255.255.255.0   U     0      0      16    eth0
127.0.0.0       *               255.0.0.0       U     0      0      2    lo
default         router.company. 0.0.0.0         UG    0      0      71    eth0
```

The output has eight columns:

- The first column (**Destination**) indicates the route destination. The name is substituted if a corresponding entry exists in either /etc/hosts or /etc/networks. The special name default indicates the default gateway.
- The second column (**Gateway**) indicates the gateway through which packets to this destination are sent. An asterisk (`*`) means that packets will be sent directly to the destination host.
- The third column (**Genmask**) indicates the netmask that applies to this route. The netmask is applied to the value in the **Destination** column.
- The fourth column (**Flags**) can have several values. The most common flags are:
    - `U` Route is up. This route is enabled.
    - `H` Target is a host. This is a static route to a specific host (see “Host-Based Static Routes” later in this chapter).
    - `G` Use a gateway. That packet will not be sent directly to the destination host. The gateway will be used instead.
- The fifth column (**Metric**) indicates the distance to the target. This is used by some routing daemons to dynamically calculate the best route to get to a target host.
- The sixth column (**Ref**) isn’t used in the Linux kernel. In other UNIX systems it indicates the number of references to this route.
- The seventh column (**Use**) is the number of times the kernel has performed a lookup for the route.
- The eighth column (**Iface**) shows the name of the interface through which packets directed to this route will be sent.

There will always be at least one active route--the localhost route, which is set up in the `/etc/init.d/network` script. There should also be at least one route per network interface, pointing to the network the interface is connected to.

The `-n` option modifies the display slightly. It doesn’t do host or network name lookups, displaying instead numerical addresses:

```
$ /sbin/route -n
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref  Use Iface
10.0.1.0        0.0.0.0       255.255.255.0   U     0      0    16 eth0
127.0.0.0       0.0.0.0       255.0.0.0       U     0      0    2 lo
0.0.0.0         10.0.1.254    0.0.0.0         UG    0      0    71 eth0
```

In this case, the default destination and the `*` gateway are replaced by the address `0.0.0.0`. This output format is often more useful than the standard output format because there is no ambiguity as to where things are going.
