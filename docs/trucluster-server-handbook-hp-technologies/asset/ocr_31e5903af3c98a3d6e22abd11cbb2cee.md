```
# cluamgr -r start
```

```
# arp clua_den_virt
clua_den_virt (192.206.126.99) -- no entry
```

```
# netstat -r | wc -l
17
```

```
# netstat -r

192.206.126    localhost    UG    0    0 100
clua_den_virt  localhost    UH    0    0 100
```

The following output is from a client node. We ran the routed daemon and specified that it run silently (-q no outgoing route advertising) and display a trace of its activities (-t). The routed daemon understands the RIP protocol just as the gated daemon. Therefore, it is legitimate to mix routed and gated daemons in a network as long as both do not run in the same network node. The first part of the output is standard routed startup sequence where it sends a broadcast (192.168.0.255) to announce its presence and hears back from itself on port 520 (192.168.0.104.520). So far, no excitement.

```
# routed -q -t

Tracing packets started Wed Sep 18 20:04:53 2002

Wed Sep 18 20:04:53:
ADD dst 127.0.0.0, router 127.0.0.1, metric 1,
flags UP state PASSIVE|INTERFACE|CHANGED|EXTERNAL timer 0
ADD dst 192.168.0.0, router 192.168.0.104, metric 1,
flags UP state INTERFACE|CHANGED timer 0
STOCADDRT: File exists
REQUEST to 192.168.0.255 0 Wed Sep 18 20:04:53:
REQUEST from 192.168.0.104.520 Wed Sep 18 20:04:53:
```

The routed trace after this point happened just after the "cluamgr -r start" command was issued on the cluster member. The gated daemon on the cluster (at address 192.168.0.69) advertised two items to the client, one network route that identifies a router with which to communicate when attempting to access a node on network 192.206.126, and one host route that identifies a router with which to communicate when attempting to access the interface at address 192.206.126.99. These items were added to the current information in the client's routing table.