
# Chapter 5. The proc File System

- rsig-max — Configures the maximum number of POSIX realtime signals that the system may have queued at any one time. The default value is 1024.
- rsig-nr — The current number of POSIX realtime signals queued by the kernel.
- sem — Configures semaphore settings in the kernel. A semaphore is a System V IPC object that is used to control utilization of a particular process.
- shmall — Sets the total amount of shared memory that can be used at one time on the system, by bytes. The default value is 209712.
- shmmax — Sets the largest shared memory size allowed by the kernel, in bytes. By default, this value is 3555432. However, the kernel supports much larger values than this.
- shmni — Sets the maximum number of shared memory segments for the whole system, in bytes. By default, this value is 4096.
- sysrq — Activates the System Request Key, if this value is set to anything other than the default of 0. See 5.3.9/proc/sys/sys for details about the System Request Key.
- threads-max — Sets the maximum number of threads to be used by the kernel, with a default value of 2048.
- version — Displays the date and time the kernel was last compiled. The first field in this file, as #3, relates the number of times a kernel was built from the source. random stores a number of values related to generating random numbers for the kernel.

## 5.3.9./proc/sys/net/

This directory contains subdirectories concerning various networking topics. Various configurations at the time of kernel compilation make these directories available, such as appletalk, ethernet, ipv4, and ipv6. Within these directories, system administrators are able to adjust the network configuration on a running system.

Given the wide variety of possible networking options available with Linux, the most common /proc/sys/net/ directories will be discussed.

The proc/sys/net/core/ directory contains a variety of settings that control the interaction between the kernel and networking layers. The most important of these files are:

- message-burst — The time in seconds of a new warning message. This is used to prevent Denial of Service (DoS) attacks. The default setting is 50.
- message-cost — Also used to prevent DoS attacks by placing a cost on every warning message. The higher the value of this file (default of 5), the more likely the warning will be ignored.

The idea of a DoS attack is to bombard the system with requests that generate errors and fill disk partitions with logs or require all of the system's resources to handle the error logging. The settings in message_burst and message_cost are designed to be modified based on the system's recursive need for comprehensive logging.
- netdev_max_backlog — Sets the maximum number of packets allowed to queue when a particular interface receives packets faster than the kernel can process them. The default value for this is 300.
- optem_max — Configures the maximum ancillary buffer allowed per socket.
- rmem_default — Sets the receive socket buffer default size in bytes.
- rmem_max — Sets the receive socket buffer maximum size in bytes.
- wmem_default — Sets the send socket buffer default size in bytes.
- wmem_max — Sets the send socket buffer maximum size in bytes.

/proc/sys/net/ipv4/ contains additional networking settings. Many of these settings, used in conjunction with one another, are very useful in preventing attacks on the system or using the system as a router.

![](img/31025704b51d5760c0228ff0f3db98bf_85_0.png)

> Caution
> An erroneous change to these files may affect remote connectivity to the system.

Here are some of the most important files in the /proc/sys/net/ipv4/:

- icmp_destreach_rate, icmp_echoreply_rate, icmp_paramprob_rate and icmp_timeexceeded_rate — Set the maximum ICMP send packet rate, in 1/100 of a second, to hold under conditions. A setting of 0 removes any entry and is not a good idea.
- icmp_echo_ignore_all and icmp_echo_broadcasts — Allows the kernel to ignore ICMP packets from host or only those originating from broadcast and multicast addresses. A value of 0 allows the kernel to respond, while a value of 1 ignores the packets.
- ip_default_ttl — Sets the default Time To Live (TTL), which limits the number of hops a packet may make before reaching its destination. Increasing this can diminish performance.
- ip_forward — Permits files on the system to forward packets to one another. By default, this file is set to 0. Setting it to 1 enables network packet forwarding.
- ip_local_port_range — Specifies the range of ports to be used for UDP or TCP when a port is needed. The first number is the lowest to be used and the second number specifies the highest port. Any value from 1024 to 4999 should be used in this file.
- tcp_syn_retries — Provides a limit on the number of times the system will retransmit a SYN packet when attempting to make a connection.
- tcp_retries1 — Sets the number of permitted re-transmissions to answer an incoming connection. Default of 3.
- tcp_retries2 — Sets the number of permitted re-transmissions to answer an incoming connection. Default of 15.

The usr/src/linux-2.4/Documentation/networking/ip-sysctl.txt contains various options.

The /proc/sys/net/ipv4/conf/ directory contains settings.

The /proc/sys/net/ipv4/neigh/ directory contains settings.

The /proc/sys/net/ipv4/all/ directory contains settings.

The /proc/sys/net/ipv4/default/ directory contains settings.

The /proc/sys/net/ipv4/custom/ directory contains settings.

The /proc/sys/net/ipv4/tcp/ directory contains settings.

The /proc/sys/net/ipv4/udp/ directory contains settings.

The /proc/sys/net/ipv4/icmp/ directory contains settings.

The /proc/sys/net/ipv4/arp/ directory contains settings.

The /proc/sys/net/ipv4/ip/ directory contains settings.

Additional information about these can be found in usr/src/linux-2.4/Documentation/filesystems/proc.

# Chapter 5. The proc File System

## 5.3.9./proc/sys/vm/

This directory facilitates the configuration of the virtual memory (VM) subsystem. The following files are commonly found in /proc/sys/vm/:

- bflush — Sets various values related to the bflush daemon.
- buffermem — Allows you to control the amount of system memory used as buffer.
- kswapd — Sets various values concerned with the kernel swap-out daemon.
- max_map_count — Configures the maximum number of memory maps a process may have.
- overcommit_memory — When set to default value of 0 the kernel estimates the amount of memory available.
- pagecache — Controls the amount of memory used by the page cache.
- pagecluster — Sets the number of pages read in a single attempt.
- pagetable_cache — Controls the number of page tables that are cached on a per-processor basis.

The usr/src/linux-2.4/Documentation/sysctl/vm.txt file contains additional information on these files.
