![](bbox=[0.18, 0.13, 0.65, 0.38])

Figure 15.1: winipcfg – Windows network interface

Once you're certain that each systems network interface is operational, check reachability by using the ping command to send an ICMP echo request between problem systems (Example 15.2). Echo round-trip time and dropped-packet rate statistics are displayed, indicating the overall health of the communication path between the participating systems.

# Example 15.2 ping – Verify Communication Path

```
# ping foo.bar.com
PING foo.bar.com (130.111.58.1): 56 data bytes
64 bytes from 130.111.58.1: icmp_seq=0 ttl=252 time=8 ms
64 bytes from 130.111.58.1: icmp_seq=1 ttl=252 time=3 ms
64 bytes from 130.111.58.1: icmp_seq=2 ttl=252 time=8 ms
64 bytes from 130.111.58.1: icmp_seq=3 ttl=252 time=5 ms
--- foo.bar.com ping statistics ---
4 packets transmitted, 4 packets received, 0% packet loss
round-trip min/avg/max = 3/5/8 ms
```

In most cases reachability problems will be related to routing configuration or an incorrectly assigned subnet mask. Use the netstat command to display additional interface statistics (Table 15.2) including netmask and routing information (Example 15.3). An interval flag may be used with netstat to collect statistics snapshots over time.

# Table 15.2 Useful netstat Options

| Option | Description |
| -i | Interface state, packet rates and errors. |
| -a | Display socket connection status. |