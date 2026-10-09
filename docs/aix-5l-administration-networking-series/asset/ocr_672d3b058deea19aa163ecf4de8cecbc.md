# # Network Interface Configuration

As stated in the preceding section, if you use the Minimum Configuration & Startup SMIT panel to configure TCP/IP, the default interface is already configured for you. Additional network interfaces may be configured using SMIT FastPath smit chinet or by using the **ifconfig** command. The same command can be used to change the addresses or masks of an adapter, should you need to make changes to the network configuration. Please note that if you use the **ifconfig** command, your modification is in effect only for the current instance of the running system. In other words, it will not be persistent across a system reboot unless you add an **ifconfig** entry in the /etc/rc.net startup script. However, this is not the recommended method because, depending on the order of execution, you may get unexpected results.

The adapter interface can be brought up and down for maintenance or testing using SMIT or from the command line using the **ifconfig** command. Note that this will interrupt service to the target interface and may affect dependent applications.

```
# ifconfig en0 up
# ifconfig en0 down
# ifconfig en0 detach
```

The following is an example of using **ifconfig** to assign address 123.145.100.18 to the Standard Network Interface with a netmask of 0xffffff00 and the broadcast address of 123.145.100.255.

```
# ifconfig en0 123.145.100.18 netmask 0xffffff00 broadcast 123.145.100.255
```

# # arp Command

The **arp** command can be used to view and configure the ARP table in AIX 5L. **arp -a** will display all entries in the ARP table. Incomplete entries will be shown for addresses for which ARP requests have been sent but no reply has yet been received. Normally, it is not necessary to edit the ARP table by hand; but in a few special circumstances, it may be necessary—for instance, if a system on the network does not respond to ARP requests, or if an adapter in the network has been replaced and it is necessary to delete an old ARP entry.

```
# arp -a
```

# # autoconf6 Command

Running the **autoconf6** command is the first step in configuring a system to use the IPv6 protocol. IPv6 requires that each network interface have a link local address that can be used to communicate with routers and other hosts on the local network link. **autoconf6** automatically generates and assigns a link local address on each interface that is already configured with an IPv4 address. In addition, it will create the si10