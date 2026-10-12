
![](img/1744bde8c889adfab3fc911e1687fecf_651_0.png)

**Figure 15-12:** The Orinoco Silver wireless LAN card can be used with a PCI adapter (shown here).

## Checking that the cards are working

If the modules have been loaded properly, the cardmgr should recognize each card and start up the Ethernet interface for it. To check that this has happened, restart the interface as follows:

```bash
# /etc/init.d/pcmcia restart
Shutting down PCMCIA services: cardmgr modules.
Starting PCMCIA services: modules cardmgr.
```

Check the `/var/log/messages` file. You should see some messages at or near the end of this file, describing what happened when the PCMCIA interface was shut down and restarted. If the card starts successfully, these messages will give you a wealth of information, such as the MAC address of the card, a list of valid channels, and the name of the interface associated with the card. Here are some examples:

```text
May 4 10:21:12 nsl kernel: PCI: Enabling device 01:09.0 (0000 -> 0002)
May 4 10:21:12 nsl kernel: PCI: Assigned IRQ 5 for device 01:09.0
May 4 10:21:12 nsl kernel: PCI: Sharing IRQ 5 with 00:1f.3
May 4 10:21:12 nsl kernel: Yenta IRQ list 0000, PCI irq5
May 4 10:21:12 nsl kernel: Socket status: 10000011
...
May 4 10:21:23 nsl cardmgr[1935]: starting, version is 3.1.22
May 4 10:21:23 nsl cardmgr[1935]: initializing socket 0
May 4 10:21:23 nsl kernel: cs: memory probe 0xa0000000-0xa0ffffff: clean
May 4 10:21:23 nsl cardmgr[1935]: socket 0: Lucent Technologies
WaveLAN/IEEE Adapter
May 4 10:21:23 nsl cardmgr[1935]: executing: 'modprobe orinoco_cs'
May 4 10:21:23 nsl cardmgr[1935]: executing: './network start eth1'
May 4 10:21:23 nsl /etc/hotplug/net.agent: invoke ifup eth1
```

The preceding code shows that the kernel recognizes the PCI card (at IRQ 5). The cardmgr identifies the Orinoco card as a WaveLAN/IEEE adapter in socket 0. The network script starts an Ethernet interface (eth1).

If the wireless LAN interface started properly, you should be able to see the new interface by using the `iwconfig` command. The following is an example of output from the `iwconfig` command:

```text
io        no wireless extensions.

eth0      no wireless extensions.

eth1      IEEE 802.11-DS  ESSID:"Wavelan Network"  Nickname:"a.abc.com"
          Mode:Ad-Hoc  Frequency:2.457GHz  Cell: 02:02:2D:2E:8C:A8
          Bit Rate:2Mb/s  Tx-Power=15 dBm  Sensitivity:1/3
          Retry limit:4  RTS thr:off  Fragment thr:off
          Encryption key:7365-6375-31
          Power Management:off
          Link Quality:0  Signal level:0  Noise level:0
          Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:0
          Tx excessive retries:0  Invalid misc:0  Missed beacon:0
```

If your wireless LAN interface does not appear to be working, refer to the section “Troubleshooting a wireless LAN” later in this chapter. If the interface does seem to be working, you are ready to tune your wireless LAN card interface and set up TCP/IP to be able to use the interface.

# Configuring the wireless interface

> **CAUTION:** Explicit support for wireless LAN cards was removed from the Network Configuration window at the last moment for Red Hat Linux 7.3. The procedure in this section describes how to configure a wireless card manually. The result is a wireless configuration file that is similar to the one that would be produced by the Network Configuration window.

After your wireless card is detected, an interface configuration file is created in your `/etc/sysconfig/network-scripts` directory. The name of the configuration file is `ifcfg-` followed by the interface name (such as eth0, eth1, and so on). So, if your wireless card is providing your only network interface, it would be called `ifcfg-eth0`.

Using any text editor, open the `ifcfg-eth?` file as root user. The following is an example of an `ifcfg-eth1` file:

```text
USERCTL=no
HWADDR=00:02:2d:2e:8c:a8
BOOTPROTO=none
ONBOOT='yes'
DEVICE=eth1
TYPE=Ethernet
NETMASK='255.255.255.0'
IPADDR='10.0.1.1'
BROADCAST='255.255.255.255'
GATEWAY='10.0.1.2'
```

In this example, the wireless card's hardware (MAC) address is automatically set to 00:02:2d:2e:8c:a8. The interface is set to come up at boot time (ONBOOT='yes'). Your MAC address will be different. The interface device is eth1 (which matches the interface filename ifcfg-eth1), because the computer has another Ethernet card on the eth0 interface. The interface type is set to Ethernet.

Other information in the file sets standard TCP/IP address information. The NETMASK is set to 255.255.255.0 and the IP Address for the card is set to 10.0.1.1. The broadcast address is 255.255.255.255. In this case, the computer is using another computer on the wireless network (10.0.1.2) on the wireless network as a gateway to the Internet.

You can also set many options that are specific to your wireless network in this file. The following is a list of some options that you might want to set:

- **ESSID** — The network name (or Network ID) that identifies cells that are part of the same network. If you have a group of cells (which might include multiple nodes and repeaters among which a client could roam), this name can identify all of those cells as falling under one virtual network. Choose any name you like and then use that name for all computers in your virtual network. (ESSID stands for Extended Service Set ID.)
- **MODE** — Indicates the mode of operation for the wireless LAN card. Because I am setting up a wireless LAN consisting of only one cell (in other words, with no roaming to cells set up in other areas), I could set the mode to Ad hoc or simply leave it on Auto. Ad hoc mode allows the card to communicate directly with each of its peers. You can use Managed mode if you have multiple cells, requiring your card to communicate directly to an access point. You can also use Managed mode for a point-to-point network, such as when you use the wireless LAN to extend a network from one building to another.
- **NWID** — Identifies the name of this particular computer on the network. The computer's host name (determined from the uname -n command) is used by default if you don't set it with NWID.
- **FREQ** — You can choose a particular frequency in which to transmit. No value is required, because selecting a channel implies a certain frequency. If you do enter a frequency, the value must be a number followed by a k (kilohertz), M (megahertz), or G (gigahertz). The default values for the channels you select range from 2.412G (channel 1) to 2.484G (channel 14), with other channels occurring at increments of .005G. The default is 2.422G.
- **CHANNEL** — Choose a channel between 1 and 14. You can begin with channel 1 and, if you get interference on that channel, try changing to other channels.
- **SENS** — You can select the sensitivity level of the access point. SENS can be set to 1 (low density), 2 (medium density), 3 (high density). The default is 1. The sensitivity threshold has an impact on roaming.
- **RATE** — Choose the rate of transmission from the following rates: 11M, 5.5M, 2M, 1M, or auto. Choosing auto (which is the default) allows the interface to automatically ramp down to lower speeds as needed. Lower speeds allow the interface to transmit over greater distances and deal with noisy channels.
- **KEY** — You need the same encryption key for all wireless LAN cards that are communicating with each other. It is critical to get this value right. This key is used to encrypt all data transmitted and decrypt all data received on the wireless interface. Though you can leave the default key, you can ensure greater security by selecting a new key and entering it for the card on each wireless computer on your network. You can enter the number (up to 10 digits) as XXXXXXXXXXXX or XXXX-XXXX-XX (where each X is a number). You can also enter fewer than 10 digits. For example, entering 99 would result in the number 9900-0000-00.

> **CAUTION:** The encryption algorithm used with 802.11 networks is the Wired Equivalent Privacy (WEP) algorithm. Though using the encryption key is more secure than not using it, some experts feel that WEP has some inherent flaws that might allow a drive-by hacker to decrypt your wireless LAN traffic. For that reason, I strongly recommend using additional techniques to protect your wireless LANs, such as firewalls and diligent log-checking. See the Wireless Security sidebar for further information.

Besides those options just shown, you can also pass any valid options to the `iwconfig` command (which actually interprets these values), by adding an IWCONFIG option to the configuration file. Display the `iwconfig` man page (`man iwconfig`) to see all wireless options. Also view the `/etc/sysconfig/network-scripts/ifup-wireless` script to see how the options you just added are processed.

> **NOTE:** On the computer that is acting as a gateway to your Internet connection, you need to turn on IP packet forwarding. Change the value of `net.ipv4.ip_forward` to 1 in the `/etc/sysctl.conf` file. Open that file as the root user with any text editor and change the line as follows:
> `net.ipv4.ip_forward = 1`

Repeat this procedure for each wireless Red Hat Linux computer on your LAN. At this point, your wireless network should be ready to go. Restart your network, as described in the following steps, to make sure that it is working.

# Restarting wireless interfaces

To cause the information you just entered to take effect for your wireless cards, simply restart the PCMCIA interface on your Linux computer. You can then test that you can communicate between the two wireless computers using standard TCP/IP tools (such as the `ping` command).

To restart the wireless interfaces, type the following as root user from a Terminal window on each of the wireless computers:
