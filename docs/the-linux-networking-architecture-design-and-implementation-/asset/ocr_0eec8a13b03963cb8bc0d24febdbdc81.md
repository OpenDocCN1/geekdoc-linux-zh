# 5.3 Network Drivers 103

```
dev_free_skb(skb);
#endif
    return 0;
}
```

# Receiving Packets and Messages from a Network Adapter

```
net_interrupt() drivers/isa_skeleton.c
```

A network adapter uses interrupts and its driver-specific interrupt-handling routine to communicate with the operating system. More specifically, the network adapter triggers an interrupt to stop the current processor operation and notify it about an event. When a network adapter uses an interrupt, we generally distinguish between three different events:

+   * Receive a data packet: The network adapter has accepted and buffered a data packet and now wants to forward this packet to the operating system.
* Acknowledge a packet transmission: The network adapter uses this interrupt to acknowledge that a packet previously forwarded by the operating system was sent and that there is now a space available in the ring buffer. However, this acknowledgment does not mean that the receiver has received the packet successfully; it merely means that the network adapter has put the packet successfully to the medium.
* Notify an error situation: Depending on the network adapter used, an interrupt can be used to notify the driver of error situations.

Figure 5–5 shows how the interrupt handling routine of a network driver works. First, we should set an IRQ lock to prevent the function from being executed more than once at the same time. In older versions of the Linux kernel, the flag

![](bbox=[0.142, 0.663, 0.558, 0.813])

FIGURE 5–5 A network adapter uses an interrupt to send messages.