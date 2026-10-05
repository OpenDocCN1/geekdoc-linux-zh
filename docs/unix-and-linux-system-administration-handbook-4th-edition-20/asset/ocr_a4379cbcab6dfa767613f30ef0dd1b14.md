# Chapter 19

# Sharing System Files

By default, most systems ship with nswitch.conf files that are reasonable for a stand-alone machine. All entries go to the flat files, with the exception of host lookups, which first construct flat files and then DNS. A few systems default to compat mode for passwd and group, which is probably worth changing. If you use NIS, just put it in the nswitch.conf file.

# nscd: cache the results of lookups

On Linux distributions, another finger in the system file belongs to nscd, the somewhat misleadingly named service daemon.

nscd works in conjunction with the C library to cache the results of library calls such as getpwd. nscd is a wrapper for these library routines; it knows nothing about the actual data sources being consulted. nscd should in theory improve the performance of lookups, but any improvement is rarely unnoticed from the user's viewpoint.

![](bbox=[0.198, 0.233, 0.227, 0.273])

See Chapter 17 for more information about DNS.

We say that "name service daemon" is misleading because the term "service" usually refers to DNS, the distributed database system that matches hostnames and Internet addresses. nscd does in cache the results of DNS lookups (because it wraps gethostname, etc.), but it also wraps the library routines that access information from the passwd and group files and their network databases. (For security, lookups to /etc/shadow are not cached).

In concept, nscd should have no effect on the operation of the system other than speed up repeated lookups. In practice, it can cause unexpected behavior because it maintains its own copy of the lookup results. Results are stored in the cache for a fixed amount of time (set in nscd's configuration file, /etc/nscd.conf), and there is the possibility that recent changes will not be reflected in nscd's cache until the previous day has timed out. nscd is smart to monitor local data sources (such as /etc/passwd) for changes, so local updates propagate within 15 seconds. For remote entries, as those retrieved through NIS, you may have to wait for the full timeout before changes take effect.

Among example distributions, only SUSE run nscd by default. Red Hat has nscd but does not start at boot time by default; to ensure the use of nscd, run chconfig nscd. Ubuntu is compatible but does not include nscd in the default installation; run apt-get install nscd to download.

nscd starts at boot time and runs continuously. The /etc/nscd.conf specifies a timeout of 10 minutes for passwd data and an hour for hosts and group, with a 20-second negative timeout (the amount of time before an unsuccessful lookup is retried). In practice, these values rarely need changing. If a change recently made doesn't show up, nscd is probably the reason.