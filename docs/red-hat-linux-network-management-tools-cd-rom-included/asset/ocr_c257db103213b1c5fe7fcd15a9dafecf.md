for this noticeable packet loss is that some of the critical Internet routers might be quite busy or even overloaded with network traffic. As a result, some of the ICMP requests might be discarded because the requests expired before they were delivered to the final destination. Also, the relative load of the target device can be a factor because these systems might not have the computing resources to answer all network requests as required. Because of the popularity of this site, it is not unreasonable to think that both the servers and the networks that connect them are all quite busy or even overloaded. An overloaded condition will occur when too many users are using resources from the system at the same time.

Sometimes it is desirable to provide additional time for acknowledging each **ping** request instead of using the default value of one second. If additional time is desired between successive ICMP requests, the `-i` option can be used, followed by the desired value. The interval should be long enough to provide the required amount of time for the remote system to respond. When we increase the timeout value as suggested, we will generally notice less packet loss. The command

```
`ping -c 10 www.whitehouse.gov -i 5`
```

adds a five-second delay to each request, thus providing additional time for the processing of the requests through the network and to the destination server. Using the command above, the following was produced:

```
```
PING www.whitehouse.com (209.67.27.247): 56 data bytes
64 bytes from 209.67.27.247: icmp_seq=1 ttl=244 time=240.1 ms
64 bytes from 209.67.27.247: icmp_seq=2 ttl=244 time=240.1 ms
64 bytes from 209.67.27.247: icmp_seq=3 ttl=244 time=240.0 ms
64 bytes from 209.67.27.247: icmp_seq=4 ttl=244 time=240.0 ms
64 bytes from 209.67.27.247: icmp_seq=5 ttl=244 time=250.1 ms
64 bytes from 209.67.27.247: icmp_seq=6 ttl=244 time=240.1 ms
64 bytes from 209.67.27.247: icmp_seq=7 ttl=244 time=240.1 ms
64 bytes from 209.67.27.247: icmp_seq=8 ttl=244 time=240.2 ms
64 bytes from 209.67.27.247: icmp_seq=9 ttl=244 time=250.1 ms

 --- www.whitehouse.com ping statistics ---
10 packets transmitted, 9 packets received, 10% packet loss
round-trip min/avg/max = 240.0/242.3/250.1 ms
```
```