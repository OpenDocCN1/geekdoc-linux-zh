
# Configuring a new network interface

Before you do anything, run the `dmesg` program (or view the `/var/log/dmesg` file) to find out whether your NIC is recognized by your current Linux kernel. If the Linux kernel recognizes your card, you should see some lines in the `dmesg` output pertaining to the kernel's discovery of your network device. For example, when I run

```
dmesg | grep -I eth
```

on a Red Hat Linux system with a generic (NE2000-compatible) Ethernet card, it displays the following output:

```
NE*000 ethercard probe at 0x340: 00 c0 f6 98 37 37
eth0: NE2000 found at 0x340, using IRQ 5.
```

This tells me that my NE2000-compatible NIC is found by the kernel and is using Interrupt Request Line (IRQ) 5 as well as the I/O address space starting at 0x340. Also note that this device is called `eth0` (Ethernet device 0).

After you confirm that your network device is being recognized by the kernel, you are ready to configure it. This example assumes that you want to configure the first Ethernet device, `eth0`, and that you want a *persistent* configuration, meaning that it will be used every time you start your computer. This is done with the help of the `/etc/rc.d/init.d/network` script. When this script is linked (where the name of the link is `S*network`; `*x` is any number) from the default run level directory (which could be `/etc/rc.d/rc3.d`), the `/etc/rc.d/init.d/network` script is run at boot time. This script loads the network interfaces using files stored in the `/etc/sysconfig` directory.

Now, take a look at how to configure `eth0` so that it automatically starts at boot time. The very first file you have to modify is `/etc/sysconfig/network`. Listing 7-1 shows an example of this file.

### Listing 7-1 The `/etc/sysconfig/network` file

```
NETWORKING=yes
FORWARD_IPV4=yes

HOSTNAME=picaso.nitec.com
DOMAINNAME=nitec.com

GATEWAY=206.171.50.49
GATEWAYDEV=eth0
```

The following list explains the lines in this file:

- The `NETWORKING=yes` line states that you want to enable networking support.
- `FORWARD_IPV4=yes` should be set to yes if you want to allow forwarding of IP packets to and from your Red Hat Linux computer. This is required only if a Red Hat Linux computer is going to act as a gateway or router (discussed in a later section) for a network. For example, if you plan to install proxy server software on your computer to allow Web access for other computers on your LAN, set this to yes. Conversely, if you plan to use this computer only as a co-located Web server on an ISP network, you can turn off IP forwarding by setting this to no.
- The next two lines specify the host name of the computer and the domain name of your network. The host name you specify must include the domain name you specify in the `DOMAINNAME` line. In other words, don't specify a host name that uses a different domain name from what you state in the `DOMAINNAME` line.
- The next two lines specify the information needed to determine the default gateway for a computer. A default gateway is a computer (or a router) that transfers packets to and from your computer. For example, if your Red Hat Linux computer is going to be connected to your LAN, where you have an ISDN router that connects the LAN to the Internet, specify the IP address of the ISDN router's network interface as the default gateway. The `GATEWAYDEV` entry is important when you have multiple network interfaces. If you have only one Ethernet device, this always should be set to `eth0`. If you have multiple Ethernet devices (`eth0`, `eth1`, and so on), you have to use the interface name that is connected to the default gateway.

After you configure the `/etc/sysconfig/network` file, you are ready to create the network interface file in the `/etc/sysconfig/network-scripts` directory. The network interface file uses `ifcfg-interface` as the naming convention. For example, the network interface filename for `eth0` is `ifcfg-eth0`. An example of this file is shown in Listing 7-2.

### Listing 7-2 The `/etc/sysconfig/network-scripts/ifcfg-eth0` file

```
DEVICE=eth0
NETMASK=255.255.255.240
IPADDR=206.171.50.50
NETWORK=206.171.50.48
BROADCAST=206.171.50.63
ONBOOT=yes
```

Before you can configure the information in this file, you must obtain from your ISP the network address, the network mask, the IP address for the network interface on the host, and the broadcast address. The network mask and broadcast address are discussed in a later section.

The following are explanations of the entries in the preceding file:

- The first line specifies the device name.
- The second line specifies the network mask (netmask) number.
- The third line specifies the IP address of the computer.
- The fourth line specifies the network address.
- The fifth line specifies the broadcast address.
- The sixth line contains the `ONBOOT` option, which should be set to yes if you want the network interface to be “up” (started) after boot.

After you configure these two files, you are ready to bring up the network. The easiest way to bring up the interface you just configured is to run the following:

```
/etc/sysconfig/network-scripts/ifup eth0
```

The `ifup` script takes the device name as the argument and starts it. It also creates a default route for the network. After you run this command, you can use the `ifconfig` program to see whether the interface is up and running. To see whether or not device `eth0` is up, run this:

```
ifconfig eth0
```

You should see output similar to the following:

```
eth0  Link encap:Ethernet  HWaddr 00:C0:F6:98:37:37
      inet addr:206.171.50.50  Bcast:206.171.50.63
      Mask:255.255.255.240
      UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
      RX packets:9470  errors:0  dropped:0  overruns:0  frame:0
      TX packets:7578  errors:0  dropped:0  overruns:0  carrier:0
      collisions:0
      Interrupt:5  Base address:0x340
```

Here, `ifconfig` reports that network interface device `eth0` has Internet address (`inet addr`) 206.171.50.50, broadcast address (`Bcast`) 206.171.50.63, and network mask 255.255.255.240. The rest of the information shows how many packets this interface has received so far (`RX packets`), how many packets this interface has transmitted so far (`TX packets`), how many errors of different types have occurred so far, what interrupt address line is being used for this device, what I/O address base is being used, and so on.

You can run `ifconfig` without any arguments to get the full list of all the up network devices. Note that the `ifup` script uses `ifconfig` to bring up an interface. For example,

```
ifconfig eth0  206.171.50.50 netmask 255.255.255.240 \
    broadcast 206.171.50.63
```

starts `eth0` with IP address 206.171.50.50. You can also quickly take down an interface by using the `ifconfig` command. For example, the following command takes down the `eth0` interface:

```
ifconfig eth0 down
```

After the interface is up and running, try to contact a computer in your network. You can use the `ping IP address` command to see whether your new interface can be used to contact a host on the same network.

If your `/etc/resolv.conf` file was not set up properly during installation, you will not be able to ping a host using its host name. The `/etc/resolv.conf` file looks like the following:

```
search nitec.com
nameserver 206.171.50.50
```

This is set up during Red Hat Linux installation. If you have specified an invalid IP address for the name server, your computer will not be able to contact the name server. So, if your network interface is up but you are unable to ping a host using the host name, try using the IP address of the host (really the network interface address). If you can ping the other host on your network, your interface is set up properly; just correct the name server link by fixing the IP address of the name server.

However, if you cannot ping a host using either the IP address or the host name, you might have a routing problem. If you haven’t used the `ifup` script as shown earlier and instead used `ifconfig` to bring up the interface, you need to create a default route to your network and a default gateway manually. To create a default route for your network, use the `route` command as follows:

```
route add -net network address netmask device
```

For example, to create a default route for the 206.171.50.48 network with a 255.255.255.240 netmask and `eth0` as the interface, I can run:

```
route add -net 206.171.50.48 255.255.255.240 eth0
```

To set the default gateway, run the `route` command as follows:

```
route add default gw gateway address device
```

For example, to set the default gateway address to 206.171.50.49, I can run the following command:

```
route add default gw 206.171.50.49 eth0
```

To verify that your network route and default gateway are properly set up in the routing table, use the following command:

```
route -n
```

Here is an example of output of the preceding command:

```
Kernel IP routing table
Destination     Gateway         Flags  Metric  Ref  Use  Interface
206.171.50.48   0.0.0.0       U      255.255.255.240 U          0        0      eth0
127.0.0.0       0.0.0.0       U           0        0        0      lo
0.0.0.0         206.171.50.49 UG          0        0        0      eth0
```

At this point, use the `ping` program to ping hosts inside and outside your network. If you are successful, your network is up. If you still do not...
