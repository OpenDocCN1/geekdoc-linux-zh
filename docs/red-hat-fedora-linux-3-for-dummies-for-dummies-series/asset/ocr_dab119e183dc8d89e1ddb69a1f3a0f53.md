This example assumes that another computer has the IP address **192.168.1.254**. Adjust the address you use to work with your network. You should see a response similar to what’s shown in this bit of code:

```
PING 192.168.1.2 (192.168.1.2): 56 data bytes
64 bytes from 192.168.1.254: icmp_seq=0 ttl=32 time=3.1 ms
64 bytes from 192.168.1.254: icmp_seq=1 ttl=32 time=2.3 ms
--- 192.168.1.2 ping statistics ---
4 packets transmitted, 4 packets received, 0% packet loss
round-trip min/avg/max = 2.3/2.5/3.1 ms
```

If you see a continuous stream of returned packets and the packet loss is 0 or near it, your network is working. If not, the problem may be in the other machine. Review the troubleshooting steps in this chapter. Note that the ICMP is taking about 1 full millisecond (ms) longer to travel to the external computer than to the loopback device. The reason is that the loopback is completely internal to the Linux computer.