# ### 5.13 More about traceroute

You need to be aware of a few points when interpreting **traceroute** output.

+   1. the path that **traceroute** prints isn't cast in stone – it can vary from day to day, or in exceptional circumstances even from packet to packet. Figure 5.15 shows two **traceroutes** we ran within a few seconds of one another, giving very different paths.

```
```
alice% traceroute -w 1 -n 195.66.224.14
traceroute to 195.66.224.14 (195.66.224.14), 30 hops max,
1 192.0.2.1 5 ms 5 ms 5 ms
2 194.73.5.1 249 ms 388 ms 698 ms
3 194.74.16.225 893 ms 578 ms 546 ms some routers may
4 194.72.9.148 55 ms 37 ms 35 ms not respond at all
5 194.74.65.21 31 ms 33 ms 28 ms
6 * * * *
7 * * * *
8 * * * * some responses
9 * * * * from a router may
10 195.66.224.14 49 ms * * be dropped

alice% traceroute -w 1 -n 195.66.224.14
traceroute to 195.66.224.14 (195.66.224.14), 30 hops max,
1 192.0.2.1 6 ms 5 ms 5 ms
2 194.73.5.1 64 ms 216 ms 232 ms the routers may
3 194.74.16.225 31 ms 34 ms 35 ms not be the same
4 194.72.9.148 33 ms 29 ms 30 ms every time (e.g.
5 194.74.65.21 37 ms 38 ms 33 ms ten hops on the
6 195.66.224.14 31 ms * * first run, only six
alice% on the second)
```
```

**Figure 5.15** Two **traceroutes** with very different paths

![](bbox=[0.24, 0.56, 0.79, 0.73])

![](bbox=[0.24, 0.73, 0.79, 0.88])

**Figure 5.16** Why successive **traceroute** outputs can differ