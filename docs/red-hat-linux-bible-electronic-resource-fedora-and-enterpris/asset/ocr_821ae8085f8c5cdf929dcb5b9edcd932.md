name (such as eth0, eth1, and so on). So, if your wireless card is providing your only network interface, it would be called `ifcfg-eth0`.

Using any text editor, open the `ifcfg-eth?` file as root user. The following is an example of an `ifcfg-eth1` file:

```
# Please read /usr/share/doc/initcripts-*/sysconfig.txt
# for the documentation of these parameters.
USERCTL=no
PEERDNS=no
GATEWAY=10.0.0.1
TYPE=Wireless
DEVICE=eth1
HWADDR=00:02:2d:2e:8c:a8
BOOTPROTO=none
NETMASK=255.255.255.0
ONBOOT=no
IPADDR=10.0.1.1
NAME=
DOMAIN=
ESSID=
CHANNEL=1
MODE=Ad-Hoc
KEY=9900-0000-00
RATE=11Mb/s
NETWORK=10.0.1.0
BROADCAST=10.0.1.255
```

In this example, the wireless card's hardware (MAC) address is automatically set to `00:02:2d:2e:8c:a8`. (Your MAC address will be different.) The interface is not yet set to come up at boot time (`ONBOOT=no`). The interface device is `eth1` (which matches the interface filename `ifcfg-eth1`), because this particular computer has another Ethernet card on the `eth0` interface. The interface type is set to **Wireless**.

Other information in the file sets standard TCP/IP address information. The NETMASK is set to 255.255.255.0 and the IP address for the card is set to 10.0.1.1. The broadcast address is 10.0.1.255.

You can also set many options that are specific to your wireless network in this file. The following is a list of some additional options that you might want to set:

+   - **NWID** — Identifies the name of this particular computer on the network. The computer's host name (determined from the `uname -n` command) is used by default if you don't set it with NWID.
+   - **FREQ** — You can choose a particular frequency in which to transmit. No value is required, because selecting a channel implies a certain frequency. If you do enter a