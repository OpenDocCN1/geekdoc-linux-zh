# Managing Layer-3 Protocols

If the packet be forwarded successfully to a network adapter, then the kernel assumes that this transmission process is completed, and the kernel turns to the next packet (qdisc_run()).

Transmitting over NET_SOFT-IRQ The NET_SOFTIRQ is an alternative for sending packets. It is marked for execution (_cpu_raise_softirq()) by the method netif_schedule().netif_schedule() is invoked whenever a socket buffer cannot be seen over the normal transmission process, described in the previous section. This problem can have several causes:

+   - Problems occurred when a packet was forwarded to the network adapter (e.g., no free spaces).

+   - The socket buffer has to be sent later, to honor special handling of packets. In the case of traffic shaping, packets might have to be delayed artificially, to maintain a specific data rate. For this purpose, a timer is used, which starts the transmission of the packet when the transmission time is reached. (See Figure 6–4).

Now, if NET_TX_SOFTIRQ is marked for execution by netif_schedule(), it is started at the next call of the CPU scheduler.

```
net_tx_action()
```

net_tx_action() is the handling routine of the NET_TX_SOFTIRQ software interrupt. The main task of this method is to call the method qdisc_restart() to start the transmission of the packets of a network device.

The benefit of using the NET_TX_SOFTIRQ software interrupt is that processes can be handled in parallel in the Linux network architecture. In addition to NET_RX_SOFTIRQ, which is responsible for the main protocol handling, the NET_SOFT-IRQ can also be used to increase the throughput considerably in multiprocessor computers.

# MANAGING LAYER-3 PROTOCOLS

The previous section of this chapter described the path of a packet between a network adapter and the interface to higher protocol instances. This section discusses this interface in detail. First, we will explain how new protocols can be added because only protocols of the network layer (IP, ARP, IPv6, IPX) are added to the Linux network architecture over this interface, it is also referred to as the interface to the network layer or layer-3 protocols in the following discussion.

In the Linux kernel, we distinguish between two types of layer-3 protocols, where the first type is used mostly for analysis purposes:

+   - A protocol receives all packets arriving at the interface to the layer-3 protocols.

+   - A protocol receives only packets with the correct protocol identifier (e.g., 0x0800 for the Internet Protocol).