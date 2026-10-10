your kernel, building the correct driver into the main kernel file will also ensure that it's loaded at system startup.

If your network hardware isn't correctly detected, though, subsequent configuration (as described in the upcoming sections “**DHCP Configuration**” and “Static IP Address Configuration”) won't work. To correct this problem, you must load your network hardware driver. You can do this with the **modprobe** command:

```
# modprobe tulip
```

You must know the name of your network hardware's kernel module, though (*tulip* in this example). If you're not sure of your network hardware's driver name, consult Task 6.1 and Phase 2.

# ## DHCP Configuration

One of the easiest ways to configure a computer to use a TCP/IP network is to use **DHCP**, which enables one computer on a network to manage the settings for many other computers. It works like this: When a computer running a **DHCP** client boots up, it sends a broadcast in search of a **DHCP** server. The server replies (using nothing but the client's hardware address) with the configuration information the client needs to enable it to communicate with other computers on the network— most importantly the client's IP address and netmask and the network's gateway and DNS server addresses. The **DHCP** server may also give the client a hostname. The client then configures itself with these parameters. The IP address is not assigned permanently; it's referred to as a **DHCP lease**, and if it's not renewed, the **DHCP** server may give the lease to another computer. Therefore, from time to time the client checks back with the **DHCP** server to renew its lease.

Three **DHCP** clients are in common use on Linux: *pump*, *dhclient*, and *dhcpd* (not to be confused with the **DHCP** server, *dhcpd*). Some Linux distributions ship with just one of these, but others ship with two or even all three. All distributions have a default **DHCP** client, though—the one that's installed when you tell the system you want to use **DHCP** at system installation time. Those that ship with multiple **DHCP** clients typically enable you to swap out one for another simply by removing the old package and installing the new one.

Ideally, the **DHCP** client runs at system startup. This is usually handled either by its own SysV startup file, as described in Phase 3, “Managing Software”, or as part of the main network configuration startup file (typically a SysV startup file called *netconf* or *networking*). To enable networking when the computer next boots, use *chkonfig*, *rc-update*, *ntsysv*, or another tool (as described in Phase 3) to activate the network or networking script in your default runlevel:

```
# chkconfig --add network
```

This command adds the *network* script to the current runlevel, if it's not already active. As described in Phase 3, the details of SysV init script configuration vary from one distribution to another, so you may need to adjust this command.

The system often uses a line in a configuration file to determine whether to run a **DHCP** client. For instance, Red Hat and Fedora Linux set this option in a file called */etc/sysconfig/network-scripts/ifcfg-eth0* (this filename may differ if you use something other than a single Ethernet interface). The line in question looks like this:

```
BOOTPROTO=dhcp
```