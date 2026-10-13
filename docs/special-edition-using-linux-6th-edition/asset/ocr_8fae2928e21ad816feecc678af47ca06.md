The preceding line says to configure the interface eth0 and give it the IP address 192.168.0.2. This will be on a network defined by 192.168.0.0–192.168.0.255 and will use the broadcast address of 192.168.0.255. You can omit the broadcast address and the word BROADCAST will disappear from the third line in Listing 22.1. This is not recommended because systems are expected to reply to network broadcasts. If you are concerned with someone outside trying to cause havoc by pinging your broadcast address, you don't need to worry, because most routers are designed to drop external traffic sent to broadcast addresses.

You can turn off the interface by using the following command:

```
```shell
ifconfig eth0 down
```
```

If you have built a kernel to support the ethertap device, feel free to experiment by configuring tap0. This makes an excellent way to test features on a host with no Ethernet device. The ethertap device can be configured almost any way you’d like. Before you start using the ethertap device, read /usr/src/linux/Documentation/networking/ethertap.txt.

# ROUTE

The second utility you’ll need to be able to network beyond the local systems is route. The route utility will enable you to specify a default gateway to the Internet. If your system is connected directly to the Internet through a modem, your system should have been automatically configured by your Internet provider. Otherwise, you’ll have to tell your system where the system (gateway) is that’s connected to the Internet.

Assuming your host has IP 192.168.0.2 and the system 192.168.0.1 is connected to the Internet, you’ll need to tell your host to use 192.168.0.1 as its gateway to the Internet. You can do this as follows:

```
```shell
route add default gateway 192.168.0.1
```
```

This command tells route to add 192.168.0.1 as the default to reach the Internet. Any packets that don’t have any other route to take to reach their destination will be passed to 192.168.0.1. If you look at the output of route with no options, you’ll see where all packets will route. Listing 22.2 shows the routes on the local system.

**LISTING 22.2 — OUTPUT FROM ROUTE**

| Kernel IP routing table |  |  |  |  |  |  |
|---|---|---|---|---|---|---|
| Destination | Gateway | Genmask | Flags | Metric | Ref | Use Iface |
| 192.168.0.0 | 0.0.0.0 | 255.255.255.0 | U | 0 | 0 | eth0 |
| 127.0.0.0 | 0.0.0.0 | 255.0.0.0 | U | 0 | 0 | lo |
| 0.0.0.0 | 192.168.0.1 | 0.0.0.0 | UG | 1 | 0 | eth0 |

This listing shows that anything destined for a system on the network 192.168.0.0 (from 192.168.0.1 to 192.168.0.255) will be put on the local wire. Anything for 127.0.0.1–127.255.255.255 will go to localhost. Anything else (designated by 0.0.0.0) will go to 192.168.0.1 for further routing.