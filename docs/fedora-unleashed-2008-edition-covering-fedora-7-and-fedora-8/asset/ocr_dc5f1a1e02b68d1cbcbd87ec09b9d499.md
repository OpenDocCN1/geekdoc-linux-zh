# **Support for Wireless Networking in Fedora**

The Linux kernel that ships with Fedora provides extensive support for wireless networking. Related wireless tools for configuring, managing, or displaying information about a wireless connection include the following:

+   ► **iwconfig**—Sets the network name, encryption, transmission rate, and other features of a wireless network interface

+   ► **iwlist**—Displays information about a wireless interface, such as rate, power level, or frequency used

+   ► **iwpriv**—Uses i to set optional features, such as roaming, of a wireless network interface

+   ► **iwspy**—Shows wireless statistics of a number of nodes

Support varies for wireless devices—most likely in the form of a PCMCIA adapter—although some USB wireless devices now work with Linux. In general, Linux wireless device software (usually in the form of a kernel module) supports the creation of an ethernet device that can be managed by traditional interface tools such as *ifconfig*—with wireless features of the device managed by the various wireless software tools.

For example, when a wireless networking device is first recognized and initialized for use, the driver will most likely report a new device:

```
``` 
wlan_cs: WaveLAN/IEEE PCMCIA driver v1.0.6
wlan_cs: (c) Andreas Neuhaus <and@yafsta.fh-dortmund.de>
wlan_cs: index 0x01: Vcc 3.3, irq 3, io 0x0100-0x013f
wlan_cs: Registered netdevice eth0
wlan_cs: MAC address on eth0 is 00 05 5d f3 1d da
```
```

This output (from the *dmesg* command) shows that the *eth0* device has been reported. If DHCP is in use, the device should automatically join the nearest wireless subnet and be automatically assigned an IP address. If not, the next step is to use a wireless tool such as *iwconfig* to set various parameters of the wireless device. The *iwconfig* command, along with the device name (*eth0* in this example), shows the status:

```
``` 
# iwconfig eth0
eth0    IEEE 802.11-DS  ESSID:"GreyUF0"  Nickname:"Prism I" 
Mode:Managed  Frequency:2.412GHz  Access Point: 00:02:2D:2A:FE:3C 
Bit Rate:2Mb/s  Tx-Power=15 dBm  Sensitivity:1/3
RTS thr:off  Fragment thr:off 
Encryption key:off 
Power Management:off 
Link Quality:92/92 Signal level:-11 dBm Noise level:-102 dBm 
Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:0 
Tx excessive retries:0  Invalid misc:4  Missed beacon:0
```
```