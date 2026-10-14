# 34.6.1 Determining If a Host Is Online

Use ping to determine whether a particular system is currently connected to the Internet. It tells the time it takes for an IP packet to travel from your system to the other one, and back.

Type ping followed by the hostname or numeric IP address of the system you want to check; if your system is online and the system to be checked is also online, ping should continually output lines telling how long the latency, in milliseconds, is between the two systems. Type CTRL-C to interrupt it and stop pinging.

⇒ To ping the host bfi.org, type:

```
$ ping bfi.org RET
PING bfi.org (209.196.135.250): 56 data bytes
64 bytes from 209.196.135.250: icmp_seq=0 ttl=63 time=190.0 ms
64 bytes from 209.196.135.250: icmp_seq=1 ttl=63 time=159.9 ms
64 bytes from 209.196.135.250: icmp_seq=2 ttl=63 time=160.5 ms
CTRL-C
--- bfi.org ping statistics ---
3 packets transmitted, 3 packets received, 0% packet loss
round-trip min/avg/max = 159.9/170.1/190.0 ms
$
```

In this example, the host bfi.org was pinged and a total of three pings were sent and received before the user typed CTRL-C to interrupt it. As long as these ping lines are output, you know that the other machine is connected to the Internet (or at least to the same network that your localhost is connected to).

You really don’t need to analyze the information on each line of a ping message—the only useful information is the number at the end of the line, which tells you how many milliseconds it took to go out to the Internet, touch or “ping” that host, and come back. The quicker the better—pings that are four or five digits long (or greater) mean a slow connection between the two machines. When you interrupt the ping, some statistics are output, including the minimum, average, and maximum number of milliseconds it took to ping

> 4 "I named it after the sound that a sonar makes, inspired by the whole principle of echo-location," said the original author of ping, Mike Muss. He died in an automobile accident in November 2000.