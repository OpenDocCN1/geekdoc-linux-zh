
## 658 TCP/IP and Linux Protocol Implementation

There are a number of scheduling dimensions:

**Priority levels.** If we implement a priority system, how many levels should there be? It is not obvious why you want more than two or three. Since a higher-priority queue services services first, this approach can cause starvation for lower-priority queues, unless we have some sort of admission control for the overall occupancy of the higher-priority service in the network, or on any given path.

**Work-conserving or not.** We must decide if delay/jitter control is required. Is the cost of implementation of delay/jitter control in a network acceptable? In practice it isn't.

**Degree of aggregation.** What is the flow granularity? Do we have per-application flow, or per-user or per-end system? It is a question of tradeoff the cost of implementation of the scheduling system (in terms of state, state setup messages, classification frequency, and complexity) and the granularity of control.

**Servicing within a queue.** Can we get away with FCFS within a queue? Should we check for other parameters? What other added processing overhead may be there (e.g., network management/logging). What kind of queue management do we need in an emergency?

## 9.6.1 Common Scheduling Disciplines

Let's now look at some of the more common systems for picking which to send next, and when to send it.

**Priority queuing.** We have $K$ queues: $1 <= k <= K$. Queue $k + 1$ has greater priority than queue $k$. In other ways, higher-priority queues are serviced first. This is very simple to implement and has a low processing overhead. It offers fairly relative priority in practice (assuming we keep no history), and this offers no deterministic performance bounds. In terms of fairness and protection, it is not max-min fair and it hazards the risk of starvation of lower-priority queues.

**Generalized processor sharing (GPS).** This is a work-conserving scheme, and it serves an infinitesimally small amount of data from flow $i$ and then visits the next flows round robin. This provides a max-min fair share to each flow. However in practice it is not directly implementable. Instead, it is used as a baseline abstract reference for comparing other schedulers.

**Weighted round robin.** This is the simplest attempt at an implementable approximation of GPS. The queues are visited round robin in proportion to weights assigned. Since different flows have different mean packet sizes, the weight has to be divided by mean packet size for each queue. Because mean packet size is unpredictable, this may cause unfairness. The service is max-min fair over long time scales. We must have more one to visit each flow/queue. This means that there are deviations from fairness for short-lived flows.

**Deficit round robin (DRR).** DRR does not need to know the mean packet size. Each queue has a deficit counter (dc); initially, this is set to zero. The DRR scheduler attempts to serve one quantum of data from a non-empty queue:

```
if size <= quantum + dc
    packet at head served
    dc = quantum + dc - size
else
    dc += quantum
```

Queues that are not served during a round build up credits. The quantum is normally set to be the maximum expected packet size. This ensures that each packet is served per round per non-empty queue: RFB: 37/r(T=maxpacketservetime, r=linkrate). It works best for flows with small packet sizes and is fine for a small number of flows.

**Weighted fair queuing (WFQ).** The WFQ scheduler is also based on GPS. It is effectively a GPS emulation that serves to produce finish numbers for packets in the queue. The simplification is that the scheme is packet time scale instead of the GPS time scale that serves packets bit by round robin. The finish number is the time that a packet would have completed service, under the ideal (bit-by-bit) GPS. Packets are tagged with the finish number, then the smallest finish number across the queues is served first in the next round.

The round is a cycle of execution defined by an idealized bit-by-bit robin-server. The finish number is calculated from the round. If the queue is empty, the finish number is the number of bits in packet + round-number. If the queue non-empty, the finish number is highest current finish number for queue + number of bits in packet.

When a flow completes (empty queue), there is one less flow in the round, so R increases more quickly. As more flows complete, R increases more quickly, and so on. Because of this, WFQ needs to evaluate each time a packet arrives or leaves, which can be a significant processing overhead.

In addition to the schedule, r, we have to have a buffer-drop policy to handle overflows. If packets arrive at full queue, we can drop packets already queued in order of decreasing finish numbers, for example. This can be used for best-effort queuing, or for providing a guaranteed data rate and deterministic end-to-end delay. WFQ is used in the real world, as is. There are several alternatives also available, including self-clocked fair queuing (SCFQ), worst-case fair-weighted fair queuing (WF2Q), and a neat statistical approximation, stochastic fairness queuing (SFQ).

## 9.6.2 Class-Based Queuing

As well as organizing scheduling with a traffic class, we need to have a way of managing a set of different traffic classes, potentially with a range of different, appropriate scheduling algorithms. There are two specific approaches. One is class-based queuing (CBQ), and the other is the so-called (after Clark/Shenker).

![](img/06c1ba8be5c124a63e12ebd_715.png)
Figure 9.8 Class-based queuing.

## 9.7 Queue Management

Having revised scheduling, which addresses the problems of organizing packets within queue, let's take a look at queue management. Queue management entails the tasks of ensuring buffers are available, using memory management, and deals with packet dropping.

Congestion is typically caused (as we have seen previously) by a range of misfortunes, including misbehaving sources, routing instability, and network failure. Congestion could hurt many flows, so we need to manage it. Typically, we drop packets. Key questions: Do we drop new packets until the queue clears, or do we admit new packets and drop existing packets? How much history, explicitly or implicitly, concerning misbehaving flows, do we keep?

Packet drop mechanisms include:

- **Drop from tail.** Given a FIFO queue, tail-drop is clearly easy to implement. Of course, delayed packets within a queue may expire. own- **Drop from head.** This may be harder to implement (especially if some of a queue is no longer owned by the IP level, but in the buffer is owned (or on) the NIC). The idea here is that old packets are purged first, and this ought to be good for real time, and even better for TCP. In practice, it's not widely implemented.
- **Random drop.** Random drop, especially in its random detection guise, is popular. If the random number is chosen carefully to be uniform (proportional to the queue length), this is in some senses fair, since if all sources are behaving correctly, they are equally likely to see the drop; if there are misbehaving sources, then they will be proportionally heavily.
- **Flush queue.** When a queue is overloaded, there is also the option to drop all packets in the queue. This is simple, and would mean that all the flows that are adaptive should back off. However it is inefficient, and possibly unsafe, since all the backed-off flows will start up again in a synchronized fashion, unlike random drop.
- **Intelligent drop.** Various fair drop mechanisms have been proposed, sometimes based on level 4 (transport-specific) information such as port numbers. These may need a lot of state information, although it should be possible to make them fairer.

The reaction to drop packets is well defined for non-real time applications using TCP. Packet drop is to be interpreted as congestion that leads to a slow down in transmission rate, as described in Chapter 7 (“Slow Start and Congestion Avoidance”). This leads to a happy network.
