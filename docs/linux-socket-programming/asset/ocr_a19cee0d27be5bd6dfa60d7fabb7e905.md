+   * `linger` is nonzero, a socket-close waits for the data to transmit or times out. (`struct linger`, disabled by default.)

+   * `SO_OOBINLINE` You can send very short messages that the receiver does not place in the data queue. Instead, it accepts the message separately (out of band), so you can use it for transmitting urgent messages. This flag forces the out-of-band data into the data queue where your socket could read it normally.

+   * `SO_PASSCRED` Enable/disable passing of user identification (see `SO_PEERCRED`). (Boolean, disabled by default.)

+   * `SO_PEERCRED` Set peer credentials (user ID, group ID, and process ID). (`struct ucred`, zero by default.)

+   * `SO_RCVBUF` You can use this option to resize the input buffers. For TCP you should set this to 3 or 4 times the size of MSS (Maximum Segment Size, see `TCP_MAXSEG` below). UDP does not have flow control, however, and you lose any messages that exceed the receive-buffer's size. (Integer, 65,535 bytes by default.)

+   * `SO_RCVLOWAT` Like `SO_SNDLOWAT`, this works with I/O multiplexing system calls and signal-based I/O. As soon as the socket receives the indicated number of bytes, the socket notifies your program. On Linux this option is read-only. (Integer, 1 byte by default.)

+   * `SO_RCVTIMEO` Like `SO_SNDTIMEO`, this places a limit on the amount of time waiting for input. If the reading call (`read()`, `readv()`, `recv()`, `recvfrom()`, or `recvmsg()`) exceeds the time without getting any data, the read returns with an error. (`struct timeval`, 1 byte by default, get only.)

+   * `SO_REUSEADDR` Using this option, you can create two sockets that share the address:port connection. You can share a port with different sockets in the same process, different processes, or different programs. Most of the time this is useful when your server crashes and you need to restart it quickly. The kernel typically reserves a port for several seconds after the termination of the owner. If you get a `Port Already Used` error in the `bind()`, use this option to get around it. (Boolean, disabled by default.)

+   * `SO_SNDBUF` This option lets you define the size of the output socket data buffer. (Integer.)

+   * `SO_SNDLOWAT` This is the low water mark for transmitting information. The I/O multiplexing system calls report that a socket is writable when you can write that many bytes to the socket. If you are using signal-based I/O, you get a signal upon reaching the low water mark. On Linux this option is read-only. (Integer, 1 byte by default.)

+   * `SO_SNDTIMEO` This option allows you to set a timeout on all your write calls (`write()`, `writev()`, `send()`, `sendto()`, and `sendmsg()`). If one of these calls in your program takes too long, it aborts with an error. (`struct timeval`, 1 byte by default, get only.)

+   * `SO_TYPE` This option returns the socket type. This number matches the second parameter in the `socket()` system call. (Integer, no default, get only.)

# ## IP-Specific Socket Options

The IP-specific socket options apply mostly to datagrams and managing lower-level details. To use these options, you must set the `level` parameter in `getsockopt()` and `setsockopt()` to `SOL_IP`.

+   * `IP_ADD_MEMBERSHIP` Join a multicast membership. (`struct ip_mreq`, no default, write-only.)

+   * `IP_DROP_MEMBERSHIP` Drop multicast membership. (`struct ip_mreq`, no default, write-only.)

+   * `IP_HDRINCL` This option allows you to build the raw IP packet header information. The only field you don't fill is the checksum. This option is for raw packets only. (Boolean, disabled by default.)