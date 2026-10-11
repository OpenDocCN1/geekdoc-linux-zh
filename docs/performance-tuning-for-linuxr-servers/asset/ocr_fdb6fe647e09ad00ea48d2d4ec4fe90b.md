| Parameter | Description |
| :--- | :--- |
| `error_burst` | Time before logging a warning message |
| `error_cost` | Cost factor for logging a warning message |
| `max_size` | Maximum size of routing cache |
| `max_delay` | Maximum delay in seconds for flushing routing cache |
| `min_delay` | Minimum delay in seconds for flushing routing cache |

The `error_cost` and `error_burst` parameters limit the warning messages written to the kernel log. The default setting limits warning messages to one every 5 seconds. The higher `error_cost` is, the fewer messages are written. The `error_burst` parameter controls when messages are dropped.

# ## TCP

**Sysctl Prefix:** net.ipv4

**/proc Prefix:** /proc/sys/net/ipv4/

| Parameter | Description |
| :--- | :--- |
| `tcp_app_win` | Maximum window for application buffer |
| `tcp_reordering` | Maximum reordering of packets in a TCP stream |
| `tcp_max_syn_backlog` | Length of per-socket backlog queue |
| `tcp_rfc1337` | Sets TCP stack confirming to RFC1337 |