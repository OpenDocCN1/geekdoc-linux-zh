The `tcp_keepalive_probes` parameter is the number of times the probes are sent before killing the nonresponding connections.

The `tcp_syn_retries` parameter is the number of times initial SYNs for a TCP connection are transmitted. This timeout is for outgoing connections. For incoming connections, the number of retransmits is defined by the `tcp_retries1` parameter.

# ## IP Fragmentation

**Sysctl Prefix:** net.ipv4

**/proc Prefix:** /proc/sys/net/ipv4

| Parameter | Description |
|---|---|
| `ip_nonlocal_bind` | Binds to nonlocal IP address |
| `ip_no_pmtu_disc` | Disables MTU path discovery |
| `ip_autoconfig` | How host got IP configuration |
| `ip_default_ttl` | Maximum number of hops a packet may travel |
| `ip_forward` | Forward packets between interfaces |
| `ipfrag_time` | Time in seconds to keep IP fragment in memory |
| `ip_dynaddr` | Enables dynamic socket address rewriting on interface address change |
| `ipfrag_low_thresh` | Low-memory watermark for fragment handler |
| `ipfrag_high_thresh` | Maximum amount of memory used to reassemble IP fragments |
| `ip_local_port_range` | Range of ports used by TCP and UDP to choose the local port |