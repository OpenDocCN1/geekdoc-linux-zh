# AIX workload partitions

# 1001

Now the zone is running, and an invocation of zlogin -C proprietary-zone will connect to its console. The boot process for a zone is like that of a physical system, connecting with zlogin before bootstrapping complete displays output the boot process. We must perform all the normal configuration for a new system, such as choosing login options and an authentication method.

The remaining task is to create a zone for our web server. The server zone will share the default resource pool with the global zone, it's not necessary to create a new pool. Instead, we would just create the zone with zonecfg as above, but with set-pool-pool-default.

There is considerably more depth to zones and containers that we've shown here. Advanced features that administrators should be aware of include migration of zones between physical systems (although migrations are not supported), ZFS resources for smaller whole-root zones, and "branded zones" that support running binaries from other platforms (e.g., Linux) on a Solaris kernel.

# 24.6 AIX WORKLOAD PARTITIONS

IBM has been in the virtualization game a long time. They pioneered the concept in the 1960s, but it wasn't until the release of AIX 6.1 in 2007 that software virtualization was included in AIX. Any system capable of running AIX 6 workloads partitions (WPARs). This technology is distinct from IBM's logical partition implementations found in versions as early as 4.3)

WPARs run in an isolated execution environment. Processes can only communicate with peers in the same partition. Signals and events in the global environment do not affect the partition, and vice versa. WPARs can have their own dedicated network addresses.

WPARs are served in two delicious flavors: system and application.

+   A system WPAR shares only the AIX kernel with the global environment (the host, essentially). An application running in a system WPAR believes it is running in an independent AIX installation with its inet daemon for networking autonomy.

+   An WPAR runs a single application in an isolated environment. It shares all filesystems with the global environment and cannot provide remote access capabilities. The application WPAR exits when the application completes.

IBM provides several tools for managing WPARs, continuing the AIX tradition of convenient administration. We discuss the command-line interface here, but administrators should be aware that in typical AIX fashion, there is a full SM interface as well as WPAR Manager, a web-based management interface for centralized management of multiple servers and their workload partitions.

![](bbox=[0.953, 0.423, 0.993, 0.547])