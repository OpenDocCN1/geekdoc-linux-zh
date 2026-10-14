diagnostic tools on those systems with pretty good response times. On the other hand, I’ve seen systems with relatively low I/O-bound loads on which just logging in took a minute, since the disk I/O was completely saturated. A system that runs out of RAM resources often appears to have I/O-bound load, since once the system starts using swap storage on the disk, it can consume disk resources and cause a downward spiral as processes slow to a halt.

# top

One of the first tools I turn to when I need to diagnose high load is top. I have discussed the basics of how to use the top command in Chapter 2, so here I will focus more on how to use its output to diagnose load. The basic steps are to examine the top output to identify what resources you are running out of (CPU, RAM, disk I/O). Once you have figured that out, you can try to identify what processes are consuming those resources the most. First let’s examine some standard top output from a system:

```
top - 14:08:25 up 38 days,  8:02,  1 user,  load average: 1.70, 1.77, 1.68
Tasks: 107 total,   3 running, 104 sleeping,   0 stopped,   0 zombie
Cpu(s): 11.4%us, 29.6%sy,  0.0%ni, 58.3%id,  0.7%wa,  0.0%hi,  0.0%si,  0.0%st
Mem:   1024176k total,   997408k used,   26768k free,   85520k buffers
Swap:  1004052k total,   4360k used,   999692k free,   286040k cached
```

| PID | USER | PR | NI | VIRT | RES | SHR | %CPU | %MEM | TIME+ | COMMAND |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 9463 | mysql | 16 | 0 | 686m | 111m | 3328 | S | 53 | 5.5 | 569:17.64 mysqld |
| 18749 | nagios | 16 | 0 | 140m | 134m | 1868 | S | 12 | 6.6 | 1345:01 nagios2db_status |
| 24636 | nagios | 17 | 0 | 34660 | 10m | 712 | S | 8 | 0.5 | 1195:15 nagios |
| 22442 | nagios | 24 | 0 | 6048 | 2024 | 1452 | S | 8 | 0.1 | 0:00.04 check_time.pl |

The first line of output is the same as you would see from the uptime command. As you can see in this case, the machine isn’t too heavily loaded for a four-CPU machine:

```
top - 14:08:25 up 38 days,  8:02,  1 user,  load average: 1.70, 1.77, 1.68
```

top provides you with extra metrics beyond standard system load, though. For instance, the Cpu(s) line gives you information about what the CPUs are currently doing:

```
Cpu(s): 11.4%us, 29.6%sy,  0.0%ni, 58.3%id,  0.7%wa,  0.0%hi,  0.0%si,  0.0%st
```