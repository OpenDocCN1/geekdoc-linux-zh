| Option | Description |
| --- | --- |
| nick name | Sets the station name to define this particular computer. |
| rate XXM | Defines the transmission rate to use. |
| rts number | Sets the RTS/CTS threshold for packet transmission. |
| retry number | For cards that support MAC retransmissions, you can use this option to determine how many retries are made before the transmission fails. The value can be a number (indicating number of seconds allotted for retries), or a number followed by an m (for milliseconds) or u (for microseconds). Instead of a number, you can set a number of retries using the limit parameter. For example: retry limit 100 indicates that the transmission can retry up to 100 times. |
| sens number | Sets the lowest possible sensitivity threshold for which the wireless interface will try to receive a packet. Raising this level can help block out interference from other wireless LANs that might weakly encroach on your transmission area. |

The best place to add iwconfig options permanently in Red Hat Linux systems is the configuration file for your wireless interface in the /etc/sysconfig/network-scripts directory.

Options to iwconfig are added to the wireless-interface file (such as ifcfg-eth0 or ifcfg-eth1) using the IWCONFIG parameter. For example, to add an encryption-key value of 1234-1234-12 for your wireless LAN card, you could add the following line to your wireless-interface file:

```
IWCONFIG="key 1234-1234-12"
```

# ### Troubleshooting a wireless LAN

If you set up your two (or more) wireless LAN cards in order for Red Hat Linux systems to communicate, and they are not communicating, you can troubleshoot the problem in several different ways.