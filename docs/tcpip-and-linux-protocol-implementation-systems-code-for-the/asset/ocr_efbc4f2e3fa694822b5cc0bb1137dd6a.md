paths are not known by the end user in advance, and are subject to change by dynamic routing. The influence of other traffic and varying traffic patterns, including localized traffic and time-of-day effects, means deterministic delay is often impractical, but not impossible.

**Delay variation and end-to-end jitter.** Variation in delay is the per-packet delay change. It can be contributed to effects at the receiver, such as packet arrival rate and variable data rate for flow. For non-real-time applications, this does not represent a problem. For real-time applications, a receiving application may need jitter compensation.

Causes of jitter include media access (LAN and modem access delays for asymmetric codec lines) and FIFO queuing, where there is no notion of a flow. For traffic aggregation, a mix of different applications, the variation in load on routers due to localized load/congestion, and dynamic path changes can lead to jitter.

**Loss.** End-to-end loss can be compensated for by non-real-time retransmission, for example, TCP. For real-time applications, it is possible to mask loss by using forward error correction and redundant encoding. This can also be achieved via media-specific fill-in at the receiver. If packet loss persists, this often be taken as an indication of congestion. Many newer real-time applications are adaptive: they adjust flow construction and the resulting output rate according to a *TCP-equivalent* formula, so that they look to a network provider like a smoothly varying TCP source.

Causes of loss include packet drop at routers due to short-, medium-, or long-term congestion, or traffic contract violations caused by misbehaving sources. More systemic, but lesser sinister, causes of problems can be source synchronization, excessive load due to failure in another part of the network, or simply abnormal traffic patterns, for example, new downloads.

Note that packet reordering, due to misbehavior of a load balancing scheme, misconfiguration of routers, or odd interactions between retransmission and rerouting, may be seen as loss by some receivers.

**Throughput.** Throughput is often referred to as bandwidth—wrongly, but we're stuck with that.

The end-to-end data rate is subject to short-term changes, during the life-time of a flow over, seconds (on the order of round-trip times), as well as long-term changes during the course of a day on the order of hours. This is partly a result of protocol behavior such as TCP congestion control and flow control, partly because of human reactions to perceived performance, and partly because of the normal daily patterns of life and Internet usage.