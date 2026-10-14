you can move to the next section, Is the Remote Port Open? If you can’t ping web1, try to identify another host on that network and see if you can ping it. If you can, then it’s possible web1 is down or blocking your requests, so move to the next section.

If you can’t ping any hosts on the network, packets aren’t being routed correctly. One of the best tools to test routing issues is traceroute. Once you provide traceroute a host, it will test each hop between you and the host. For example, a successful traceroute between ubuntu1 and web1 would look like the following:

```
$ traceroute 10.1.2.5
traceroute to 10.1.2.5 (10.1.2.5), 30 hops max, 40 byte packets
 1  10.1.1.1 (10.1.1.1)  5.432 ms  5.206 ms  5.472 ms
 2  web1 (10.1.2.5)  8.039 ms  8.348 ms  8.643 ms
```

Here you can see that packets go from ubuntu1 to its gateway (10.1.1.1), and then the next hop is web1. This means it’s likely that 10.1.1.1 is the gateway for both subnets. On your network you might see a slightly different output if there are more routers between you and your host. If you can’t ping web1, your output would look more like the following:

```
$ traceroute 10.1.2.5
traceroute to 10.1.2.5 (10.1.2.5), 30 hops max, 40 byte packets
 1  10.1.1.1 (10.1.1.1)  5.432 ms  5.206 ms  5.472 ms
 2  * * *
 3  * * *
```

Once you start seeing asterisks in your output, you know that the problem is on your gateway. You will need to go to that router and investigate why it can’t route packets between the two networks. If instead you see something more like

```
$ traceroute 10.1.2.5
traceroute to 10.1.2.5 (10.1.2.5), 30 hops max, 40 byte packets
 1  10.1.1.1 (10.1.1.1)  5.432 ms  5.206 ms  5.472 ms
 1  10.1.1.1 (10.1.1.1) 3006.477 ms !H 3006.779 ms !H 3007.072 ms
```

then you know that the ping timed out at the gateway, so the host is likely down or inaccessible even from the same subnet. At this point if I hadn’t