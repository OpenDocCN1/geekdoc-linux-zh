
This procedure creates an interface configuration file in your `/etc/sysconfig/network-scripts` directory. The name of the configuration file is `ifcfg-` followed by the interface name (such as `eth0`, `eth1`, and so on). So, if your wireless card is providing your only network interface, it might be called `ifcfg-eth0`.

Using any text editor, open the `ifcfg-eth?` file (replacing `?` with the interface number) as root user. The following is an example of an `ifcfg-eth1` file:

```
# Please read /usr/share/doc/initscripts-*/sysconfig.txt
# for the documentation of these parameters.
ONBOOT=no
USERCTL=no
PEERDNS=no
GATEWAY=10.0.1.1
TYPE=Wireless
DEVICE=eth1
HWADDR=00:02:2d:2e:8c:a8
BOOTPROTO=none
NETMASK=255.255.255.0
IPADDR=10.0.1.2
DOMAIN=
ESSID=
CHANNEL=1
MODE=Ad-Hoc
RATE=11Mb/s
NETWORK=10.0.1.0
BROADCAST=10.0.1.255
```

In this example, the wireless card's hardware (MAC) address is automatically set to `00:02:2d:2e:8c:a8`. (Your MAC address will be different.) The interface is not yet set to come up at boot time (`ONBOOT=no`). The interface device is `eth1` (which matches the interface filename `ifcfg-eth1`) because this particular computer has another Ethernet card on the `eth0` interface. The interface type is set to `Wireless`.

Other information in the file sets standard TCP/IP address information. The `NETMASK` is set to `255.255.255.0` and the `IP` address for the card is set to `10.0.1.1`. The broadcast address is `10.0.1.255`.

You can also set many options that are specific to your wireless network in this file. The following list explains some additional options that you might want to set:

- **NWID** — Identifies the name of this particular computer on the network. The computer’s hostname (determined from the `uname -n` command) is used by default if you don’t set it with NWID.
- **FREQ** — You can choose a particular frequency in which to transmit. No value is required because selecting a channel implies a certain frequency. If you do enter a frequency, the value must be a number followed by a `k` (kilohertz), `M` (megahertz), or `G` (gigahertz). The default values for the channels you select range from 2.412G (channel 1) to `2.484G` (channel 14), with other channels occurring at increments of .005G. The default is `2.422G`.
- **SENS** — You can select the sensitivity level of the access point. SENS can be set to 1 (low density), 2 (medium density), or 3 (high density). The default is 1. The `sensitivity threshold` has an impact on roaming.

> **CAUTION:** The encryption algorithm used with 802.11 networks is the Wired Equivalent Privacy (WEP) algorithm. Although using the encryption key is more secure than not using it, experts feel that WEP has some inherent flaws that might allow a drive-by hacker to decrypt your wireless LAN traffic. For that reason, I strongly recommend using additional techniques to protect your wireless LANs, such as firewalls and diligent log-checking. See the “Wireless Security” sidebar for further information. (If your wireless card supports WPA encryption standards, use those as they are more secure than WEP.)

Besides those options just shown, you can also pass any valid options to the `iwconfig` command (which actually interprets these values) by adding an IWCONFIG option to the configuration file. Display the `iwconfig` man page (`man iwconfig`) to see all wireless options. Also view the `/etc/sysconfig/network-scripts/ifup-wireless` script to see how the options you just added are processed.

Repeat the configuration procedure for each wireless Fedora computer on your LAN. At this point, your wireless network should be ready to go. Restart your network, as described in the following steps, to make sure that it is working.

## Checking your wireless connection

Your wireless LAN interface should be operating at this point. If another wireless computer is available on your wireless network, try communicating with it using the `ping` command and its IP address (as described in the section “Can you reach another computer on the LAN?” later in this chapter).

If you are not able to communicate with other wireless nodes or if transmission is slow, you may have more work to do. For example, if you see messages that say “Destination Host Unreachable,” instead of the output shown earlier, refer to the section on “Troubleshooting a wireless LAN” for help. Some access points will not allow you to communicate with other wireless clients, so double-check your AP’s settings or try pinging the AP itself.

## Testing distances

Although you may be thrilled to have a wireless LAN working between two computers, you will probably want these computers to be located some distance from each other to make the LAN useful. Getting your wireless LAN to work at the desired distances can be quite a challenge. See the section “Selecting antennas” earlier in this chapter for suggestions on selecting and using antennas to configure the type of wireless LAN you are interested in.

## Wireless Security

The Wireless Ethernet Compatibility Alliance (WECA) has recommended changes in response to security concerns about wireless networks. They did this because, unlike wired networks, which can often be physically protected within a building, wireless networks often extend beyond physical boundaries that can be protected.

The Wireless Equivalent Privacy (WEP) standard adds encryption to the 802.11 wireless standard. WECA refers to it as its way of providing “walls” that make wireless Ethernet as secure as wired Ethernet. However, you need to implement WEP, as well as other security methods that would apply to any computer network, in order to make your wireless network secure. Here are WECA’s suggestions:

- Change the default WEP encryption key on a regular basis (possibly weekly or even daily). This prevents casual drive-by hackers from reading your encrypted transmissions.
- Use password protection on your drives and folders.
- Change the default Network Name (SSID).
- Use session keys, if available in your product (session keys are not supported in current Linux wireless drivers).
- Use MAC address filtering (supported in a limited way in Linux).
- Don’t broadcast from the access point, if possible.
- Use a VPN (Virtual Private Network) system, which can add another layer of encryption beyond that which is available on your wireless network.

For larger organizations requiring greater security, WECA suggests such features as firewalls and user-verification schemes (such as Kerberos). As I mentioned earlier in this chapter, features for protecting from intrusions and restricting services are already built into Fedora. Refer to the descriptions of security tools in Chapters 13, 14, and 15 for methods of securing your network, its computers, and their services. In particular, you could consider adding a VPN to further secure all data sent on your wireless LAN.

Wi-Fi Protected Access (WPA) features are available for most wireless cards in Linux. The software for implementing WPA, wpa_supplicant, is used by NetworkManager to connect to a WPA-enabled access point.

## Setting wireless extensions

After the wireless module is loaded, you can change wireless extensions using the **iwconfig** command. The **iwconfig** command is the command that is actually used to set the options added to the **ifcfg** configuration script (for example, for the eth1 interface, the script would be /etc/sysconfig/network-scripts/ifcfg-eth1).

Some of the same options that you set when the module was loaded can be reset using the `iwconfig` command. The `iwconfig` command can be useful for testing different settings on an active wireless LAN. The syntax of the `iwconfig` command is as follows:

```
# iwconfig interface parameter value
```

The `interface` is the name of the wireless interface you want to change, such as `eth1` or `wlan0`. The `parameter` is the name of the option, and the `value` is replaced by its value. For example, to set your network name (also called `ESSID`, or Extended Service Set Identifier) to Homelan, you could type the following as root user:

```
# iwconfig eth0 essid "Homelan"
```

Table 14-2 contains a list of available options for the `iwconfig` command. Refer back to the section “Configuring the wireless interface” for further details on these options.

### Table 14-2: Options for the iwconfig Command

| Option | Description |
| :--- | :--- |
| `essid` `name` | Indicates the network name. |
| `ap` `address` | Indicates that the access point is at a particular MAC address. For low-quality connections, the client driver may return to trying to automatically detect the access point. This setting is useful in Managed mode only. |
| `channel` `#` | Picks the channel number to operate on. |
| `frag` `frag_size` | Sets the fragmentation threshold for splitting up packets before they are transmitted. |
| `freq` `2.4??g` | Sets the frequency of the channel to communicate on. |
| `key` `xxxx-xxxx-xx` | Sets the key used for WEP encryption. |
| `mode` `option` | Sets the mode used for communications to Ad-hoc, Managed, Master, Repeater, Secondary, or Auto. |
| `nick` `name` | Sets the station name to define this particular computer. |
| `rate` `XXM` | Defines the transmission rate to use. |
| `rts` `number` | Sets the RTS/CTS threshold for packet transmission. |
| `retry` `number` | For cards that support MAC retransmissions, you can use this option to determine how many retries are made before the transmission fails. The value can be a number (indicating number of seconds allotted for retries), or a number followed by an `m` (for milliseconds) or a `u` (for microseconds). Instead of a number, you can set a number of retries using the `limit` parameter. For example: `retry limit 100` indicates that the transmission can retry up to 100 times. |
