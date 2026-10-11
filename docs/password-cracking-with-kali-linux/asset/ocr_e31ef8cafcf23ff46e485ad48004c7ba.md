# METASPLOITABLE 2 - SETTING THE IP ADDRESS

By default, Metasploitable 2’s address is set as “Dynamic”. That will be perfectly fine for our lab. If you don’t need to change the IP address you can skip ahead to “**Windows 11 - Installing as a Virtual Machine**.”

If you want to set it to a Static IP, edit the “*/etc/network/interfaces*’ file. In this file you can set the IP address, Netmask and Gateway.

+   > In Metasploitable2 navigate to “*/etc/network*’

+   Enter, “***sudo nano interfaces***’

+   Change the “iface eth0 inet dynamic” line to say “***iface eth0***  
+   ***inet static***’

+   Then enter the IP address, netmask, and your router gateway.

+   Example IP addresses just for reference, use IP addresses appropriate for your network.

```
# This file describes the network interfaces available on your system
# and how to activate them. For more information, see interfaces(5).
#
# The loopback network interface
auto lo
iface lo inet loopback

# the primary network interface
auto eth0
iface eth0 inet static
	address	192.168.1.68
					netmask	255.255.255.0
					gateway	192.168.1.1
```

+   When finished, hit “***ctrl-x***’, “***y***’, and then hit “***enter***’

+   Type in “***cat interfaces***’ to verify your changes: