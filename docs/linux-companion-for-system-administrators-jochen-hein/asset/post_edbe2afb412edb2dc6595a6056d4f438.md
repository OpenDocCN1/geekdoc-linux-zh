
-   The default value for the broadcast address is determined automatically,
but it can equally be changed to allow subnetting. With the parameter
-broadcast, the use of broadcasts on this interface can be deactivated.

-   point followed by the IP address of the counterpart configures
specified interface for SLIP, PPP, or PLIP.

-   With the parameter hw, the hardware (Ethernet) address of the adapter can
be changed provided the corresponding driver supports this feature. This
can be sensible in special network configurations if the partner needs to be
configured on hardware addresses.

-   As the last parameter, the interface can be assigned an IP address. If this is
case, the interface is activated automatically (up is executed).

Listing 13.4 shows a sample output of ifconfig on a computer with
active Token Ring connection (and obviously loopback). For each interface,
various data are displayed: hardware address, assigned IP address (including
netmask and broadcast address), status of the interface and MTU. The following
two lines show the number of packets received (RX) and sent (TX), including
the number of errors, dropped packets and overruns. As a rule, these numbers,
compared to the number of successfully transmitted packets, should be very
small for a computer under normal load.

```
(Linux):# ifconfig
lo encap:Local Loopback
inet addr:127.0.0.1 Bcast:127.255.255 Mask:255.0.0.0
UP BROADCAST LOOPBACK RUNNING MTU:2000 Metric:1
RX packets:0 errors:0 dropped:0 overruns
TX packets:50 errors:0 dropped:0 overruns:0
t0 encap:UNSPEC Hwaddr:10-00-5A-D2-62-F8
inet addr:192.168.3.55 Bcast:192.168.3.255 Mask:255.255.255.0
UP BROADCAST RUNNING MTU:2000 Metric:1
RX packets:10723 errors:0 dropped overruns:0
TX packets:5456 errors:0 dropped overruns:0
interrupt:3 Base address:0xa20
```

Listing 13.4 Output of the ifconfig program for loopback and Token ring
interfaces.

## 13.5 All about route

The route program is used for specification of static routes which ensure that other computers in the Internet can be reached. As explained above, direct connection of computers by means of Ethernet is only realistic up to a certain network size. After this, separation into logically connected subnets must be carried out.

Connection between individual subnets is obtained through routers (formerly known as gateways). A router works on the protocol level (for example IP, IPX, or SNA) and can establish a suitable connection on the basis of the information contained in the protocols. In the following sections, we only look at the route of Internet protocols, or IP routing.

The route program is used to establish which computers or networks can be reached via which interface or which IP address is used as default gateway. Provided that the programs routed or gated are activated, routes can be modified by means of different routing protocols. In private local networks this is generally not needed.

A possibility for changing routes dynamically is provided by ICMP redirect messages. A detailed description of this protocol can be found in [rfc0792]. The route command without parameters displays (only under LINUX) the kernel routing tables. The parameter -n causes IP addresses to be output instead of host names, so no name server needs to be interrogated. A better alternative, because it is available on all UNIX systems, this is netstat -r. This command also displays the current routing tables of the kernel in a readable form. This information is provided by the kernel in the file /proc/net/route.

```
(Linux):# route -n
kernel routing table
Destination Gateway Genmask MSS Window Use Iface
192.168.3.0 * 255.255.255.0 U 1872 0 5537 tr0
127.0.0.0 * 255.0.0.0 U 1872 0 41 lo
default 192.168.3.1 * UG 1872 0 0 tr0
```

-   Listing 13.5 Output of the route program.

After activating an interface with ifconfig, computers and networks can be configured by means of route. A route is added with the parameter add. If the route leads to a computer, the corresponding address is prefixed with the keyword -host. If it leads to a network, -net is specified.

![](img/ad3b0471a5d608a011338d028bec5422_409_0.png)

## ALL ABOUT route 391

Each TCP/IP computer can address itself by means of the IP address 127.0.0.1 or the name localhost, which are reserved for this purpose. The corresponding network 127.0.0.0 is often called localnet. To be able to access the loopback interface, this must be activated by means of ifconfig, and the corresponding route must be established. This is done with the command:

```
route add -net 127.0.0.0
```

The route program automatically uses the netmask 255.0.0.0. The following example shows the configuration of the interfaces in more detail. These flags are listed in Table 13.4.

The next example shows the creation of a route.

```
route add -net 192.168.3.0 netmask 255.255.255.0 eth0
```

The route program automatically uses the netmask 255.0.0.0. The following example shows the configuration of the interfaces in more detail. These flags are listed in Table 13.4.

The next example shows the creation of a route.

```
route add -net 192.168.3.0 netmask 255.255.255.0 eth0
```

The route program automatically uses the netmask 255.0.0.0. The following example shows the configuration of the interfaces in more detail. These flags are listed in Table 13.4.

The next example shows the creation of a route.

```
route add -net 192.168.3.0 netmask 255.255.255.0 eth0
```

The route program automatically uses the netmask 255.0.0.0. The following example shows the configuration of the interfaces in more detail. These flags are listed in Table 13.4.

The next example shows the creation of a route.

```
route add -net 192.168.3.0 netmask 255.255.255.0 eth0
```

The route program automatically uses the netmask 255.0.0.0. The following example shows the configuration of the interfaces in more detail. These flags are listed in Table 13.4.

The next example shows the creation of a route.

```
route add -net 192.168.3.0 netmask 255.255.255.0 eth0
```

The route program automatically uses the netmask 255.0.0.0. The following example shows the configuration of the interfaces in more detail. These flags are listed in Table 13.4.

The next example shows the creation of a route.

```
route add -net 192.168.3.0 netmask 255.255.255.0 eth0
```

## 392 LINUX IN A NETWORKED ENVIRONMENT

The first command looks after transport of packets from its own SLIP, which is called sliprv. In the second step, a route 192.168.66.0 is entered via SLIP. For this purpose, it must be configured as gateway (IP forwarder). If you are not connected to a local network and connect to your provider (and thus the Internet) via SLIP, you must specify a default route.

A route can be deleted from the routing table, for example in case of problems or termination of dial-in connection, by means of the parameter del. The following command removes the routing entries of example.

The route program automatically uses the netmask 255.0.0.0. The following example shows the configuration of the interfaces in more detail. These flags are listed in Table 13.4.

The next example shows the creation of a route.

```
route add -net 192.168.3.0 netmask 255.255.255.0 eth0
```

The route program automatically uses the netmask 255.0.0.0. The following example shows the configuration of the interfaces in more detail. These flags are listed in Table 13.4.

The next example shows the creation of a route.

```
route add -net 192.168.3.0 netmask 255.255.255.0 eth0
```

## 13.6 The netstat program

The netstat program is another alternative for obtaining information on the current state of the network. It provides a number of options which display different kinds of information. netstat combines a series of utilities in one program. The different functions are selected via options.

-   -a generates a list of all Internet sockets, that are TCP, UDP, RAW, and UNIX sockets, including the ports that are only listening. This command informs you about the existing connections and their status, as well as your system provides to the net.

-   -i displays statistics on the network devices. All sent and received packets are shown, together with the errors, drops, and overruns that occurred. A sample output can be found in Listing 13.6. In the last column, you will find a series of flags which describe the configuration of the interfaces in more detail. These flags are listed in Table 13.4.

```
(Linux):# netstat -i
kernel Interface table
Iface MT MT-RX RX-ERR RX-DRP RX-OVR TX-OK TX-ERR TX-DRP TX-OVR Flags
lo 2000 0 0 0 0 89 0 0 0 BLU
tr0 2000 0 10840 0 0 1000 0 0 BRU
```

Listing 13.6 Output of the netstat -i command.
