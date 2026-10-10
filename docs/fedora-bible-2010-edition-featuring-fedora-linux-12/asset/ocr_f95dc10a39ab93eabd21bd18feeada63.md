To determine if your data link is saturated, the act of pinging an outside host can tell much of the story. Much higher than usual latency is a dead giveaway. Normal ping latency (that is, the time it takes for a ping response to come back from a remote host) looks like the following:

```
# ping www.example.com
PING www.example.com (192.0.32.10) from 10.0.0.11: 56(84) bytes of data
64 bytes from 192.0.32.10: icmp seq=1 ttl=49 time=40.1 ms
64 bytes from 192.0.32.10: icmp seq=2 ttl=49 time=42.5 ms
64 bytes from 192.0.32.10: icmp seq=3 ttl=49 time=39.5 ms
64 bytes from 192.0.32.10: icmp seq=4 ttl=49 time=38.4 ms
64 bytes from 192.0.32.10: icmp seq=5 ttl=49 time=39.0 ms

--- www.example.com ping statistics ---
5 packets transmitted, 5 received, 0% loss, time 4035ms
rtt min/avg/max/mdev = 38.472/39.971/42.584/1.432 ms
```

In the preceding example, the average time for a ping packet to make the round trip was about 39 thousandths of a second.

A ping to a nearly saturated link will look like the following:

```
# ping www.example.com
PING www.example.com (192.0.32.10) : from 10.0.0.11: 56(84)bytes of data
64 bytes from 192.0.32.10: icmp seq=1 ttl=62 time=1252 ms
64 bytes from 192.0.32.10: icmp seq=2 ttl=62 time=1218 ms
64 bytes from 192.0.32.10: icmp seq=3 ttl=62 time=1290 ms
64 bytes from 192.0.32.10: icmp seq=4 ttl=62 time=1288 ms
64 bytes from 192.0.32.10: icmp seq=5 ttl=62 time=1241 ms

--- www.example.com ping statistics ---
5 packets transmitted, 5 received, 0% loss, time 5032ms
rtt min/avg/max/mdev = 1218.059/1258.384/1290.861/28.000 ms
```

In this example, a ping packet took, on average, 1.3 seconds to make the round trip. From the first example to the second example, latency increased by a factor of 31! A data link that goes from working normally to slowing down by a factor of 31 is a clear sign that link utilization should be investigated.

For a more accurate measure of data throughput, a tool such as tcpt can be used. To test your connection with tcpt you must have installed the tcpt RPM package on machines inside *and* outside of your network. Install the tcpt package if needed using the *yum* command. If you are not sure whether the package is installed, simply type **tcpt** at a command prompt. You should see something like the following:

```
# tcpt
Usage: tcpt -t [-options] host [ < in ]
	tcpt -r [-options > out]

Common options:
-4  	Use IPv4
```