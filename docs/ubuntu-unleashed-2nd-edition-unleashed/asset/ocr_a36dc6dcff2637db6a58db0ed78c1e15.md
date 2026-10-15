```
Rx invalid nwid:0 Rx invalid crypt:0 Rx invalid frag:0
Tx excessive retries:0 Invalid misc:4 Missed beacon:0
```

This example shows a 2Mbps connection to a network named GreyUFO. To change a parameter, such as the transmission rate, use a command-line option with the iwconfig command like so:

```
$ sudo iwconfig eth0 rate 11M
```

Other options supported by the iwconfig command include essid, used to set the NIC to connect to a specific network by named; mode, used to enable the NIC to automatically retrieve settings from an access point or connect to another wireless host; or freq, to set a frequency to use for communication. Additional options include channel, frag, enc (for encryption), power, and txpower. Details and examples of these options are in the iwconfig manual page.

You can then use the ifconfig command or perhaps a graphical Ubuntu tool to set the device networking parameters, and the interface will work as on a hardwired LAN. One handy output of the iwconfig command is the link quality output, which can be used in shell scripts or other graphical utilities for signal monitoring purposes.

# Advantages of Wireless Networking

Advantages of wireless networking are its mobility and potential range. If you have a large enough antenna network, your network can stretch many miles. This would be an expensive network, but one that would easily break out of the brick and mortar confines of the office.

Wireless networking would also be a great advantage to college campuses to eliminate the need to tear through walls to install cabling because more and more students expect to have a network connection in their dorm rooms. Wireless networking cards are becoming more reasonable in price and can easily be issued to each student as he requires them.

Home networkers can also benefit from wireless networking. For those who cannot do wired network modifications to their homes, wireless networking removes the unsightly wires running along baseboards and ceilings that are required to connect computers in different rooms. With a wireless home network, you are not even confined to inside the house. Depending on the transmit power of your router, you can sit out in your backyard and watch clouds drifting by as you type away. Wireless routers are coming down in price with each passing day.

Choosing the right types of wireless devices is an important decision. The next sections discuss some of the basic differences between current protocols used for wireless networking.

# Choosing from Among Available Wireless Protocols

The Institute of Electrical and Electronics Engineers (IEEE) started to look seriously at wireless networking in 1990. This is when the 802.11 Standard was first introduced by the