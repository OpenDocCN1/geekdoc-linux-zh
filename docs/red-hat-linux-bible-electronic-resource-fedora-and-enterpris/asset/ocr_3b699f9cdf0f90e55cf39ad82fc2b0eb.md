| Option | Description |
| :--- | :--- |
| **mode** *option* | Sets the mode used for communications to Ad-hoc, Managed, Master, Repeater, Secondary, or Auto. |
| **nick** *name* | Sets the station name to define this particular computer. |
| **rate** *XXX* | Defines the transmission rate to use. |
| **rts** *number* | Sets the RTS/CTS threshold for packet transmission. |
| **retry** *number* | For cards that support MAC retransmissions, you can use this option to determine how many retries are made before the transmission fails. The value can be a number (indicating number of seconds allotted for retries), or a number followed by an m (for milliseconds) or u (for microseconds). Instead of a number, you can set a number of retries using the limit parameter. For example: retry limit 100 indicates that the transmission can retry up to 100 times. |
| **sens** *number* | Sets the lowest possible sensitivity threshold for which the wireless interface will try to receive a packet. Raising this level can help block out interference from other wireless LANs that might weakly encroach on your transmission area. |

The best place to add `iwconfig` options permanently in Red Hat Linux is the configuration file for your wireless interface in the `/etc/sysconfig/network-scripts` directory.

Options to `iwconfig` are added to the wireless interface file (such as `ifcfg-eth0` or `ifcfg-eth1`) using the `IWCONFIG` parameter. For example, to add an encryption-key value of `1234-1234-12` for your wireless LAN card, you could add the following line to your wireless-interface file:

```
IWCONFIG="key 1234-1234-12"
```

# ## Understanding IP Addresses

Whether you are using a wired or a wireless network, each computer you communicate with (including yours) must have a unique address on the network. In TCP/IP, each computer must be assigned an IP address. This section gives you some background in IP addresses.

There are two basic ways to assign a host name and IP address to a network interface in Linux:

+   *   **Static addresses** — With static IP addresses, each computer has an IP address that doesn't change each time the computer reboots or restarts its network interface. Its IP