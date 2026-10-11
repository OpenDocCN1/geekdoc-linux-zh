| Parameter | Description |
|---|---|
| `wmem_default` | Socket send buffer size |
| `rmem_max` | Maximum receive socket buffer size |
| `wmem_max` | Maximum send socket buffer size |

The `message_cost` and `message_burst` parameters are used to limit the warning messages written to the kernel log. The default setting limits warning messages to one every 5 seconds. The higher the `error_cost` is, the fewer messages are written. The `error_burst` parameter controls when messages are dropped.

# ICMP

**Sysctl Prefix:** net.ipv4

*/proc Prefix:* /proc/sys/net/ipv4

| Parameter | Description |
|---|---|
| `icmp_ratemask` | Mask value for ICMP types |
| `icmp_ratemlim` | Rate for sending ICMP packets |
| `icmp_ignore_bogus_error_responses` | Warning messages from router |
| `icmp_echo_ignore_broodcasts` | ICMP echo requests to broadcast addresses |
| `icmp_echo_ignore_all` | ICMP echo requests |
| `igmp_max_membership` | Maximum number of multicast groups |