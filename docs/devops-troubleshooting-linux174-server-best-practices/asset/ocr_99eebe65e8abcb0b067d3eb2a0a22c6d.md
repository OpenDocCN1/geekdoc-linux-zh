network card or some other network component to which your host is connected starts to fail, you can see it in packet errors on your system. The ifconfig command you may have used for network troubleshooting before can also tell you about TX (transmit) or RX (receive) errors for a card. Here's an example from a healthy card:

```
```
$ sudo ifconfig eth0
eth0 Link:encap:Ethernet HWaddr 00:17:42:f1:18:be
in64 addr:10.1.1.7 Bcast:10.1.1.255 Mask:255.255.255.0
inet6 addr: fe80::217:42ff:fe1f:18be/64 Scope:Link
UP BROADCAST MULTICAST MTU:1500 Metric:1
RX packets:1 errors:0 dropped:0 overruns:0 frame:0
collisions:0 txqueuelen:1000
RX bytes:229 (229.0 B) TX bytes:2178 (2.1 KB)
Interrupt:10
```
```

The lines you are most interested in are

```
```
RX packets:1 errors:0 dropped:0 overruns:0 frame:0
TX packets:11 errors:0 dropped:0 overruns:0 carrier:0
collisions:0 txqueuelen:1000
```
```

These lines will tell you about any errors on the device. If you start to see a lot of errors here, then it's worth troubleshooting your physical network components. It's possible a network card, cable, or switch port is going bad. Start with the easiest-to-test component by swapping out the network cable with a new or known good cable, and if you continue to get errors, then move the cable to a new, hopefully known, good switch port. Finally, if neither of those solutions help, try swapping out the network card (or switching to a different port if your server has multiple Ethernet ports).

# ### The Server Is Too Hot

Servers, especially busy servers, generate a lot of heat. Although ideally your server is collocated in a facility with good active cooling, it might also just be shoved under someone's desk, or it may sit at the top of a rack in