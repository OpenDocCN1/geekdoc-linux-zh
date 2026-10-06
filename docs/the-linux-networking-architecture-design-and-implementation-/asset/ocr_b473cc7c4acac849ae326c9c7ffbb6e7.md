# 5.2 Managing Network Devices

NETDEV_REGISTER means that a network device was registered but no instance of it has yet opened.

NETDEV_UNREGISTER informs that a network driver was removed.

NETDEV_CHANGEMTU means that the MTU (Maximum Transfer Unit) changed.

NETDEV_CHANGEADDR means that the hardware address of a network device changed.

NETDEV_CHANGENAME means that the name of a network device changed.

When a registered handler routine is called, it can use the appropriate functions based on the type passed. For example, when a network device is deactivated (NETDEV_DOWN) in KIDS (see Chapter 22), the corresponding hook is deleted. The modifier notifier_call_chain(&netdev_chain, EVENT, dev), which will be described below, is used to call the notifier chain.

```
notifier_call_chain(&netdev_chain)
net/core/dev.c
```

notifier_call_chain(&netdev_chain, EVENT, dev) informs all handling methods registered in the list netdev about the events described above. notifier_call_chain() is very simple. The linking in the list is used to call all registered functions, one after the other. If one of the functions returns the constant NOTIFY_STOP_MASK, then the notification is stopped. Otherwise, all registered handler routines are informed about the event each time this function is called. The registered handler also decides whether the message is meaningful for it.

```
register_netdev_notifier()
net/core/dev.c
```

register_netdev_notifier(nb) is merely another representation of the method notifier_chain_register(&netdev_chain, nb), inserts into the notifier_block structure passed to the list netdev. The position within the list is determined by the priority.

```
unregister_netdev_notifier()
net/core/dev.c
```

unregister_netdev_notifier(nb) removes the specified notifier_block structure from the list netdev. The function notifier_chain_unregister() is used for this purpose.

# 5.2.5 Transmitting Over Network Devices

```
dev_queue_xmit()
net/core/dev.c
```

dev_queue_xmit(skb) is used by protocol instances of the higher protocols to send a packet in the form of the socket buffer skb over a network device, which is specified by the parameter skb->dev in the socket buffer structure. Section 6.2.2 explains how a packet is transmitted in detail.