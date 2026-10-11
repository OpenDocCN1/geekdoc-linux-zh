| Parameter | Description |
|---|---|
| tcp_stdurg | Enables strict RFC793 interpretation of the<br>TCP urgent pointer field |
| tcp_fin_timeout | Time in seconds it takes to receive a final<br>FIN before the socket closes |
| tcp_tw_reuse | Reuse of timewait sockets |
| tcp_max_orphans | Maximum number of orphaned connections |
| tcp_max_tw_buckets | Maximum number of timewait sockets |
| tcp_window_scaling | Enables window scaling as defined in<br>RFC1323 |
| tcp_timestamps | Enables timestamps as defined in RFC1323 |
| tcp_rmem | Receive buffers for TCP socket |
| tcp_wmem | Send buffers for TCP socket |
| tcp_mem | Memory pages for TCP usage |

The `tcp_wmem` parameter has three fields. The first field, $min$, specifies the amount of memory reserved for send buffers for a TCP socket. The second field is the default amount of memory allowed for send buffers for a TCP socket. The last field, $max$, is the maximum amount of memory allowed for automatically selected send buffers for a TCP socket.

The `tcp_rmem` parameter has three fields. The first field, $min$, is the minimum size of receive buffer used by TCP sockets. The second is the default amount of memory allowed for receive buffers used by TCP sockets. The last field, $max$, is the maximum size of the receive buffer allowed for automatically selected receive buffers for TCP sockets.