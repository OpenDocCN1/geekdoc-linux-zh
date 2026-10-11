any given time.

Therefore, memory allocation failures while opening sockets can occur even though the system still has available memory.

For systems that need to support busy workloads, increasing the tcp_mem() parameter benefits performance. For example, here are some values that it can be set to for a large networking workload:

```
net.ipv4.tcp_mem = 1000000 1001024 1002048
```

This change should be made with caution, because it comes with a trade-off.

A large amount of memory is consumed by each socket buffer, and this limits the amount of memory available for other activity in the system.

# # TCP Options

The following sections describe the TCP options most likely to be of use to the system administrator.

# ## tcp_window_scaling

net.ipv4.tcp_window_scaling (*/proc/sys/net/ipv4/tcp_window_scaling*)

This kernel variable enables the TCP window scaling feature. It is on by default. Window scaling implements RFC1379.

The window scale option is required for the employment of TCP window sizes larger than 64K. Because the length field in the TCP protocol header for the advertised receive buffer is specified by 16 bits, the window size cannot be larger than 64K.

Window scaling allows buffers larger than 64K to be advertised, thereby enabling the sender to fill network pipes whose bandwidth latency is larger than 64K. Particularly for connections over satellite links and on networks with large round-trip times, employing large windows (greater than 64K) results in a significant improvement in performance.

Optimum throughput is achieved by maintaining a window at least as large as the bandwidth-delay product of the network. If that quantity is larger than 64K, window scaling can potentially provide improved throughput, with a trade-off between the overhead of creating and processing the TCP option and the much larger amount of data that can be sent in transit without delay.

It should be noted that socket buffers larger than 64K are still potentially beneficial even when window scaling is turned off.

Although the kernel does not advertise or allow windows larger than that limit, having a larger buffer enables the kernel to absorb a greater amount of data from the application one write() call at a time, and hence return earlier.