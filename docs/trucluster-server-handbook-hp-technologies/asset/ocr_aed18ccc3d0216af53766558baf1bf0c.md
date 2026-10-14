# 17.6.1 The Node Announcement

The CNX pinger thread repeatedly sends out an announcement message until the system becomes a cluster member. Once the system becomes a cluster member the CNX pinger thread kills itself.

Essentially what happens here is the CNX pinger thread broadcasts an announcement message across the cluster interconnect using the ICS BOOT channel³. If there are any other systems that are up to receive the announcement message, they will respond by exchanging information with the booting system. Included in the node announcement is the cluster name, node name, incarnation, member ID, version, and how it can be reached via ICS.

You may observe a message similar to the following:

```
CNX MGR: Node molari id 1 incarn 0x914b6 attempting to form or join cluster babylon5
```

Figure 17-5 illustrates the node announcement communication flow.

When the announcement message is received by a cluster member (or potential member), the systems establish a communication channel to each other and exchange more information to flesh out each other's CSB information.

![](bbox=[0.2, 0.73, 0.85, 0.88])

Figure 17-5: CNX Node Announcement

5 See Chapter 18 for more information on the ICS subsystem.