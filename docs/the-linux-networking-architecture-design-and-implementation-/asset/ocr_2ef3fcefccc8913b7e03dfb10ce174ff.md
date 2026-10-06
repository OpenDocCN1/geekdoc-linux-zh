# 6.2 Processes on the Data-Link Layer

to the receiving network device, and the type of the data contained in the layer-2 data frame is recognized. For this purpose, Ethernet drivers can use the method eth_type_trans(). There are similar methods for other MAC technologies FDDI, token ring.

The demultlexing process takes place in the LLC layer at this point. The exact process will be explained in Section 6.3.1.

net_rx() completes the interrupt handling. First, the current time is set in skb->time, and the socket buffer is placed in the input queue. As compared with earlier versions of the Linux kernel, there is now only one queue having the name "backlog"; instead, each CPU stores "its" incoming packets in the structure softnet_data[cpu], input_pkt_queue. This means that the processor that handles the interrupt stores packets in its queue. This mechanism was introduced to avoid kernel-wide locks of a single queue.

Once the packet is placed in the queue, the interrupt handling is complete. As was explained in Section 2.2.2, the handling routine of a hardware interrupt should run only the operations absolutely required to ensure that other activities of the computer (software interrupts, tasklets, processes) will not be unnecessarily interrupted.

Incoming packets are further handled by the software interrupt NET_RX_SOFTIRQ, which replaces the net bottom half (NET_BH) used in earlier versions of the Linux kernel. NET_RX_SOFTIRQ is marked for execution by cpu_softirq(cpu, NET_RX_SOFTIRQ). This mechanism is similar to bottom halves, but the use of interrupts allows much more parallelism and makes possible improved performance on multiprocessor systems. (See Section 2.2.3).

The path of a packet initially begins in the queue for incoming packets. The interrupt handling was terminated, and the kernel continued handling the activity (process, software interrupt, tasklet, etc.). When the process scheduler (schedule()) is invoked once after a certain interval, it first checks for whether a software interrupt is marked for execution. This is the case here, and it uses do_softirq() to start the soft-IRQ. The following sections as this concern the NET_RX soft-IRQ:

```
net_rx_action() net/core/dev.c
```

> ¹net_dev_max_backlog specified the length of the (only) input queue, backlog, in earlier versions of the Linux kernel, and was initialized with the value 300 (packets). In the new kernel, this is the maximum length of the input queues of the processors.