Instead of writing down a table of the configuration for each machine, we show it directly on the diagram (which is how we do it in real life).

In the next module we use this notation (Figure 6.2):

+   on a machine, a route is shown as
+   
+           R(10.6.6.0, 255.255.255.0 -> 10.4.4.46=Richard)
+   
+   which means a route to the network/range 10.6.6.0, netmask 255.255.255.0 uses 10.4.4.46 (the router Richard) as gateway
+   
+   * a large curved arrow, usually marked **dg**, points from a machine to its default gateway router.

![](bbox=[0.19, 0.27, 0.85, 0.51])

> **Tip**: when we use diagrams like this on-site for building a real network, we often make a photocopy of it. Then, as we configure a parameter, we scratch it off using a fluorescent highlighter, so it's easy to see what we have and haven't done.

# Configuring a machine to use multiple routers

Use the `route add` command to create a route to the routers, just as we did in the previous chapter. For example, if Bob is a Linux box, to tell it to use Robert and Richard to get to the adjacent networks (but nothing else) you might use:

```
```
route add -net 10.1.1.0 netmask 255.255.255.0 gw 10.4.4.14
route add -net 10.6.6.0 netmask 255.255.255.0 gw 10.4.4.46
```
```

whereas on Windows it would be:

```
```
route add 10.1.1.0 mask 255.255.255.0 10.4.4.14
route add 10.6.6.0 mask 255.255.255.0 10.4.4.46
```
```