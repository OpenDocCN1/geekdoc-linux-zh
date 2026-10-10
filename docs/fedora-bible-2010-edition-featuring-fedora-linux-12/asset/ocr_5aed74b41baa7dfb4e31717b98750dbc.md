```
64 bytes from www.example.com (208.77.188.166): icmp_seq=9 ttl=255
time=0.365 ms
64 bytes from www.example.com (208.77.188.166): icmp_seq=10 ttl=255
time=0.367 ms

--- example.com ping statistics ---
10 packets transmitted, 10 packets received, 0% packet loss, time 9011ms
rtt min/avg/max/mdev = 0.351/0.402/0.457/0.042 ms, pipe 2
```

A line of output is printed each time a packet is sent and received in return. It shows how much data was sent and how long it took for each package to be received. After you have watched this for a while, press Ctrl+C to stop ping. At that point, you will see statistics on how many packets were transmitted, received, and lost.

If you don't see output that shows packets have been received, it means you are not contacting the other computer. Try to verify that the names and addresses of the computers that you want to reach are in your `/etc/hosts` file or that your DNS server is accessible. Next, confirm that the names and IP addresses you have for the other computers you are trying to reach are correct (the IP addresses are the most critical).

# Is your Ethernet connection up?

Using the `ip` command, you can determine whether your Ethernet and other network interfaces are up and running. Type the following command:

```
# ip -s link
```

The output that appears is similar to the following:

```
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 16436 qdisc noqueue state UNKNOWN
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    RX:  bytes  packets  errors  dropped overrun  mcast
            1756      20        0        0        0        0
    TX:  bytes  packets  errors  dropped carrier collsns
            1756      20        0        0        0        0
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo fast
    state UP  qlen 1000
    link/ether 00:11:11:4c:dc:0f brd ff:ff:ff:ff:ff:ff
    RX:  bytes  packets  errors  dropped overrun  mcast
         672375007  912637      0        0        0        55
    TX:  bytes  packets  errors  dropped carrier collsns
         51041835  743940      0        0        0        0
```

In this example, two network interfaces are on the current computer. The second section shows your Ethernet interface (eth0) and its Ethernet hardware address and that it is UP. The next lines provide information on packets that have been sent, along with the number of errors and collisions that have occurred.