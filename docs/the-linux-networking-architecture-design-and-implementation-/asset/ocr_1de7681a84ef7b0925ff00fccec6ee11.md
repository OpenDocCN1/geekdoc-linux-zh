# Entries in the /proc/sys/net/core Directory

rmem_default: Default value for the memory space used for incoming socket buffers (in bytes).
rmem_max: Maximum size for incoming socket buffers (in bytes).
wmem_max: Maximum size for outgoing socket buffers (in bytes).
message_burst: Parameters limiting the number of warning or log messages created by the network implementation (number of messages per second). This is necessary to limit the consequences of denial-of-service attacks.

Entries in /proc/sys/net/ipv4/ This directory holds the most important information and configuration options for the TCP/IP protocols. Specifically, if a 1 is written to the file, a specific functionality is enabled; if a 0 is written to the file, this functionality is disabled.

icmp_echo_ignore_all or icmp_echo_ignore_broadcasts.respectively, suppresses replies to all icmp requests to the host or to multicast broadcast addresses.
icmp_... can be used to specify, for various ICMP message types, how often at most an ICMP packet may be sent. This value is set in packets per second.
icmp_autoconfig shows whether the computer should be configured automatically (e.g., by RARP, BOOT, DHCP, or similar mechanisms).
ip_dynaddr specifies whether IP addresses may be dynamically allocated.
ip_forward enables or disables packet forwarding: 1 means that packets will be forwarded and that the computer behaves like a router; 0 means that the computer behaves like a host. “Toggling” this switch sets the default parameters specified in RFC 1122 (for hosts) and RFC 1812 (for routers).
ip_default_ttl handles the default value for the Time-To-Live (TTL) field in the IP packet header. This parameter normally is initialized to 64.
icmp_mask debug enables or disables debugging messages in masquerading.
ip_no_pmtu_disc disables the path MTU discovery mechanism.
ipfrag_high_thresh specifies the maximum memory used for IP packet fragmenting. If this threshold value is exceeded, the kernel starts dropping fragments until the bottom threshold value, ipfrag_low_thresh, is reached. (See Chapter 14.)
ipfrag_low_thresh—see ipfrag_high_thresh.
ipfrag_time is the interval (in seconds) an IP fragment is held in memory. If the rest of the fragmented packet does not arrive by the time it expires, then the fragment is dropped.

The following parameters concern the TCP transport protocol only:

tcp_syn_retries: Number of attempts to establish a TCP connection (sending the initial SYNs). This value should not be greater than 255.
tcp_keepalive_time specifies how long keepalive packets are sent, if keepalive is active.