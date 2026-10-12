Figure 4-16 summarizes the common tasks one could perform to survey in the IP layer.

![](bbox=[0.25, 0.18, 0.8, 0.6])

Figure 4-16 Survey in the IP layer

Figure 4-17 shows a sample ping output. The ping command tells us whether we could reach the destination address and, if yes, how much time it took. So, if there was no reply from the destination address (meaning, not able to reach), then we should continue our check below the IP layer. If there was a reply, then we should continue our check above the IP layer.

```
# ping -c 3 -R 172.16.3.189
PING 172.16.3.189 (172.16.3.189) 56(124) bytes of data.
64 bytes from 172.16.3.189: icmp_seq=1 ttl=64 time=17.9 ms
RR: 172.16.3.131
172.16.3.189
172.16.3.189
172.16.3.131

64 bytes from 172.16.3.189: icmp_seq=2 ttl=64 time=0.683 ms  (same route)
64 bytes from 172.16.3.189: icmp_seq=3 ttl=64 time=0.635 ms  (same route)

--- 172.16.3.189 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2011ms
rtt min/avg/max/mdev = 0.635/6.416/17.936/8.164 ms
```

Figure 4-17 Using ping for diagnosis