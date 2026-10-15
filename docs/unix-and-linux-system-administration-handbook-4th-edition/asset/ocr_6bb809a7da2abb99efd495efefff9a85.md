To be fair, **mktcpip** does more than just set device configuration parameters—it also runs the **rc.tcpip** script to start relevant network daemons.

SMIT’s network configuration facilities are relatively complete, so you can, and should, rely on SMIT for most basic configuration. Look under the “Communications Applications and Services” topic for TCP/IP configuration options.

Most sysadmins will never need to operate below the level of **chdev/lsattr** et al. However, this layer can be useful for seeing the authoritative list of configuration options for a device. For example, the following query shows the configurable parameters for the network interface **en3**:

```
aix$ lsattr -H -E -l en3
```

| attribute | value | description | settable |
|---|---|---|---|
| alias4 |  | IPv4 Alias including Subnet Mask | True |
| alias6 |  | IPv6 Alias including Prefix Length | True |
| arp | on | Address Resolution Protocol (ARP) | True |
| authority |  | Authorized Users | True |
| broadcast | 192.168.10.255 | Broadcast Address | True |
| mtu | 1500 | Maximum IP Packet Size | True |
| netaddr | 192.168.10.11 | Internet Address | True |
| netaddr6 |  | IPv6 Internet Address | True |
| netmask | 255.255.255.0 | Subnet Mask | True |
| prefixlen |  | Prefix Length for IPv6 Address | True |
| remmtu | 576 | Max. Packet Size for REMOTE Nets | True |
| security | none | Security Level | True |
| state | up | Current Interface Status | True |
| tcp_mssdflt |  | Set TCP Maximum Segment Size | True |
| tcp_nodelay |  | Enable/Disable TCP_NODELAY Option | True |
| tcp_recvspace |  | Set Socket Buffer Space for Receiving | True |
| tcp_sendspace |  | Set Socket Buffer Space for Sending | True |

The **-H** option asks for the output columns to be labeled, the **-E** option requests current (“effective,” as opposed to default) values, and the **-l** option identifies the device to probe. Many of the devices that **chdev** et al. can operate on have no entries in **/dev**. You can run **lsdev -C** to see a complete list of the available devices.

To set a value, use **chdev**. For example, to set the MTU for **en3** above to 1450, you could use the command

```
aix$ sudo chdev -l en3 -a mtu=1450
```

# no: manage AIX network tuning parameters

AIX breaks out its system-wide TCP/IP options into a separate, parallel world of persistent attribute/value pairs that are accessed through the **no** command rather than through **chdev**. (The difference is that **no** is for system-wide configuration, whereas **chdev** configures instances of specific drivers or devices.)