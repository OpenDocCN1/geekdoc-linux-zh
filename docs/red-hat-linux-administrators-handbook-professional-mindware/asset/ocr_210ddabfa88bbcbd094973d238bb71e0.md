between the involved hosts. For example, if you ping a host internal to the same LAN, you should see the round-trip numbers in the one-millisecond range.

If you want ping to automatically stop after transmitting a number of packets, use the -c option. For example, the following sends 10 ping requests to the named host:

```
ping -c 10 blackhole.nitsec.com
```

By default, ping sends a 64-byte packet (56 data bytes + 8 header bytes). If you are also interested in controlling the size of the packet sent, use the -s option. For example,

```
ping -c 1024 -s 1016 reboot.nitsec.com
```

sends a packet 1,024 (1016 + 8) bytes long to the remote host.

# **Caution**

By sending large packets to a remote host running weak operating systems, you might cause the host to become very unusable to the user(s) on the remote host. This could be considered an attack and therefore is very likely to be illegal in most parts of the world. So, be very careful when you start experimenting with ping and someone else's computer.

# route

**Syntax:** route add -net *network address* *netmask* dev *device*

```
route add -host *hostname or IP* dev *device*
route add default gw *hostname or IP*
```

The *route* command enables you to control routing to and from your computer. To create a default route for your network, use the *route* command as follows:

```
route add -net *network address* *netmask* *device*
```

For example, to create a default route for network 206.171.50.48 with a 255.255.255.240 netmask and *eth0* as the interface, I can run the following:

```
route add -net 206.171.50.48 255.255.255.240 eth0
```