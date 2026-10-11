| **Table 13-2 Common options to the sar command (Continued)** |
|---|---|
| **Option** | **Description** |
| `-q` | Displays statistics for the processor queue |
| `-r` | Displays memory and swap statistics |
| `-R` | Displays memory statistics |
| `-u` | Displays CPU statistics; this is the default action when no options are specified |
| `-v` | Displays kernel-related filesystem statistics |
| `-W` | Displays swapping statistics |

From Table 13-2, you can see that the `-b` and `-d` options to the `sar` command display information similar to the output of the `iostat` command. In addition, the `-u` option displays CPU statistics equivalent to the output of the `mpstat` command.

Another important option to the `sar` command is `-q`, which shows processor queue statistics. Recall that a queue, also known as a cache, is used to store information temporarily for a certain device; the queues that surround the CPU are known as L1, L2, and L3 cache. To view processor queue statistics every five seconds, you can execute the following command:

```
```
[root@server1 root]# sar -q 1 5
Linux 2.6.5-1.358 (server1)          07/14/2005

12:31:10 PM runq-sz plist-sz ldavg-1 ldavg-5 ldavg-15
12:31:11 PM    0      82    0.45    0.36    0.21
12:31:12 PM    0      82    0.45    0.36    0.21
12:31:13 PM    0      82    0.45    0.36    0.21
12:31:14 PM    0      82    0.41    0.35    0.21
12:31:15 PM    0      82    0.41    0.35    0.21
Average:        0      82    0.43    0.36    0.21
[root@server1 root]# _
```
```

The `runq-sz` (run queue size) indicates the number of processes that are waiting for execution on the processor run queue; for most Intel architectures, this number is typically two or less on average.

> NOTE
> 
> A `runq-sz` much greater than two for long periods of time indicates that the CPU is too slow to respond to system requests.