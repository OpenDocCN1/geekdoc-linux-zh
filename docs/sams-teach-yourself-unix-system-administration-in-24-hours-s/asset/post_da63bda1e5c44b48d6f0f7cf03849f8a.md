
![](img/5ced0c78d748bd190e9027e5549a3622_361_0.png)

> If your client systems have RX and TX errors, or drops/overruns that account for more than about 10% of the overall packets, you might have overly busy subnets. The solution is to break up your subnets further. If you have zero (as seen here), the logical conclusion is that there's plenty of room for more servers on the wire.

The summary line showing RX bytes is a nice addition that saves some hand calculations: This server has received packets totaling 3.9MB and transmitted 14.4MB of packets.

- 2. In contrast to the loquacious output from Red Hat Linux, consider the same ifconfig output from Mac OS X:

    ```
    # ifconfig -a
    lo0: flags=8049<UP,LOOPBACK,RUNNING,MULTICAST> mtu 16384
    inet 127.0.0.1 netmask 0xff000000
    en0: flags=8863<UP,BROADCAST,RUNNING,SIMPLEX,MULTICAST> mtu 1500
    inet 198.76.82.132 netmask 0xffffff00 broadcast 198.76.82.255
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
    pcn0: flags=1000843<UP,BROADCAST,RUNNING,MULTICAST,IPv4> mtu 1500 index 2
    inet 198.76.82.155 netmask ffffff00 broadcast 198.76.82.255
    ether 0:50:56:54:45:9d
    ```

    Even more minimal, but it still offers the core information necessary for verifying the setup of the Ethernet interface, with the IP address, netmask (albeit in a more difficult-to-interpret format), broadcast address, and MTU.

- 3. It's useful to have a good picture of the network traffic on a given system, and that's what the multipurpose netstat network status command offers.

    ```
    # netstat
    Active Internet connections (w/o servers)
    Proto Recv-Q Send-Q Local Address Foreign Address State
    tcp 0 208 10.10.2.200:ssh ds1-132.dsldesign:49172 ESTABLISHED

    Active UNIX domain sockets (w/o servers)
    Proto RefCnt Flags Type State I-Node Path
    unix 7 [ ] DGRAM 905 /dev/log
    unix 2 [ ] DGRAM 1226
    unix 2 [ ] DGRAM 1207
    unix 2 [ ] DGRAM 1162
    unix 2 [ ] DGRAM 961
    unix 2 [ ] DGRAM 914
    unix 2 [ ] STREAM CONNECTED 628
    ```

    ![](img/5ced0c78d748bd190e9027e5549a3622_361_1.png)

    By default, the first section shows the active established network connections (here it's showing an ssh connection to 10.10.2.200 from ds1-132.dsldesign, with a connection ID of 49172). The second section is a list of all open sockets, some associated with daemons, some tied to specific files (such as /dev/log), and most fairly cryptic.

    Similar output is produced by netstat on other Unices, though the exact format often varies. Solaris has a particularly helpful output format:

    ```
    # netstat

    TCP: IPv4
    Local Address Remote Address Swind Send-Q Rwind Recv-Q State
    solaris.32804 mac.6000 33304 0 66608 0 ESTABLISHED

    Active UNIX domain sockets
    Address Type Vnode Conn Local Addr Remote Addr
    e10c0d08 stream-ord 00000000 00000000
    e10cdea8 stream-ord 0be79920 00000000 /tmp/.X11-unix/X0
    ```

    Clearly denoting that there's a remote X11 event occurring.

    Various flags to netstat produce different output. Most useful is -a, which offers a different format that includes what protocols are listening, as well as established:

    ```
    # netstat -a

    Active Internet connections (servers and established)
    Proto Recv-Q Send-Q Local Address Foreign Address State
    tcp 0 0 *:32768 *:* LISTEN
    tcp 0 0 localhost.localdomain:32769 *:* LISTEN
    tcp 0 0 *:sunrpc *:* LISTEN
    tcp 0 0 *:http *:* LISTEN
    tcp 0 0 *:ssh *:* LISTEN
    tcp 0 0 localhost.localdomain:smtp *:* LISTEN
    tcp 0 0 *:https *:* LISTEN
    tcp 0 224 10.10.2.200:ssh ds1-132.dsldesign:49172
    ->ESTABLISHED
    udp 0 0 *:32768 *:*
    udp 0 0 *:793 *:*
    udp 0 0 *:sunrpc *:*

    Active UNIX domain sockets (servers and established)
    Proto RefCnt Flags Type State I-Node Path
    unix 7 [ ] DGRAM 985 /dev/log
    unix 2 [ ] DGRAM 1226
    unix 2 [ ] DGRAM 1287
    unix 2 [ ] DGRAM 1162
    unix 2 [ ] DGRAM 961
    unix 2 [ ] DGRAM 914
    unix 2 [ ] STREAM CONNECTED 628
    ```

    We can see that this system is supporting SunRPC (remote procedure call), http (for the Apache Web server), ssh (secure shell), smtp (for e-mail), https (secure Apache connections) and that there's an established ssh connection. There are also a few UDP listeners.

    The output of netstat -a is one way you can verify that the services you think you've disabled really aren't running. (See Hour 19, "Running Internet Services," for more information about disabling services.)

- 4. The netstat command also offers transmit/receive statistics in a quite concise manner if the -i flag is used:

    ```
    # netstat -i
    Kernel Interface table
    Iface MTU Met RX-OK RX-ERR RX-DRP RX-OVR TX-OK TX-ERR TX-DRP TX-OVR Flg
    eth0 1500 0 37597 0 0 0 36220 0 0 0 BMRU
    lo 16436 0 98 0 0 0 98 0 0 0 LRU
    ```

    This is consistent with what ifconfig reported: lots of in and out packets with nary a single hiccup or glitch.

    Solaris reports Ipkts and Opkts (in and out) packets, rather than RX and TX packets, but otherwise the data is quite similarly presented:

    ```
    # netstat -i
    Name Mtu Net/Dest Address Ipkts Ierrs Opkts Oerrs Collis Queue
    lo0 8232 loopback localhost 125 0 125 0 0 0
    pcn0 1500 198.76.82.128 solaris 6780 0 4728 0 0 0
    ```

    Finally, Mac OS X is a bit more odd, but the same basic information is included in this longer output:

    ```
    # netstat -i
    Name Mtu Network Address Ipkts Ierrs Opkts Oerrs Coll
    lo0 16384 <Link> 1662 0 1662 0 0
    lo0 16384 127 localhost 1662 0 1662 0 0
    en0 1500 <Link> 00:30:65:3d:e8:10 6565 0 11226 0 0
    en0 1500 198.76.82.128 ds1-132.dsldesi 6565 0 11226 0 0
    ```

    Ipkts are input packets (RXs), and Opkts are output packets (TXs).

- 5. Let's turn from analyzing the system to exploring the network connectivity itself. There are two basic tools to accomplish this task: ping and traceroute.

    The ping command, which takes its name from the sound a submarine sonar makes when trying to identify a remote object, sends an ECHO_REQUEST packet to a specified remote system, times the duration of the send plus the echo back, and reports that to you.

    By convention, the first step with ping is to always try and check the connection to the router. If that's up and working, we've confirmed that the network card is working, the Ethernet wire is okay, and that this computer can talk to its Ethernet card.

    ```
    # ping -c 10 198.76.82.129
    PING 198.76.82.129 (198.76.82.129): 56 data bytes
    64 bytes from 198.76.82.129: icmp_seq=0 ttl=255 time=59.642 ms
    64 bytes from 198.76.82.129: icmp_seq=1 ttl=255 time=33.371 ms
    64 bytes from 198.76.82.129: icmp_seq=2 ttl=255 time=33.787 ms
    64 bytes from 198.76.82.129: icmp_seq=3 ttl=255 time=33.842 ms
    64 bytes from 198.76.82.129: icmp_seq=4 ttl=255 time=55.218 ms
    64 bytes from 198.76.82.129: icmp_seq=5 ttl=255 time=33.934 ms
    64 bytes from 198.76.82.129: icmp_seq=6 ttl=255 time=60.519 ms
    64 bytes from 198.76.82.129: icmp_seq=7 ttl=255 time=69.425 ms
    64 bytes from 198.76.82.129: icmp_seq=8 ttl=255 time=34.3 ms
    64 bytes from 198.76.82.129: icmp_seq=9 ttl=255 time=34.241 ms

    --- 198.76.82.129 ping statistics ---
    10 packets transmitted, 10 packets received, 0% packet loss
    round-trip min/avg/max = 33.371/44.827/69.425 ms
    ```

    The -c 10 specifies that ping should send 10 ECHO_REQUEST packets, spaced one second apart by default. Each ping displays its own statistics, where you can see that system vagaries cause the echo time to vary from 33.3 milliseconds to 69.4 milliseconds. The last two lines are the most important: percentage of loss (0%) and average speed (44.8ms).

    If you'd rather not see the individual lines of output, the -q flag hides them, limiting ping to the first and last lines of output only, as shown in this next example, where ping shows connection speed to the "other end of the wire," a DNS server at our ISP:

    ```
    # ping -q -c10 dns1.dsldesigns.com
    PING dns1.dsldesigns.com (192.216.138.10): 56 data bytes

    --- dns1.dsldesigns.com ping statistics ---
    10 packets transmitted, 10 packets received, 0% packet loss
    round-trip min/avg/max = 33.851/58.407/113.713 ms
    ```

    Remarkably similar performance to the local router, so the connection between them is clearly not a significant slowdown.
