characteristics to pinpoint specific network traffic. These qualifiers include the following:

+   - from or src
+   - to or dst
+   - ether

The from and src qualifiers are used with the host, net, ipaddr, etheraddr, port, or rpc primitives to filter based on a specific destination address or port. The qualifiers to or dst modify the primitives just mentioned, but will result in the captured packets going to a particular address or port. The ether modifier resolves a name to a datalink address when used with the host primitive. To illustrate the use of the host keyword, let’s suppose we want to capture traffic from a particular host only. The following tcpdump command could be used:

```
```
# tcpdump from host monet
```
```

Contrast the command above with the following:

```
```
# tcpdump host monet
```
```

In the latter example, all the traffic involving monet, which includes packets being sent to and received from monet, will be displayed. In the former example, only traffic received from monet will be displayed. As you can see, this can make a big difference when attempting to isolate a network problem.

# ## Tcpdump Examples

Table 4.15 contains a list of command examples and associated description of each one. It is hoped that these commands will provide a quick reference on using the tcpdump in real-world situations.

# # Traceroute Tool

# ## General Description

The traceroute command examines and records the path to a specified network destination. Within a traditional IP network, one or more routers are used to provide connectivity between different IP networks. IP routers come in different shapes and sizes,