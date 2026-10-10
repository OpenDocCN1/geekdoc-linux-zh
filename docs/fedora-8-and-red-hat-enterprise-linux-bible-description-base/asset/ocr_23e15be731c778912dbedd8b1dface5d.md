+   - **Statically set IP addresses:** Click here to manually set your IP addresses.
+   - **Address:** If you selected static IP addresses, type the IP address of this computer into the Address text box. This number must be unique on your wireless network.
+   - **Subnet Mask:** Enter the netmask to indicate what part of the IP address represents the network. (Netmask is described later in this chapter.)
+   - **Default Gateway Address:** If a computer on your wireless LAN is providing routing to the Internet or other network, type the IP address of the computer here.

+   7. Click Forward to see a listing of the information you just entered.
+   8. Click Apply to complete the new wireless network interface.
+   9. Select File → Save (on the main window) to save the interface.

This procedure creates an interface configuration file in your /etc/sysconfig/network-scripts directory. The name of the configuration file is ifcfg- followed by the interface name (such as eth0, eth1, and so on). So, if your wireless card is providing your only network interface, it might be called ifcfg-eth0.

Using any text editor, open the ifcfg-eth? file (replacing ? with the interface number) as root user. The following is an example of an ifcfg-eth1 file:

```
```
# Please read /usr/share/doc/initscripts-*/sysconfig.txt
# for the documentation of these parameters.
ONBOOT=no
USERCTL=no
PEERDNS=no
GATEWAY=10.0.0.1
TYPE=Wireless
DEVICE=eth1
HWADDR=00:02:2d:2e:8c:a8
BOOTPROTO=none
NETMASK=255.255.255.0
IPADDR=10.0.1.1
DOMAIN=
ESSID=
CHANNEL=1
MODE=Ad-Hoc
RATE=11Mb/s
NETWORK=10.0.1.0
BROADCAST=10.0.1.255
```
```

In this example, the wireless card's hardware (MAC) address is automatically set to 00:02:2d:2e:8c:a8. (Your MAC address will be different.) The interface is not yet set to come up at boot time (ONBOOT=no). The interface device is eth1 (which matches the interface filename ifcfg-eth1), because this particular computer has another Ethernet card on the eth0 interface. The interface type is set to Wireless.