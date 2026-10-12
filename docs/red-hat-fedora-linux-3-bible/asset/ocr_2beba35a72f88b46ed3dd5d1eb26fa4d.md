```
```
64 bytes from pine (10.0.0.10): icmp_seq=10 ttl=255 time=0.367 ms
--- pine ping statistics ---
10 packets transmitted, 10 packets received, 0% packet loss, time 9011ms
rtt min/avg/max/mdev = 0.351/0.402/0.457/0.042 ms
```
```

A line of output is printed each time a packet is sent and received in return. It shows how much data was sent and how long it took for each package to be received. After you have watched this for a while, type Ctrl+C to stop ping. At that point, you will see statistics on how many packets were transmitted, received, and lost.

If you don’t see output that shows packets have been received, it means you are not contacting the other computer. Try to verify that the names and addresses of the computers that you want to reach are in your `/etc/hosts` file or that your DNS server is accessible. Next, confirm that the names and IP addresses you have for the other computers you are trying to reach are correct (the IP addresses are the most critical).

# ## Is your Ethernet connection up?

Using the `ifconfig` command, you can determine whether your Ethernet (and other network interfaces) are up and running. Type the following command:

```
```
# ifconfig
```
```

The output that appears is similar to the following:

```
```
eth0 Link encap:Ethernet HWaddr 00:90:27:4E:67:35
in     addr:10.0.0.10 Bcast:10.0.0.255 Mask:255.255.255.0
UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
RX packets:156 errors:0 dropped:0 overruns:0 frame:0
TX packets:104 errors:0 dropped:0 overruns:0 carrier:0
collisions:0 txqueuelen:100
RX bytes:20179 (19.7 Kb)  TX bytes:19960 (19.4 Kb)
Interrupt:11 Base address:0x0000 Memory:fff8f000-fff8f038

lo     Link encap:Local Loopback
in     addr:127.0.0.1 Mask:255.0.0.0
UP LOOPBACK RUNNING  MTU:3924  Metric:1
RX packets:56 errors:0 dropped:0 overruns:0 frame:0
TX packets:56 errors:0 dropped:0 overruns:0 carrier:0
collisions:0 txqueuelen:0
RX bytes:3148 (3.0 Kb)  TX bytes:3148 (3.0Kb)
```
```

In this example, two network interfaces are up on the current computer. The first section shows your Ethernet interface (eth0), and its Ethernet hardware address, IP address (inet addr), broadcast address, and netmask. The next lines provide information on packets that have been sent, along with the number of errors and collisions that have occurred.