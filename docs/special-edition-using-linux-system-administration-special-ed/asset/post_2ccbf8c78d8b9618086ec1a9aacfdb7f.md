
> **Note**
> 
> While you can specify a search path containing any combination of one or more of the three available options listed above, it is generally wise to include the local hosts file in your path, preferably as the first option. You should include commonly looked-up names (including your own host) in this file so that these lookups don't require a network connection to a server for resolution. This will reduce network bandwidth requirements and speed up resolution of frequently used hostnames.

To edit your hostname search path, select the Host Name Search Path entry in the Client Tasks section of the netconf main menu and press Enter. The Host Name Search Path menu will be displayed (see Figure 13.11).

![](img/6c13bcf02a08ad7923caab46f051d96a_264_0.png)

In this screen, you use the arrow key to move up and down between entries in the menu and Enter to select a menu item. This screen presents a pre-defined list of possible paths. Use the up and down arrow keys to highlight your preferred path and press the spacebar to choose this path. Press Tab to highlight the Accept key and press Enter to return to the main menu.

### Completing Configuration

To complete configuration of your network, save your changes. Follow these steps:

1. On the main menu, press Tab to highlight the Quit button and press Enter. The menu illustrated in Figure 13.12 will be presented.
2. Select the Activate the Changes entry, press Tab to highlight the Quit button and press Enter.

The changes will be applied and activated and netconf will quit and return you to the command line. If you entered your network settings correctly, your network should be active.

**Figure 13.12**  
The status of the System menu.

![](img/6c13bcf02a08ad7923caab46f051d96a_265_0.png)

## MANUAL LINUX NETWORK CONFIGURATION

While tools such as netconf are useful for quickly editing your network configuration, they hide the actual Linux tools and commands that are used to configure and enable your network. In this section, we consider the techniques for manually enabling your network.

> **Note**
> 
> The examples here come from Red Hat Linux 6.2 but generalize to most versions of Linux. If you have problems using these techniques on a specific distribution, consult your distribution’s documentation.

There are five key steps in manual network configuration:

- Configure your network interface
- Specify your name servers
- Edit your local hosts file
- Define your routes
- Automate your network setup

> **Note**
> 
> This discussion assumes that the correct kernel module for your network card is already loading at boot time and is detected as `/dev/eth0`. If you are using a common card such as a 3COM card or an NE 2000-compatible card, this is a safe assumption with most modern distributions. Otherwise, consult Chapter 9, “Installing and Using RAID,” for a discussion of installing the modules for your network adapter.

> **Tip**
> 
> All the steps in this discussion should be performed as the root user. If you attempt to configure your network as a regular user, you are likely to encounter permissions problems at some point during the procedure.

### Configure Your Network Interface

When configuring your Linux system’s network support, the first step is to configure and enable your network interface. You do this with the ifconfig command.

Consider an example: Your network interface, eth0, is connected to the network 192.168.147.0 which has the network mask 255.255.255.0 and your system’s IP address is 192.168.147.5. To configure your interface to connect to this network, use the following command:

```bash
# /sbin/ifconfig eth0 192.168.147.5 netmask 255.255.255.0 up
```

You can test if this configuration was successful. Use the ifconfig command without any arguments or flags to display the state of any currently enabled network interfaces.

```text
# ifconfig
eth0      Link encap:Ethernet  HWaddr 00:20:AF:EB:41:69
          inet addr:192.168.147.5  Bcast:192.168.147.255  Mask:255.255.255.0
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:14583 errors:9 dropped:0 overruns:0 frame:9
          TX packets:521 errors:0 dropped:0 overruns:0 carrier:9
          collisions:6 txqueuelen:100
          Interrupt:10 Base address:0x300

lo        Link encap:Local Loopback
          inet addr:127.0.0.1  Mask:255.0.0.0
          UP LOOPBACK RUNNING  MTU:3924  Metric:1
          RX packets:8 errors:0 dropped:0 overruns:0 frame:0
          TX packets:8 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
```

If you have used the ifconfig command correctly to enable your network interface then you should see an entry for eth0 like the one shown in this example. It is common as well to have a section for the local loopback device (lo); this is normally pre-configured by your distribution when you install Linux. The local loopback device provides the mechanism by which network applications can talk to the local host without using an external network interface. Because many applications in Linux presume the existence of a network, it is generally necessary to have a loopback device enabled.

Once you know that ifconfig is able to configure your network interface correctly, you can test that your system can actually talk to your LAN by using the ping command to test connectivity to another host on your LAN. For instance, if you want to ping a host with the IP address 192.168.147.1, use the following command:

```bash
# ping 192.168.147.1
```

### Specify Your Name Servers

You can specify any DNS name servers you need to connect to the network or resolve names to IP addresses on your local network by creating entries in the `/etc/resolv.conf` file. Two key types of entries are needed in this file:

- **domain:** The domain entry specifies the domain name of your local network. For instance, if your local network has the domain name `juxta.com`, the first line of `resolv.conf` could be:

  `domain juxta.com`

- **nameserver:** The nameserver entry specifies the name of a DNS server. You need one entry for each DNS server you have available to use in the order of preference. Therefore, your primary name server should be listed first, the secondary server listed second and so on. For instance, if you have two name servers, a primary at 192.168.147.200 and a secondary at 192.168.147.201, then you would have two nameserver entries:

  `nameserver 192.168.147.200`
  `nameserver 192.168.147.201`

### Edit Your Local hosts File

As discussed earlier in this chapter when we covered configuring network in Red Hat Linux 6.2 using the `netconf` tool, most systems use a local `/etc/hosts` file as the first source of hostname to IP address mapping information.

To use this file, make sure that your name server search path is correctly configured. For instance, if you want name server lookups to first check your local hosts file and then attempt lookups against your DNS servers, then you need the following entry in the `/etc/host.conf` file:

```
order hosts,bind
```

This entry indicates that hosts lookups start with the hosts file and then move on to bind, the Berkeley Internet Name Daemon (or DNS).

Once the search path is defined, you need to create entries in the `/etc/hosts` file for those hosts which you frequently access. Each entry takes the following form:

```
`<IP address> <hostname> <alias> <alias> ...`
```

At a minimum, each entry needs the IP address and the primary hostname. In addition, you can specify one or more aliases which represent alternate names for the host in question. For instance, consider the following series of entries from an `/etc/hosts` file:

```
127.0.0.1       localhost.localdomain    localhost
192.168.147.30  linux.juxta.com           linux
192.168.147.50  foo.juxta.com
```

The first entry provides a mapping for the local loopback address. The second entry maps a host on the local domain with two names (`linux.juxta.com` and `linux`) pointing to `192.168.147.30`. The final entry points the hostname `foo.juxta.com` to `192.168.147.50`.

### DEFINE YOUR ROUTES

To access hosts on your network, define the necessary routes so that your Linux system knows how to direct packets. At a minimum, you will want the following two routes defined for your system:

- A route specifying that your local machine is accessed through your loopback device.
- A route specifying that all packets destined for your local network need to be sent out through a particular network interface (`eth0` in the examples in this chapter).

Routes are defined using the `route` command. To specify a route to a particular host, use the following syntax:

```
route add -host <IP Address or host name> <device>
```

For instance, to create a route to the local host (with the IP address `127.0.0.1`) through the loopback network device, use the following command:

```
# /sbin/route add -host 127.0.0.1 lo
```

Adding a route to a network uses a similar syntax:

```
route add -net <network address> netmask <network mask> <device>
```

For instance, in our manual configuration examples, your system is connected to the network `192.168.147.0` with the network mask `255.255.255.0`. To define a route to this network through the device `eth0`, use the command:

```
# /sbin/route add -net 192.168.147.0 netmask 255.255.255.0 eth0
```

Finally, if your LAN is connected through a router to an external network such as the Internet, you need to define your default gateway to this external network. To do this, use the route command with the following syntax:

```
route add default gw <IP address or host name> <device>
```

For instance, if your LAN’s default gateway is `192.168.147.1` you would use the following command to direct packets for hosts on external networks to this host through the `eth0` device:

```
# /sbin/route add default gw 192.168.147.1 eth0
```

After configuring your routes, you can display a table of defined routes using the route command with no arguments or flags:

```
 # /sbin/route
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
192.168.147.0   *               255.255.255.0   U     0      0      0   eth0
127.0.0.0       *               255.0.0.0       U     0      0      0   lo
default         192.168.147.1   0.0.0.0         UG    0      0      0   eth0
```
