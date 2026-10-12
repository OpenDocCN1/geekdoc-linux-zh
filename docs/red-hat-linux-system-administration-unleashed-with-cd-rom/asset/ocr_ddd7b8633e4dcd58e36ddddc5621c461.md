# Decoding Kernel Errors

For the most part, the only immediately useful information you can glean from an oops message, in its raw state, is identifying which program or driver is causing a problem. The Linux kernel maintainers have developed a system for decoding the results of oops messages and reporting them back to the maintainers. This includes running ksymoops to decode the oops message, saving the output to a report file, and filing a report, along with any system-specific information that might be useful.

# ksymoops

The program used to decode oops messages is ksymoops, which gets loaded on a Red Hat 6 system if you select “Kernel development” during a custom install. To use ksymoops, you need to compile it, then copy the oops message from /var/log/messages to a separate file and run it through ksymoops.

Before you can use ksymoops, you need to compile it for your system:

```
[root@wallace /root]# cd /usr/src/linux/scripts/ksymoops
[root@wallace ksymoops]# make
```

The documentation for ksymoops is /usr/src/linux/scripts/ksymoops/README. It does not create a man page, but the essential options are

```
Usage: ksymoops
[-v vmlinux] Where to read vmlinux
[-V] No vmlinux is available
[-o object_dir] Directory containing modules
[-O] No modules is available
[-k ks yms] Where to read ks yms
[-K] No ks yms is available
[-i lsmod] Where to read lsmod
[-L] No lsmod is available
[-m system.map] Where to read System.map
[-M] No System.map is available
[-s save.map] Save consolidated map
[-c code_bytes] How many bytes in each unit of code
[-f] One shot toggle (exit after first Oops)
[-d] Increase debug level by 1
[-h] Print help text
```

The purpose of ksymoops is to provide trace information for debugging an oops. In the previous oops message, for instance, use a text editor to extract and copy the raw oops message from the log file to the file /tmp/oops.txt. You would then run it through ksymoops as follows: