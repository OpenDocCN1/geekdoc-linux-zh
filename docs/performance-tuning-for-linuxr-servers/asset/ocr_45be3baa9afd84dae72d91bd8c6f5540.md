# TCP/IPv4 Protocol Kernel Parameters

This section covers some of the more useful IPv4 parameters. The IPv4 category includes the protocol-specific parameters. We pay particular attention here to the TCP protocol parameters. When a socket is created, the protocol and address families are specified. For a TCP socket, the address family is AF_INET and the type is SOCK_STREAM. For a UDP protocol socket, the address family is AF_INET but the type is SOCK_DGRAM. TCP socket buffer sizes are controlled by their own parameters rather than the core kernel buffer size parameters.

# TCP Buffer and Memory Management

# tcp_rmem

```
net.ipv4.tcp_rmem (/proc/sys/net/ipv4/tcp_rmem)
```

This variable is an array of three integers:

+   - net.ipv4.tcp_rmem[0] = minimum size of the read buffer
+   - net.ipv4.tcp_rmem[1] = default size of the read buffer
+   - net.ipv4.tcp_rmem[2] = maximum size of the read buffer

When a socket is created, the initial size of the read buffer, in bytes, is controlled by the core default socket size. If it is a TCP protocol socket, however (type = AF_INET SOCK_STREAM), the read buffer size is set to the TCP protocol-specific default, which is the second integer of this array. To increase the initial size of the TCP read buffer, this is the variable to increase. Note that the maximum value this can take is still limited by the core socket maximum size, so this value cannot be greater than net.core.rmem_max.

The minimum and maximum TCP read buffer size limits (the first and the third integers in the tcp_rmem array) are used by the kernel while dynamically tuning the size of the buffer. The default values of this parameter are shown in Table 12-2.

| Buffer Parameters | Minimum | Default | Maximum |
| --- | --- | --- | --- |
| net.ipv4.tcp_rmem[0] | net.ipv4.tcp_rmem[1] | net.ipv4.tcp_rmem[2] | | | |
| Low Memory | PAGE_SIZE | 43689 | 43689*2 |