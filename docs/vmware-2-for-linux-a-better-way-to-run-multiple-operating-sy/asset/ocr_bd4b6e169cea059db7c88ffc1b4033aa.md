# Sharing Between a Linux Host and a Linux Guest

It would certainly be nice if you could give your virtual machine access to all the riches stored on your host PC and get information out of the virtual machine easily and quickly.

Think of host-only networking as a virtual network pipeline that connects just the virtual machine and the host, nothing else. Bridged networking gives your virtual machine a virtual Ethernet card that behaves as though it is attached to a hub with your host PC's physical Ethernet card, allowing the host and guest to communicate, while also potentially linking your guest with any computer your host can reach through its physical Ethernet connection.

Your first move is to write down the IP address of your host PC. If you are using bridged networking, simply write down the IP address of your Linux PC's main Internet or LAN adapter. (If you're using a modem or DSL connection, it might be dynamic, in which case you have to re-check it every time you reboot or reconnect to the Internet.)

There's a shortcut for all this, the ifconfig command. You might need to be root (or use the su command) to run ifconfig, and it might not even be in your default path: Generally, it is kept at /sbin/ifconfig. Run the command with no arguments at a terminal prompt, and you'll find out everything you ever wanted to know about your IP configuration. Sample output is shown in Figure 10.23. Start with your host PC.

Any computer has an entry for lo, the local loopback. Ignore this entry. You're interested in eth0 and vmnet1; you need at least one of them if you plan to network with the virtual machine.

![](bbox=[0.07, 0.78, 0.48, 0.9])