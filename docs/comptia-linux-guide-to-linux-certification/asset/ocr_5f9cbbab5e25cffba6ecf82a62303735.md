| Option | Description |
| :-: | :-: |
| -A | Displays the most information; this option is equivalent to all options |
| -b | Displays I/O statistics |
| -B | Displays swap statistics |
| -d | Displays Input/Output statistics for each block device on the system |
| -f file_name | Displays information from the specified file; these files typically reside in the /var/log/sa directory |
| -n ALL | Reports all network statistics |
| -o file_name | Saves the output to a file in binary format |
| -p CPU# | Specifies statistics for a single CPU (the first CPU is 0, the second CPU is 1, and so on) |
| -q | Displays statistics for the processor queue |
| -r | Displays memory and swap statistics |
| -R | Displays memory statistics |
| -u | Displays CPU statistics; this is the default action when no options are specified |
| -v | Displays kernel-related filesystem statistics |
| -w | Displays swapping statistics |

# Table 14-1 Common options to the sar command

Another important option to the sar command is -q, which shows processor queue statistics. A processor queue is an area of RAM that stores information temporarily for quick retrieval by the CPU. To view processor queue statistics every five seconds, you can execute the following command:

```
[root@server1 ~]# sar -q 1 5
Linux 3.11.10-301.fc20.x86_64 (server1)  11/01/2015 _x86_64_ (2 CPU)

08:34:36 AM  rrunq-sz  plistsz  ladvq-l  ladvq-5  ladvq-15  blocked
08:34:37 AM   0       252   0.00   0.00   0.00   0
08:34:38 AM   0       252   0.00   0.00   0.00   0
08:34:39 AM   0       252   0.00   0.00   0.00   0
08:34:40 AM   0       252   0.00   0.00   0.00   0
08:34:41 AM   0       252   0.00   0.00   0.00   0
Average:      0       252   0.00   0.00   0.00   0
[root@server1 ~]#_
```

The rrunq-sz (run queue size) indicates the number of processes that are waiting for execution on the processor run queue. For most Intel architectures, this number is typically 2 or less on average.

![](bbox=[0.145, 0.84, 0.31499999999999995, 0.9149999999999999])

> A rrunq-sz much greater than 2 for long periods of time indicates that the CPU is too slow to respond to system requests.