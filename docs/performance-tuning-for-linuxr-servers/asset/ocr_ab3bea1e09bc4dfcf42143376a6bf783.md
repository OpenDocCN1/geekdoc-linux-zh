This is the maximum accept queue backlog that can be specified via the listen() system call, or the number of pending connection requests. When the number of queued incoming connection requests reaches this value, further connection requests are dropped. Increasing this value allows a busy server to specify a larger backlog of requests. The default maximum is 128.

# optmem_max

optmem_max ( /proc/sys/net/core/optmem_max )

This variable is the maximum initialization size of socket buffers, expressed in bytes.