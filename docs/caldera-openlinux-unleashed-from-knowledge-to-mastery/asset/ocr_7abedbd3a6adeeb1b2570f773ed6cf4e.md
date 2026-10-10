# Note

Ports can only be specified in combination with the TCP, UDP, and ICMP protocols.

# Note

It is important to remember that, in general, the source and destination ports are not the same. For example, if you want to limit your local network's access to the Internet by only allowing users to connect to Web servers, you would not do it by allowing only packets whose source and destination port are 80 or www. You would omit the source port (or limit it to ports above 1023) and make the destination port 80. For example, with a local network at 192.168.1.0, you might set up a rule with the following addresses:

```
-s 192.168.1.0/24 1024: -d 1 192.168.1.0 www
```

Don't forget that you can only specify ports in conjunction with the TCP, UDP, or ICMP protocols. In this case, you would specify the TCP protocol along with the preceding address specifications.

# Note

Do not block all ICMP type 3 packets (destination-unreachable). If you do, you will never get Host unreachable or No route to host errors. This is not a serious problem in and of itself, but it means that you will never find out that connections can't be completed because you won't get the message. The messages will just sit and wait until they time out.

More serious, however, is the fact that these packets are used for MTU discovery. MTU discovery tries to figure out the size of the largest packet that can be sent without the packet being fragmented (avoiding fragmentation helps improve performance). It works by sending packets with the Don't Fragment bit set. If it receives a reply saying that fragmentation is needed but the Don't Fragment bit was set (ICMP type fragmentation-needed), it sends smaller and smaller packets until the packet goes through. The fragmentation-needed packet is a type of destination-unreachable packets. If it is blocked, the local host will never reduce the size of the packets it is sending, and network performance will be extremely slow or even stopped.