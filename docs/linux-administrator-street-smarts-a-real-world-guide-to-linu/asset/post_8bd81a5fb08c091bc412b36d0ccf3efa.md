
your kernel, building the correct driver into the main kernel file will also ensure that it's loaded at system startup.

If your network hardware isn't correctly detected, though, subsequent configuration (as described in the upcoming sections “**DHCP Configuration**” and “Static IP Address Configuration”) won't work. To correct this problem, you must load your network hardware driver. You can do this with the **modprobe** command:

```bash
# modprobe tulip
```

You must know the name of your network hardware's kernel module, though (*tulip* in this example). If you're not sure of your network hardware's driver name, consult Task 6.1 and Phase 2.

## DHCP Configuration

One of the easiest ways to configure a computer to use a TCP/IP network is to use **DHCP**, which enables one computer on a network to manage the settings for many other computers. It works like this: When a computer running a **DHCP** client boots up, it sends a broadcast in search of a **DHCP** server. The server replies (using nothing but the client's hardware address) with the configuration information the client needs to enable it to communicate with other computers on the network— most importantly the client's IP address and netmask and the network's gateway and DNS server addresses. The **DHCP** server may also give the client a hostname. The client then configures itself with these parameters. The IP address is not assigned permanently; it's referred to as a **DHCP lease**, and if it's not renewed, the **DHCP** server may give the lease to another computer. Therefore, from time to time the client checks back with the **DHCP** server to renew its lease.

Three **DHCP** clients are in common use on Linux: *pump*, *dhclient*, and *dhcpd* (not to be confused with the **DHCP** server, *dhcpd*). Some Linux distributions ship with just one of these, but others ship with two or even all three. All distributions have a default **DHCP** client, though—the one that's installed when you tell the system you want to use **DHCP** at system installation time. Those that ship with multiple **DHCP** clients typically enable you to swap out one for another simply by removing the old package and installing the new one.

Ideally, the **DHCP** client runs at system startup. This is usually handled either by its own SysV startup file, as described in Phase 3, “Managing Software”, or as part of the main network configuration startup file (typically a SysV startup file called *netconf* or *networking*). To enable networking when the computer next boots, use *chkonfig*, *rc-update*, *ntsysv*, or another tool (as described in Phase 3) to activate the network or networking script in your default runlevel:

```bash
# chkconfig --add network
```

This command adds the *network* script to the current runlevel, if it's not already active. As described in Phase 3, the details of SysV init script configuration vary from one distribution to another, so you may need to adjust this command.

The system often uses a line in a configuration file to determine whether to run a **DHCP** client. For instance, Red Hat and Fedora Linux set this option in a file called */etc/sysconfig/network-scripts/ifcfg-eth0* (this filename may differ if you use something other than a single Ethernet interface). The line in question looks like this:

```bash
BOOTPROTO=dhcp
```

If the BOOTPROTO variable is set to something else, changing it as shown here will configure the system to use DHCP. It's usually easier to use a GUI configuration tool to set this option, however. Such tools include Network Configuration (aka system-config-network) in Red Hat and Fedora, and YaST and YaST2 in openSUSE.

> If you don't know where the relevant configuration line is found, try searching the /etc/sysconfig or /etc/conf.d directories, if they're present. Chances are you'll find configuration files with fairly obvious names. You can use grep to search these directories, or all of /etc if necessary, for files that refer to DHCP or your network interface.

Once a DHCP client is configured to run when the system boots, the configuration task is done—at least if everything works as it should. On very rare occasions, you may need to tweak DHCP settings to work around client/server incompatibilities or to have the DHCP client do something unusual. Consult the man page for your DHCP client if you need to make changes. You'll then have to modify its SysV startup script or a file to which it refers in order to change its operation.

If you want to bring the network up without rebooting the computer, you can call the SysV script directly:

```bash
# /etc/init.d/network start
```

As described in Phase 3, the exact path to the SysV startup scripts vary from one distribution to another. If your network was already working, but didn't use DHCP, you may need to pass the stop parameter to the script before you can pass it the start parameter.

## Static IP Address Configuration

If a network lacks a DHCP server, you must provide basic network configuration options manually. Static IP address configuration is also useful for computers that require a constant IP address, such as servers. You can set these options using interactive commands, as described shortly, but to set them in the long term, you adjust a configuration file such as /etc/sysconfig/network-scripts/ifcfg-eth0. Listing 6.1 shows a typical ifcfg-eth0 file, configured to use a static IP address. (Note that this file's exact location and name may vary from one distribution to another.)

### Listing 6.1: A Sample Network Configuration File

```ini
DEVICE=eth0
BOOTPROTO=static
IPADDR=192.168.29.39
NETMASK=255.255.255.0
NETWORK=192.168.29.0
BROADCAST=192.168.29.255
GATEWAY=192.168.29.1
ONBOOT=yes
```

Several specific items are required, or at least helpful, for static IP address configuration:

- **IP address**: You can set the IP address manually via the `ifconfig` command (described in more detail shortly) or via the IPADDR item in the configuration file.
- **Network mask**: The netmask can be set manually via the `ifconfig` command or via the NETMASK item in a configuration file.
- **Gateway address**: You can manually set the gateway (that is, your LAN's router) via the `route` command. To set it permanently, you need to adjust a configuration file, which may be the same configuration file that holds other options or another file, such as /etc/sysconfig/network/routes. In either case, the option is likely to be called GATEWAY. The gateway isn't necessary on a system that isn't connected to a wider network—that is, if the system works only on a local network that contains no routers.
- **DNS settings**: In order for Linux to use DNS to translate between IP addresses and hostnames, you must specify at least one DNS server in the /etc/resolv.conf file. Precede the IP address of the DNS server by the keyword nameserver, as in `nameserver 192.168.29.1.` You can include up to three nameserver lines in this file. Adjusting this file is all you need to do to set the name server addresses; you don't have to do anything else to make the setting permanent.

The network configuration script may hold additional options, but most of these are related to others. For instance, Listing 6.1 has an option specifying the interface name (DEVICE=eth0), another that tells the computer to assign a static IP address (BOOTPROTO=static), and a third to bring up the interface when the computer boots (ONBOOT=yes). The NETWORK and BROADCAST items in Listing 6.1 are derived from the IPADDR and NETMASK items, but you can change them if you understand the consequences.

If you aren't sure what to enter for the basic networking values (the IP address, network mask, gateway address, and DNS server addresses), you should consult your network administrator. Do not enter random values or values you make up that are similar to those used by other systems on your network. Doing so is unlikely to work at all, and it could conceivably cause a great deal of trouble—say, if you mistakenly use an IP address that's reserved for another computer.

As just mentioned, the ifconfig program is critically important for setting both the IP address and netmask. This program can also display current settings, as described earlier in "Understanding Network Addressing" in Task 6.1. As an example of using ifconfig to bring up a network interface, the following command brings up eth0 (the first Ethernet card) using the address 192.168.29.39 and the netmask 255.255.255.0:

```bash
# ifconfig eth0 up 192.168.29.39 netmask 255.255.255.0
```

This command links the specified IP address to the card so that the computer will respond to the address and claim to be that address when sending data. It doesn't, though, set up a route for traffic beyond your current network. For that, you need to use the `route` command:

```bash
# route add default gw 192.168.29.1
```
