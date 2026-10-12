send information to the kernel. Many Linux utilities extract information from dynamically created directories and files under this directory, also known as a virtual filesystem. For example, the free command obtains its information from a file named meminfo:

```
$ free
    total     used      free    shared    buffers cached
Mem:  223260   157800   65460   0  55400  58872
-/+ buffers/cache:  43528  179732
Swap:  491392    400   490992
```

This information constantly changes as the system is used. You can get the same information by using the cat command to see the contents of the meminfo file:

```
$ cat /proc/meminfo
    total:   used:   free:  shared: buffers:  cached:
Mem:  228618240 161673216 66945024  0  56750000 60694528
Swap:  503185408 409600 502775808
MemTotal:     223260 kB
MemFree:      65376 kB
MemShared:     0 kB
Buffers:      55420 kB
Cached:       58872 kB
SwapCached:   400 kB
Active:       100328 kB
Inact_dirty:  25044 kB
Inact_clean:  19012 kB
Inact_target: 28876 kB
HighTotal:    0 kB
HighFree:     0 kB
LowTotal:     223260 kB
LowFree:      65376 kB
SwapTotal:    491392 kB
SwapFree:     490992 kB
Committed_AS: 51424 kB
```

The /proc directory can also be used to dynamically alter the behavior of a running Linux kernel by "echoing" numerical values to specific files under the /proc/sys directory. For example, to "turn on" kernel protection against one type of Denial Of Service (DOS) attack known as SYN flooding, use the echo command to send the number 1 (one) to the following /proc path:

```
# echo 1 > /proc/sys/net/ipv4/tcp_syncookies
```

# NOTE

The Linux kernel has a number of built-in protections, but good system administration security policies and a secure firewall protecting your gateway, router, or Internet-connected system are