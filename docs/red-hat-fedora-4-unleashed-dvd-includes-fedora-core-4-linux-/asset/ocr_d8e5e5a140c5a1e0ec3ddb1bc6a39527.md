This example shows a 2Mbps connection to a network named GREYUFO. To change a parameter, such as the transmission rate, use a command-line option with the `iwconfig` command like so:

```
# iwconfig eth0 rate 11M
```

Other options supported by the `iwconfig` command include `essid`, used to set the NIC to connect to a specific network by name; `mode`, used to enable the NIC to automatically retrieve settings from an access point or connect to another wireless host; or `freq`, to set a frequency to use for communication. Additional options include `channel`, `frag`, `enc` (for encryption), `power`, and `txpower`. Details and examples of these options are in the `iwconfig` manual page.

You can then use the `ifconfig` command or perhaps a graphical Red Hat tool to set the device networking parameters, and the interface will work as on a hardwired LAN. One handy output of the `iwconfig` command is the link quality output, which can be used in shell scripts or other graphical utilities for signal monitoring purposes (refer to Chapter 14 for an example).

# # Cellular Networking

The ads are starting to crop up on TV: This cellular service will allow you to check your email anywhere your cellular phone can reach; that cellular company will provide news and other information via the Internet to your phone. Personal digital assistants have cellular add-ons or even built-in options.

For example, if your laptop has a cellular modem, you can use it to dial in to your network. This is not truly wireless networking if the network dialed in to is wired, but it illustrates how far-reaching wireless networks can go. As long as cellular service follows you, you can dial in to any network you have access to (be it home or office) from any location in the world to check your email and use it to send electronic files to your associates. And many newer cell phones can be used as a modem by attaching a cable from the phone to a serial or USB port on a laptop. As with most devices, the majority of brand-name PCMCIA cards will work with Linux. A lot of generic equipment (such as serial I/O cards) should work, but you are taking a chance if the card is not supported (see the section “Managing PCMCIA” in Chapter 4, “Post-Installation Configuration”).

# # Advantages of Wireless Networking

Advantages to wireless networking are the mobility and the potential range. If you have a large enough antenna network, your network can stretch many miles. This would be an expensive network, but one that would easily break out of the brick and mortar confines of the office.

Wireless networking would also be a great advantage to college campuses to eliminate the need to tear through walls to install cabling because more and more students expect to have a network connection in their dorm rooms. Wireless networking cards are becoming more reasonable in price and can easily be issued to each student as he requires them.