To use **iwconfig**, you pass it the relevant data using option names such as **ssid** and **channel**, preceded by the wireless network device name (typically **wlan0**):

```
# iwconfig wlan0 ssid NoWires channel 1 mode Managed key s:N1mP7miNww
```

This example sets the options for **wlan0** to use the managed network on channel 1 with the SSID of **NoWires** and a password of **N1mP7miNww**. The password requires a few extra comments. Ordinarily, **iwconfig** takes a password as a string of hexadecimal values, with optional dashes between 2-byte blocks, as in 0123-4567-89AB. Often, however, the password is given as a text string. The string *s:* must precede the password in this case, as shown in the example.

For details on additional **iwconfig** options, including some highly technical ones, consult its man page.

Once you’ve configured a wireless interface, you can check on its settings by using **iwconfig** with no options or with only the interface name:

```
# iwconfig wlan0
wlan0	IEEE 802.11g  ESSID: 'NoWires'
	Mode:Managed  Frequency:2.462 GHz  Access Point: 08:10:74:24:1B:D4
	Bit Rate=54 Mb/s  Tx-Power=27 dBm
	Retry min limit:7  RTS thr:off  Fragment thr=2352 B
	Encryption key: 314E-506D-6d37-4E48-0A [2]
	Link Quality=100/100  Signal level=-32 dBm  Noise level=-94 dBm
	Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:0
	Tx excessive retries:0  Invalid misc:0  Missed beacon:0
```

In addition to providing information on settings, **iwconfig** provides some diagnostic information, such as the link quality, received (Rx) and transmitted (Tx) errors, and so on.

# DHCP Configuration

One of the easiest ways to configure a computer to use a TCP/IP network is to use **DHCP**, which enables one computer on a network to manage the settings for many other computers. It works like this: when a computer running a **DHCP** client boots up, it sends a broadcast in search of a DHCP server. The server replies (using nothing but the client’s hardware address) with the configuration information needed for the client needs to allow it to communicate with other computers on the network—most importantly the client’s IP address and netmask and the network’s gateway and DNS server addresses. The DHCP server may also give the client a hostname. The client then configures itself with these parameters. The IP address is not assigned permanently; it’s referred to as a *DHCP lease*, and if it’s not renewed, the DHCP server may give the lease to another computer. Therefore, from time to time, the client checks back with the DHCP server to renew its lease.

Three DHCP clients are in common use on Linux: **pump**, **dhclient**, and **dhcpcd** (not to be confused with the DHCP server, **dhcpd**). Some Linux distributions ship with just one of