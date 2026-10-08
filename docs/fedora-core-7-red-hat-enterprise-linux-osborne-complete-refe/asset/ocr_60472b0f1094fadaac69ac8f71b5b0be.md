| Parameter | Description |
| :------- | :------- |
| essid | A network name |
| freq | The frequency of the connection |
| channel | The channel used |
| nwid or domain | The network ID or domain |
| mode | The operating mode used for the device, such as Ad Hoc, Managed, or Auto. Ad Hoc = one cell with no access point; Managed = network with several access points and supports roaming; Master = the node is an access point; Repeater = node forwards packets to other nodes; Secondary = backup master or repeater; Monitor = only receives packets |
| sens | The sensitivity, the lowest signal level at which data can be received |
| key or enc | The encryption key used |
| frag | Cut packets into smaller fragments to increase better transmission |
| bit or rate | Speed at which bits are transmitted. The auto option automatically falls back to lower rates for noisy channels. |
| ap | Specify a specific access point |
| power | Power management for wakeup and sleep operations |

TABLE 5-3 Commonly Used Parameters

You can also use iwconfig to display statistics for your wireless devices, just as ifconfig does. Enter the iwconfig command with no arguments or with the name of the device. Information such as the name, frequency, sensitivity, and bit rate is listed. Check also /proc/net/wireless for statistics.

Instead of using iwconfig directly to set parameters, you can specify them in the wireless device’s configuration file. The wireless device configuration file will be located in the /etc/sysconfig/network-scripts directory and given a name like ifcg-eth1, depending on the name of the device. This file will already contain many iwconfig settings. Any further setting can be set by assigning iwconfig values to the IWCONFIG parameter as shown here:

```
IWCONFIG="rate 11M"
```

# iwpriv

The iwpriv command works in conjunction with iwconfig, allowing you set options specific to a particular kind of wireless device. With iwpriv, you can also turn on roaming or select the port to use. You use the private-command parameter to enter the device-specific options. The following example sets roaming on:

```
iwpriv eth0 roam on
```