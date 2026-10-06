
## B.3 Information in the /proc Directory

tcp_keepalive_probes: Number of KeepAlive probes sent by TCP before the connection is declared to have failed.

tcp_retries1: Number of acknowledgments for a packet before it is given up.

tcp_retries2: Maximum number of attempts to send a packet.

tcp_fin_timeout: The wait time for the acknowledgement of a connection-teardown before the connection is aborted.

tcp_max_syn_backlog: Number of TCP connection-establishment requests to be buffered for a socket.

tcp_window_scaling enables or disables the scaling of TCP windows (as specified in RFC 1323).

tcp_timestamps enables or disables the TCP timestamp (as specified in RFC 1323).

tcp_sack: Switch for select acknowledgments (TCP ACK).

tcp_sturg: Eners urgent priority data, as specified in RFC 793.

tcp_retrans_collapse: Several TCP stacks in printers are faulty. You can activate this option to work around this problem.

ip_local_port_range specifies the range for local ports of the TCP and UDP protocols. The first number specifies the beginning of the interval, the second number specifies the end.

/proc/sys/net/ipv4/conf directory is subdivided: let's look at the conf subdirectory. It contains, turn subdirectories: one for each registered network device, and one named all. All of these directories include the same entries, which are introduced here:

- * accept_redirects shows whether ICMP redirects are accepted. This option is disabled by default in routers, but disabled in end systems.
- * accept_source-route enables or disables accepting of source-route packets. This option normally is enabled in routers, but disabled in end systems.
- * forwarding enables or disables the forwarding of packets on this network device.
- * log_martians enables or disables the logging of "impossible" addresses (including Class-E addresses in IP).
- * mc_forwarding enables or disables multicast routing. If activated, the CONFIG_ROUTE option should additionally be compiled for the kernel, and a multicast routing daemon should be installed.
- * proxy_arp: Support for an ARP proxy.
- * rp_filter enables or disables the option that ICMP redirect messages are accepted only by routers in the default gateways list.

/proc/sys/net/ipv4/route

error_burst, error_cost: These parameters are used to limit the log messages of the routing code in the kernel. The larger that error_cost, the earlier that log messages will be created, error_burst limits the rejection of warning messages.

## Appendix B Debugging the Linux Kernel

ush: Accessing this file causes the routing cache to be deleted.
gc_elastic, gc_interval, gc_min_interval, gc_thresh, gc_timeout:
These parameters control the automatic garbage collection of the routing table (i.e., how soon and how strictly entries will be removed from the table).

max_size specifies the size of the routing cache. Older entries are removed as soon as this is reached.

max_delay, min_delay: Numbers for deleting the entire cache.
redirect_load, redirect_number: These factors specify how many ICMP packets may be sent. No more redirects are sent as redirect_load or redirect_number is exceeded.

redirect_silence is the timeout value for redirect packets. Once this expires, redirect packets that have not yet been acknowledged are retransmitted. This process runs when redirects are disabled redirect_load or redirect_number was exceeded.

max_size: Maximum number of entries in the routing cache. If this is exceeded, the least-used entries are overwritten.

/proc/sys/net/ipv4/neigh/[net_dev] The following parameters define the immediate network neighbors; they are located in /proc/sys/net/ipv4/neigh/[net_dev] directory of the respective network device:

- * base_reachable_time: A value used to compute the random reachable time. (See RFC 2461).
- * retrans_time: The time between two consecutive neighbor solicitation packets used for address resolution and for checking the reachability of a local computer. This time is specified in ticks.
- * q_len: Specifies the maximum queue length for (higher-layer) packets waiting for a specific address. (See Chapter 15).
- * ucast_solicit: Maximum number of packets sent to resolve a unicast address.
mcast_solicit: Maximum number of attempts to resolve a multicast address.
delay_first_probe_time: Wait time, after the expiry of a valid neighbor is entered again. (See gc_stale_time).
- * locktime: An entry in an ARP/neighbor table will be replaced by a new one once the old entry locks ticks.
- * proxy_delay: The maximum wait time for the reply to an ARP request, which has an entry in the ARP proxy.
- * proxy_len: Maximum length of the queue for a delayed ARP proxy timer.
- * arp_solicit: Specifies the number of requests sent to the ARP daemon on, user level.
- * gc_stale_time: Specifies the intervals in which the ARP table is checked for entries (state = NUD_STALE). If an entry is in the NUD_STALE state, then an initial attempt is made to check it (by a unicast packet). If this attempt fails, and if mcast_solicit > 0, a broadcast ARP request is used to find the compute.

## USING A DEBUGGER WITH THE LINUX KERNEL

A debugger is a tool that allows you to stop a program during execution and execute it step by step to monitor the program state—the values of variables and the contents of memory locations—and modify it, if necessary. A debugger can also be used for development in the kernel. However, stopping the kernel would immediately cause the entire system to become unusable. Debuggers normally offer a way to check the program state when the happened.

Interface Between Kernel and Debugger

The core file, as interface between the debugger and the program state, can also be used to monitor the Linux kernel. To this end, the /proc/kcore maps the entire memory of the system to the format of a core file. So, if we give this file to a debugger we can check the current state of the system.

## Compiler Options

In addition to a core file, a debugger requires a file with the executable program. In case of the Linux kernel, this is available under the name vmlin in the directory where it was compiled. When compiling a program to be debugged, the compiler should have inserted debugging information (the full names of variables in text form and references to the relevant places in the source code). If this information is available, the debugger lets you (for example) query variables by their name.

The C gcc gives you the -g option to embed debugging information during compilation. This option has to be entered in a make file at the appropriate position to ensure that it will be used when the Linux kernel is compiled. If we want to achieve this for the entire kernel, we can add this option to the CFLAGS variable in the main file in the top directory of the source-code tree. If we want to check only limited areas in the debugger, it is sufficient to add one EXTRA_CFLAGS=-g line to add to the make files that contain the files for each of these areas. For example, this would be to use /ip4/Makefile.

gdb and ded One of the most popular debuggers in UNIX is the gdb debugger, developed under the auspices of the Free Software Foundation (FSF). gdb offers only a text interface to the user, so it is not comfortable to use. More recently, front ends have been developed to remove this drawback (e.g., by offering a graphical user interface). Two representatives of this kind were also developed by FSF: the Data Debugger d, and the Grand Unified Debugger (gud) mode of the emacs editor dd has options for graphical representation of data structures, which make it particularly suitable to such data structures in the Linux kernel.

A detailed description of how these tools would go beyond the scope and volume of this book. Detailed instructions are included in each of the distribution packages.
