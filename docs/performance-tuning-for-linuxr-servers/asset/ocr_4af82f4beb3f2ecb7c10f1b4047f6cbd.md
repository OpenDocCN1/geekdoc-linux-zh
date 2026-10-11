| Intel e1000 Driver Baseline Throughput in Mbps | Intel e1000 Driver with NAPI Support Throughput in Mbps |
| :--- | :--- |
| 955.7 | 955.7 |

Table 21-4. Packet Forwarding (Routing) with and Without NAPI

| Intel e1000 Driver Baseline Throughput in Packets Forwarded | Intel e1000 Driver with NAPI Support Throughput in Packets Forwarded |
| :--- | :--- |
| 305 | 298580 |

The Receive Interrupt Delay (RxIntDelay) was set to 1 in the case of NAPI because RxIntDelay=0 caused a problem, and RxIntDelay was set to 64 in the case of base e1000 driver without NAPI support. The receive and transmit descriptors were set to 256 on both systems for the e1000 driver. For the TCP Stream test, the TCP socket size was set to 131070. The test duration for both the TCP Stream and the UDP Stream was 30 seconds. One million packets at 970 kpackets per second were injected into the packet-forwarding experiments.

The packet-forwarding results in Table 21-4 clearly show that NAPI is a winner for routing packets. TCP and UDP stream tests using Netperf, as shown in Tables 21-2 and 21-3, indicate that NAPI does not improve network throughput. In fact, network throughput caused performance to moderately regress.

The results of TCP stream, UDP stream, and packet forwarding in Tables 21-2, 21-3, and 21-4 show that NAPI helped improve performance significantly in routing tests. Because NAPI is optionally available in many network drivers, you can choose to use NAPI depending on your environment.

# ## TCP Offload Engine Support

Server applications that do not use some of the unique features of the Linux TCP/IP protocol, such as IP filtering or quality of service (QoS), can instead use network