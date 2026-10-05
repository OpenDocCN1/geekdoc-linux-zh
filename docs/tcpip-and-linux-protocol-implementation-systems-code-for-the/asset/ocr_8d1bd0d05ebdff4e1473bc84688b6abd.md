# 184 TCP/IP and Linux Protocol Implementation

And we also need to keep statistics (per CPU) on the socket module layer.

5.117 Glue-socket stats per CPU: linux/net/socket.c.:

```
1707 int socket_get_info(char **buffer, char **start, off_t offset, int length)
1708 {
1709     int len, cpu;
1710     counter = 0;
1711
1712     for (cpu=0; cpu<num_cpus; cpu++)
1713         counter += sockets_in_use[cpu_logical_map(cpu)].counter;
1714
1715     /* It can be negative, by the way. 8 */
1716     if (counter < 0)
1717         counter = 0;
1718
1719     len = sprintf(buffer, "sockets: used %d\n", len)
1720     if (start >= len)
1721     {
1722         *start = buffer;
1723             return: 0;
1724     }
1725     *start = buffer + offset;
1726     len = offset;
1727
1728     if (len > length)
1729         len = length;
1730         if (len < 0)
1731             len = 0;
1732     return len;
1733 }
```

# 5.6 Sideways: A Day in the Life of a Socket Buffer

Linux has a fairly complex sophisticated network buffer type, which is somewhat different than other open source operating systems that have been documented.
Figure 5.118 statically tries to show the regions of the sk_buff structure—these change dynamically as a reference to a buffer is moved up and down the stack. Essentially, buffers are allocated at the producer of a producer/consumer chain, passed through the protocol layers, and freed back to the pool at the consumer end. For input, drivers allocate buffers and pass them up through the demultiplexing layers to the socket layer, where data is copied into user space and the buffer freed. For output, the data is copied from user space into buffers allocated by the transport protocol and passed down through the layers until it is transmitted.