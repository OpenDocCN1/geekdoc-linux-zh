
- `linger` is nonzero, a socket-close waits for the data to transmit or times out. (`struct linger`, disabled by default.)

- `SO_OOBINLINE` You can send very short messages that the receiver does not place in the data queue. Instead, it accepts the message separately (out of band), so you can use it for transmitting urgent messages. This flag forces the out-of-band data into the data queue where your socket could read it normally.

- `SO_PASSCRED` Enable/disable passing of user identification (see `SO_PEERCRED`). (Boolean, disabled by default.)

- `SO_PEERCRED` Set peer credentials (user ID, group ID, and process ID). (`struct ucred`, zero by default.)

- `SO_RCVBUF` You can use this option to resize the input buffers. For TCP you should set this to 3 or 4 times the size of MSS (Maximum Segment Size, see `TCP_MAXSEG` below). UDP does not have flow control, however, and you lose any messages that exceed the receive-buffer's size. (Integer, 65,535 bytes by default.)

- `SO_RCVLOWAT` Like `SO_SNDLOWAT`, this works with I/O multiplexing system calls and signal-based I/O. As soon as the socket receives the indicated number of bytes, the socket notifies your program. On Linux this option is read-only. (Integer, 1 byte by default.)

- `SO_RCVTIMEO` Like `SO_SNDTIMEO`, this places a limit on the amount of time waiting for input. If the reading call (`read()`, `readv()`, `recv()`, `recvfrom()`, or `recvmsg()`) exceeds the time without getting any data, the read returns with an error. (`struct timeval`, 1 byte by default, get only.)

- `SO_REUSEADDR` Using this option, you can create two sockets that share the address:port connection. You can share a port with different sockets in the same process, different processes, or different programs. Most of the time this is useful when your server crashes and you need to restart it quickly. The kernel typically reserves a port for several seconds after the termination of the owner. If you get a `Port Already Used` error in the `bind()`, use this option to get around it. (Boolean, disabled by default.)

- `SO_SNDBUF` This option lets you define the size of the output socket data buffer. (Integer.)

- `SO_SNDLOWAT` This is the low water mark for transmitting information. The I/O multiplexing system calls report that a socket is writable when you can write that many bytes to the socket. If you are using signal-based I/O, you get a signal upon reaching the low water mark. On Linux this option is read-only. (Integer, 1 byte by default.)

- `SO_SNDTIMEO` This option allows you to set a timeout on all your write calls (`write()`, `writev()`, `send()`, `sendto()`, and `sendmsg()`). If one of these calls in your program takes too long, it aborts with an error. (`struct timeval`, 1 byte by default, get only.)

- `SO_TYPE` This option returns the socket type. This number matches the second parameter in the `socket()` system call. (Integer, no default, get only.)

## IP-Specific Socket Options

The IP-specific socket options apply mostly to datagrams and managing lower-level details. To use these options, you must set the `level` parameter in `getsockopt()` and `setsockopt()` to `SOL_IP`.

- `IP_ADD_MEMBERSHIP` Join a multicast membership. (`struct ip_mreq`, no default, write-only.)

- `IP_DROP_MEMBERSHIP` Drop multicast membership. (`struct ip_mreq`, no default, write-only.)

- `IP_HDRINCL` This option allows you to build the raw IP packet header information. The only field you don't fill is the checksum. This option is for raw packets only. (Boolean, disabled by default.)

- `IP_MTU_DISCOVER` Lets you open the MTU (maximum transmission unit) discovery process. The MTU is the agreement between the sender and receiver on how large the packet should be. This has three values:
  - `IP_PMTUDISC_DONT` (0) Never send DF (don't fragment) frames.
  - `IP_PMTUDISC_WANT` (1) Use per-route hints.
  - `IP_PMTUDISC_DO` (2) Always use DF frames. (Integer, disabled by default.)

- `IP_MULTICAST_IP` Sets the outgoing multicast interface. This is the IPv4 address assigned to a hardware interface. Most machines have only one interface and one address, while some may have more. This setting lets you indicate which address interface to use. (`struct in_addr`, `INADDR_ANY` by default.)

- `IP_MULTICAST_LOOP` Enables multicast loopback. Your receive buffer gets a copy of whatever you transmit. (Boolean, disabled by default.)

- `IP_MULTICAST_TTL` Sets the maximum number of hops (Time To Live) the multicast message is allowed. For any effective Internet multicasting, you must set this value, because it allows only one routing by default. (Integer-byte, 1 by default.)

- `IP_OPTIONS` Lets you select specific IP options. The options are notes in the IP header that tell the receiver specific notes (for example, timestamping, security levels, and alerts). Look at the TCPv1 and TCPv2 RFCs for more information. (Byte array, none by default.)

- `IP_TOS` This option lets you determine the type of service (TOS) that the outgoing packets require. You can select from four types: `IPTOS_LOWDELAY` (minimize delay), `IPTOS_THROUGHPUT` (maximize throughput), `IPTOS_RELIABILITY` (maximize reliability), and `IPTOS_LOWCOST` (minimize cost). (Integer, no extra services by default.)

- `IP_TTL` Set the time to live (TTL) of each packet. This indicates the maximum number of router hops before the packet expires. (Integer-byte, 64 by default.)

## IPv6-Specific Socket Options

The IPv6-specific socket options apply to extended features of IPv6 or IPng. To use these options, you must set the level parameter in `getsockopt()` and `setsockopt()` to `SOL_IPV6`.

- `IPV6_ADD_MEMBERSHIP` Like the IPv4 version, this option lets you join an IPv6 multicast group. (`struct ipv6_mreq`, none by default, write-only.)

- `IPV6_ADDRFORM` This option allows you to convert the socket between IPv4 and IPv6. (Boolean, disabled by default.)

- `IPV6_CHECKSUM` When working with raw IPv6 sockets, this option lets you tell the socket the byte offset to the checksum in the packet. If the value is -1, the kernel does not calculate the checksum for you, and the receiver skips it as well. (Integer, -1 by default.)

- `IPV6_DROP_MEMBERSHIP` Like the IPv4 version, this option lets you unsubscribe from an IPv6 group. (`struct ipv6_mreq`, none by default, write-only.)

- `IPV6_DSTOPTS` This setting allows you to retrieve all options from a received packet. This information appears in the `recvmsg()` system call. (Boolean, disabled by default.)

- `IPV6_HOPLIMIT` If you use the `recvmsg()` system call and have enabled this option, you can get the number of hops remaining in a received packet in the ancillary data field. (Boolean, disabled by default.)

- `IPV6_HOPOPTS` If you use the `recvmsg()` system call and have enabled this option, you can get the hop-by-hop options in the ancillary data field. (Boolean, disabled by default.)

- `IPV6_MULTICAST_HOPS` Similar to the IPv4 version (TTL), this option lets you define the maximum number of router hops before expiring. (Integer-byte, 1 by default.)

- `IPV6_MULTICAST_IF` Similar to the IPv4 version, this option lets you define which interface (by IP address) to use for multicasting messages. (`struct in6_addr`, zero by default.)

- `IPV6_MULTICAST_LOOP` Like the IPv4 version, this option echoes every message you send on multicast. (Boolean, disabled by default.)

- `IPV6_NEIGHOP` This option lets you specify the next hop for a datagram when you use `sendmsg()`. You need to have `root` access to perform this operation. (Boolean, disabled by default.)

- `IPV6_PKTHINFO` Normally you can't get very much information about the received packet. This option lets you get the arriving interface index and destination IPv6 address. (Boolean, disabled by default.)

- `IPV6_PKTOPTIONS` Similar to the IPv4's `IP_OPTIONS`, you can directly specify the options using a byte array. In most cases you send IPv6 options via the ancillary data of the `sendmsg()` system call. (Byte array, none by default.)

- `IPV6_UNICAST_HOPS` Similar to the IPv4's `IP_TTL`, this option lets you specify the maximum number of router hops before expiring the packet. (Integer-byte, 64 by default.)

## TCP-Specific Socket Options

The TCP-specific socket options apply to the streaming capabilities of the TCP layer. To use these options, you must set the `level` parameter in `getsockopt()` and `setsockopt()` to `SOL_TCP`.

- `TCP_KEEPALIVE` The `SO_KEEPALIVE` waits for 2 hours before checking for a connection. This option lets you change that delay. The value's units are in seconds. On Linux the `sysctl()` call replaced this option. (Integer, 7200 by default.)

- `TCP_MAXRT` This option lets you specify the retransmit time in seconds. A `0` selects the kernel default, and a `-1` forces the network subsystem to retransmit forever. (Integer, 0 by default.)

- `TCP_MAXSEG` The TCP stream is packetized into chunks of data. The Maximum Segment Size (MSS) specifies the amount of data in each chunk. The network subsystem coordinates this value with the peer's MSS. You cannot increase this value over the peer's MSS, but you can decrease it. (Integer, 540 bytes by default.)

- `TCP_NODELAY` TCP uses the Nagle Algorithm, which forbids sending any message that is smaller than the MSS until the receiver acknowledges (ACK) all outstanding messages. If you enable this option, you turn off the Nagle Algorithm, making it possible to send several short messages before getting the ACKs. (Boolean, disabled by default.)

- `TCP_STDURG` This option specifies where in the stream to find the `OOB` data byte. By default it is the byte following the `OOB` flag. Since all implementations recognize this default, you may never need to use this option. Linux replaced this option with the `sysctl()` system call. (Integer, 1 by default.)

## Recovering the Socket Descriptor

You may write many servers as you learn how to do network programming. You may run into a problem that the `bind()` fails because of an `address in use` error. This is the most common error programmers get (even experienced ones) and one of the most common questions asked on the Usenet. The problem comes from the way the kernel allocates the ports.
