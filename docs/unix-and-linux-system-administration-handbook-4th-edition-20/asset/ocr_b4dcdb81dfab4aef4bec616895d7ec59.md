# Chapter 14 TCP/IP Networking

To lock this interface to 100 Mb/s full duplex, the command

```
ubuntu# ettool -s eth speed 100 duplex flex
```

If you are trying to determine whether autonegotiation is reliable in your environ-
y, you may also use ettool -r helpful. It forces the parameters of the link to
be renegotiated immediately.

Another useful option is -k, which shows protocol-related tasks have been
assigned to the network interface rather than being performed by the kernel. Most
interfaces can calculate checksums, and some can assist with segmentation as
well. Unless you have reason to think that a network interface is not doing these
tasks reliably, it is always better to offload them. If you use ettool -k in comb-\ination with various subsets to force or disable specific types of offloading.
(-The k option shows current values and the -K option sets them).

Any changes you make with ettool are transient. If you want them to be en-
forced consistently, you'll have to make sure that ettool gets run as part of the per-interface configur-\s network configuration. It is best to do this if you adjust have some ettool commands run at boot,
your configuration will not properly cover cases in which the interfaces are re-
started without a reboot of the system.

![](bbox=[0.18, 0.495, 0.23, 0.535])

On Red Hat systems, you can include ETHOOL_OPTS= line in the configura-
tion for the interface underneath /etc/sysconfig/network-scripts. ifup passes
the line as arguments to ettool.

![](bbox=[0.18, 0.545, 0.23, 0.585])

SUSE provision for provisioning Red Hat, but the de-facto option is
called ETHOOL_OPTIONS and the per-interface configuration files are kept in
/etc/sysconfig/network.

![](bbox=[0.18, 0.605, 0.23, 0.645])

In Ubuntu, you can run the ettool commands from a post-up script secured in
the interface's configuration in /etc/network/interfaces.

# Linux TCP/IP options

Linux puts a representation of each tunable kernel variable into the /proc
filesystem. The networking variables are in /proc/sys/net/ipv4. Here's a trimmed
list of some the most interesting ones for interaction:

```
ubuntu$ cd /proc/sys/net/ipv4; ls -F
```

| conf/ | tcp_congestion_control | tcp_metrics_save |
| icmp_echo_ignore_all | tcp_dma_copyback | tcp_orphan_retries |
| icmp_echo_ignore_broadcasts | tcp_sack | tcp_reordering |
| | tcp_ecn | tcp_retrans_collapse |
| icmp_ratelimit | tcp_fact | tcp_retries1 |
| icmp_ratemask | tcp_fin_timeout | tcp_retries2 |
| igmp_max_memberships | tcp_frto | tcp_rfc1337 |
| igmp_max_msf | tcp_frto_response | tcp_rmem |
| inet_peer_gc_maxime | tcp_keepalive_intvl | tcp_sack |
| inet_peer_gc_mintime | tcp_keepalive_probes | tcp_sturdg |