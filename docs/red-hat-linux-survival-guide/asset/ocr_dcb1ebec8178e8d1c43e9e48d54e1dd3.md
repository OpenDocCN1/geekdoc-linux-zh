time. The lower these numbers are, the better the routing is between the involved hosts. For example, if you ping a host on the same LAN, you should see the round-trip numbers in the 1-millisecond range.

If you would like to have ping stop automatically after transmitting a number of packets, use the -c option. For example:

```
ping -c 10 blackhole.evoknow.com
```

This sends 10 ping requests to the named host. By default, ping sends a 64-byte (56 data bytes + 8 header bytes) packet. If you are also interested in controlling the size of the packet sent, use the -s option. For example:

```
ping -c 1024 -s 1016 reboot.evoknow.com
```

This command sends a packet 1,024 (1016 + 8) bytes long to the remote host.

![](bbox=[0.06, 0.6, 0.16, 0.68])

By sending large packets to a remote host running weak operating systems (you know what they are), you might cause the host to become very unusable to the user(s) on the remote host. This could be considered as an attack by many system administrators and therefore is very likely to be illegal in most parts of the world. So, be very careful when you start experimenting with ping and someone else's computer.

# route

+   Syntax 1: route add -net network_address netmask dev device
+   Syntax 2: route add -host hostname_or_IP dev device
+   Syntax 3: route add default gw hostname_or_IP

This command allows you to control routing to and from your computer. For example, to create a default route for your network, use the route command as follows:

```
route add -net network_address netmask device
```

To create a default route for 206.171.50.48 network with a 255.255.255.240 netmask and eth0 as the interface, you can run the following command: