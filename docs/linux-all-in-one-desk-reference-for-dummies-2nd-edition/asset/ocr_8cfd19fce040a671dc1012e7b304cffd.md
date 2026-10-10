| This Parameter | Means the Following |
| --- | --- |
| IPV6INIT | When set to *yes*, this parameter initializes IPv6 configuration for the wireless interface. Set it to *no* if you are not using IPv6. |
| MODE | The mode of operation of the wireless network card. Set to **Managed** for a typical network that connects through a wireless access point. |
| NAME | A nickname for your wireless network. If you don't specify it, the host name is used as the nickname. |
| ONBOOT | Set to *yes* to activate the wireless interface at boot time; otherwise, set to *no*. |
| PEERDNS | Set to *yes* to enable the interface to modify your system's */etc/resolv.conf* file to use the DNS servers obtained from the DHCP server (the same server that provides the IP address for the interface). If you set this parameter to *no*, the */etc/resolv.conf* file is left unchanged. |
| RATE | Bit rate for the wireless connection (set to one of the following options: 1M, 2M, 5.5M, 11M, or *auto*). The M means Mbps or a million bits per second. Set to *auto* to use the maximum possible transmission rate. |
| TYPE | Set to **Wireless** for wireless network interface. |
| USERCTL | When set to *yes*, a non-root user can control the device. Set it to *no* so that only *root* can control the device. |

In SUSE Linux, use YaST to configure the wireless network. SUSE stores the wireless configuration parameters in a file whose name begins with **ifcfg-wlan**, followed by a number such as **0** or **1**, depending on the sequence number of the wireless network interface. The configuration file is stored in the */etc/sysconfig/network* directory. Here is a typical list of wireless configuration parameters from a configuration file in SUSE Linux:

```
```
WIRELESS_MODE='Managed'
WIRELESS_ESSID='HOME'
WIRELESS_NICK=''
WIRELESS_RATE='auto'
WIRELESS_AUTH_MODE='open'
WIRELESS_KEY_0='0123-4567-89'
```
```

![](bbox=[0.15, 0.73, 0.24, 0.82])

To check the status of the wireless network interface, type the following command:

```
`iwconfig`
```