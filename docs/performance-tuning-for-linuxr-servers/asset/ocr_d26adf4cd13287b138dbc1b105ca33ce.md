# # Core Kernel Parameter Descriptions

This section describes kernel socket buffers and covers some of the more useful core kernel parameters. Adjusting the size of the kernel socket buffers is perhaps the single most effective method for improving performance, and most of the core parameters described in this section manipulate them in some fashion.

# ## An Introduction to Socket Buffers

Applications use the `socket()` system call to create a communication endpoint. Each socket has associated with it a read and write buffer (also known as the receive and send buffers, respectively).

The receive socket buffer holds the data that has been sent to this socket by a remote host. This data is retrieved by the application upon doing a `read()` system call (or a variant such as `recvfrom()`). If this buffer is full, any further incoming data received for this socket is dropped.

The write socket buffer holds the data written to the socket by the application before it is sent to the remote host. If there is insufficient room in the buffer, the application’s `write()` system call (or a variant such as `sendto()`) blocks until the kernel makes room for all the data. If the application has chosen not to block, the kernel returns an error to the application indicating that it cannot absorb that quantity of data at this time, and to retry the write.

# ### Default Socket Buffer Size

```
`net.core.wmem_default (/proc/sys/net/core/wmem_default)`
`net.core.rmem_default (/proc/sys/net/core/rmem_default)`
```

These two parameters are the global default size of the read and write socket buffers, respectively, associated with each socket. They are used to initialize the size of all types of sockets. In the case of TCP sockets, these values are later overwritten by the TCP protocol-specific defaults for the read and write buffer sizes (tcp_rmem and tcp_wmem, described in the forthcoming TCP/IPv4 protocol kernel parameters list).

Individual applications can adjust the size of the socket buffers by performing a `setsockopt()` call with a level of `SOCKET` and the options `SO_SNDBUF` and `SO_RCVBUF` for the send and receive buffers, respectively.

Systems experiencing heavy network loads benefit from increasing these variables. The kernel adjusts the initial value of these parameters at bootup based on the available memory in the system, as shown in Table 12-1.