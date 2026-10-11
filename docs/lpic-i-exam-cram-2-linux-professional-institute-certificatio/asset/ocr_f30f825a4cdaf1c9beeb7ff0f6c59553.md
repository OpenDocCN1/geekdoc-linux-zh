4. After you have your network (180 falls in the 129–191 network) you can stop, unless you just have to finish the networks.

Your network address is 10.30.200.128, the first addressable host IP is 10.30.200.129, the last addressable host IP is 10.30.200.190, and the broadcast address is 10.30.200.191. There are 62 host IP addresses on your subnet.

> Be prepared to reread questions to see if they want to know all IPs on a network or whether you leave out the router and broadcast address. If you're asked for the number of IPs that could be assigned to hosts, it's always an even number; if you are to disregard or leave out the router/gateway address, it has to be an odd number.

# ## Managing Interfaces

A Linux machine has a default interface called the loopback or local interface. The device appears as lo (that's a lowercase L, not a one) and can be configured like other interfaces, with the main difference being that the loopback is never going to connect to a network. The loopback interface is only there so your machine can have IP bound to an interface even if it's not otherwise configured to use a network card.

Real life, bosses, and the exam will require you to be able to set your IP via the interface configuration files or even statically configure the interface from the command line.

# ## Viewing IP Information

The primary tool for viewing your IP information is the ifconfig command. By default, ifconfig shows all active interfaces, including the loopback interface: lo.

To display the interfaces on a Linux machine, you would enter the following command:

```
```
ifconfig
```
```

This produces output similar to the following:

```
```
eth0      Link encap:Ethernet  HWaddr 00:0C:29:66:DE:2D
          inet addr:192.168.1.73  Bcast:192.168.1.255  Mask:255.255.255.0
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:162310 errors:0 dropped:0 overruns:0 frame:0
          TX packets:97324 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:242424213 (231.1 Mb)  TX bytes:6835983 (6.5 Mb)
          Interru:10 Base address:0x1080
```
```