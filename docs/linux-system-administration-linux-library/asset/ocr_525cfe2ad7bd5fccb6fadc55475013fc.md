# traceroute

The traceroute utility will help you track down problems in your network or determine a problem is actually outside your network. The traceroute utility prints the route that packets take to a specific network host and three measurements of the time in milliseconds for each hop. Listing 9.1 shows the traceroute command in action. Using this information, you can determine whether there is a delay at one of the network stops that your data makes between the sender and receiver, thereby providing useful information when you are troubleshooting a network problem. Listing 9.1 shows a slow increase in the times between the first hop and the final one, but there's a jump at the final hop, suggesting that the destination is overloaded or on a slow link. In this case, you can't do anything to improve network performance. If you'd seen a big jump within your network, it's possible that reconfiguring your network or upgrading its hardware could improve performance.

Listing 9.1 Output of the traceroute Command

```
$ /usr/sbin/traceroute www.linux
taceroute to www.linux.org (198.182.196.56), 30 hops max, 40 byte
  ->Capackets
1 ds1-254-070.ds1-isp.net (216.254.70.1) 30.599 ms 46.390 ms
2 border9.fe4-0.speakeasy-6.nyc.pnap.net (209.191.175.196)
  ->CA33.701 ms 37.445 ms 26.314 ms
3 core2.fe0-0-fenet1.nyc.pnap.net (209.191.128.66) 26.032 ms
  ->CA25.860 ms 25.5 97 ms
4 POS3-3.GW12.NYC4.ALTER.NET (157.130.253.217) 26.243 ms
  ->CA38.132 ms 25.969 ms
5 505.ATM2-0.XR1.NYC4.ALTER.NET (152.63.22.66) 26.275 ms 25.030 ms
  ->CAMS 26.302 ms
6 189.at-1-0-0.TR1.NYC8.ALTER.NET (152.63.21.90) 27.014 ms
  ->CA27.310 ms 26.042 ms
7 124.at-6-0.TR1.DCA6.ALTER.NET (152.63.2.165) 35.369 ms
  ->CA35.692 ms 34.126 ms
```