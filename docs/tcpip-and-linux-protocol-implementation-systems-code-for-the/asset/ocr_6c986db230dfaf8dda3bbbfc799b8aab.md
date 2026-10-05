# The Brief Life of a Packet 75

| Application blocked/descheduled during this period . . . until data ready |
|---|---|
| Application | |
| Transport | X |
| Network | X |
| Driver | X |
| Wire | ----| Time |

**Figure 3.2** The overall reception process: from wire to application.

Physical reception causes hardware to wake up, and typically interrupt. Most modern network devices include both interrupt and DMA hardware. The interrupt service routine pulls a packet off a device and puts it in memory, and flags the network bottom half that the packet(s) below are ready. Bottom halves and other Linux mechanisms (software interrupts, tasklets, and other SMP capabilities) are discussed in Chapter 2 and later on in the book.

The general system scheduler (after a system call) runs the network half (and can dispatch tasklets or software interrupts) on completion of any kernel work on behalf of any process that called a system call. The bottom halves basically complete work that the hardware started—for example, they can dequeue packets in the interface queue for IP input and send any more packets waiting to send.

IP input checks packets, carries out its reassembly work, and gets a route if the packet is to be forwarded rather than a local application process. If it is for local delivery, it demiplexes the packets according to the IP protocol to the appropriate transport handler receive function (UDP, TCP, and so on).

TCP (and UDP) input then do further packet checking, update state machinery, and then demiplex the packet further to the correct socket (i.e., to the queue of data pending for any process that has an outstanding read on that socket, which is connected to the appropriate port numbers).

Once the transport protocol demiplexinging routine has put data on the appropriate socket receive queue, it wakes up any process waiting for data, thus making any such process ready for general running by the system scheduler.