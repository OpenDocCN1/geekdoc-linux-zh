![](bbox=[0.12, 0.2, 0.18, 0.3])

> If your client systems have RX and TX errors, or drops/overruns that account for more than about 10% of the overall packets, you might have overly busy subnets. The solution is to break up your subnets further. If you have zero (as seen here), the logical conclusion is that there's plenty of room for more servers on the wire.

The summary line showing RX bytes is a nice addition that saves some hand calculations: This server has received packets totaling 3.9MB and transmitted 14.4MB of packets.

2. In contrast to the loquacious output from Red Hat Linux, consider the same ifconfig output from Mac OS X:

```
# ifconfig -a
lo0: flags=8049<UP,LOOPBACK,RUNNING,MULTICAST> mtu 16384
inet 127.0.0.1 netmask 0xff000000
en0: flags=8863<UP,BROADCAST,RUNNING,SIMPLEX,MULTICAST> mtu 1500
inet 198.76.82.132 netmask 0xffffffff broadcast 198.76.82.255
ether 00:30:65:3d:e8:10
media: autoselect (10baseT/UTP <half-duplex>) status: active
supported media: none autoselect 10baseT/UTP <half-duplex> 10baseT/UTP <full-duplex> 100baseTX <half-duplex> 100baseTX <full-duplex>
```

Quite different, and no RX/TX statistics here at all. Same proper 1500-byte MTU, though.

Solaris offers an even more concise result:

```
# /sbin/ifconfig -a
lo0: flags=1000849<UP,LOOPBACK,RUNNING,MULTICAST,IPv4> mtu 8232 index 1
inet 127.0.0.1 netmask ff000000
pcn0: flags=1000043<UP,BROADCAST,RUNNING,MULTICAST,IPv4> mtu 1500 index 2
inet 198.76.82.155 netmask ffffff00 broadcast 198.76.82.255
ether 0:50:56:54:45:9d
```

Even more minimal, but it still offers the core information necessary for verifying the setup of the Ethernet interface, with the IP address, netmask (albeit in a more difficult-to-interpret format), broadcast address, and MTU.

3. It's useful to have a good picture of the network traffic on a given system, and that's what the multipurpose netstat network status command offers.

```
# netstat
Active Internet connections (w/o servers)
Proto Recv-Q Send-Q Local Address Foreign Address State
tcp 0 208 10.10.2.200:ssh ds1.132.ds1design:49172 ESTABLISHED
```

![](bbox=[0.88, 0.4, 0.98, 0.62])