# Configuring Wireless Networking 317

```
DHCP_HOSTNAME=
NAME=
ESSID="HOME"
CHANNEL=6
MODE=Managed
RATE=auto
```

The encryption key is stored separately. For an wireless Ethernet card whose device name is eth1, the encryption key is stored in the /etc/sysconfig/network-scripts/keys-eth1 file. For example, here is the text for this file may:

```
KEY=AECFFAA0F03
```

Note that the key has 16 hexadecimal digits for a 40-bit key (for example, 1fdf-3de-fe) or 26 hexadecimal digits for a 104-bit key. The keys are in, 64-bit and 128-bit, but the encryption algorithm automatically generates 24 bits of the key, so you need to specify only the remaining bits. Needless to say, the longer key, the more secure the encryption.

If you manually edit the parameters in the wireless Ethernet configuration, type the following command to reactivate the wireless network interface after editing the configuration file:

```
service pcmia restart
```

| Table 3-1 Settings in Configuration File for a Wireless Ethernet Network Interface |
| This Parameter | Means the Following |
n| BOOTPROTO | The name of the protocol to use to get the IP address for the interface. It is either dhcp or boost for Ethernet interface. |
| CHANNEL | Channel number (between 1 and 14 in United States and Canada). Must be the same as that for the wireless access point. In Managed mode, you don't need to specify the channel. |
| DEVICE | The device name for the wireless network interface (eth0) for the first interface, eth1 for second, and so on. |
| ESSID | Extended Set (ESS) Identifier, also known as the wireless network name. It is case sensitive and must be the same as the name specified for the wireless access point. Provide the name within single quotes (for example, 'HOME'). |
| HWADDR | The hardware address (also called the MAC address) of the wireless network card (six pairs of colon-separated hexadecimal numbers, for example, 00:02:2d:8c:f9:c4). The wireless card's driver automatically detects this address. |

(continued)