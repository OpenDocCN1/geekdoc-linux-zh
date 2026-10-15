By default, most systems ship with nsswitch.conf files that are reasonable for a stand-alone machine. All entries go to the flat files, with the exception of host lookups, which first consult flat files and then DNS. A few systems default to compat mode for passwd and group, which is probably worth changing. If you really use NIS, just explicitly put it in the nsswitch.conf file.

# nscd: cache the results of lookups

On some Linux distributions, another finger in the system file pie belongs to nscd, the somewhat misleadingly titled name service cache daemon.

nscd works in conjunction with the C library to cache the results of library calls such as getpwent. nscd is simply a wrapper for these library routines; it knows nothing about the actual data sources being consulted. nscd should in theory improve the performance of lookups, but any improvement is largely unnoticeable from the user’s viewpoint.

We say that “name service cache daemon” is misleading because the term “name service” usually refers to DNS, the distributed database system that maps between hostnames and Internet addresses. nscd does in fact cache the results of DNS lookups (because it wraps gethostname, etc.), but it also wraps the library routines that access information from the passwd and group files and their network database equivalents. (For security, lookups to /etc/shadow are not cached.)

In concept, nscd should have no effect on the operation of the system other than to speed up repeated lookups. In practice, it can cause unexpected behavior because it maintains its own copy of the lookup results. Lookups are stored in the cache for a fixed amount of time (set in nscd’s configuration file, /etc/nscd.conf), and there is always the possibility that recent changes will not be reflected in nscd’s cache until the previous data has timed out. nscd is smart enough to monitor local data sources (such as /etc/passwd) for changes, so local updates should propagate within 15 seconds. For remote entries, such as those retrieved through NIS, you may have to wait for the full timeout period before changes take effect.

Among our example distributions, only SUSE runs nscd by default. Red Hat installs nscd but does not start it at boot time by default; to enable the use of nscd, run chkconfig nscd on. Ubuntu is nscd compatible but does not include nscd in the default installation; run apt-get install nscd to download it.

nscd starts at boot time and runs continuously. The default /etc/nscd.conf specifies a timeout of 10 minutes for passwd data and an hour for hosts and group, with a 20-second negative timeout (the amount of time before an unsuccessful lookup is retried). In practice, these values rarely need changing. If a change you recently made doesn’t seem to show up, nscd is probably the reason.

See Chapter 17 for more information about DNS.