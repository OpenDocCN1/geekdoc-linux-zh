```
```
fdiv bug        : no
hlt bug        : no
f00f_bug       : no
coma_bug       : no
fpu            : yes
fpu_exception  : yes
cpuid level    : 2
wp             : yes
flags          : fpu vme de pse tsc msr pae mce cx8 sep mtrr pge mca
                 cmov pat pse36 mmm fxsr sse
bogomips       : 1291.05
```
```

In this case, there is only an entry for a single processor, so on average there was slightly more work for the processor to do than it could keep up with. At a high level, this implies that the machine has more work to do than it can keep up with. Note: If `uptime` showed a load average of something less than 2.00 on a two-CPU machine, that would indicate that the processors still have additional free cycles. The same would be true on a four-CPU machine with a load average less than 4.00, and so on. However, the load average alone does not tell the entire story.

In this case, the machine in question was a laptop. The workload included an email client, word processors, web browsers, some custom applications, chat clients, and so on, all running simultaneously. However, the response time to the various workloads was deemed to be acceptable by the user.

This implies that the operating system scheduler was appropriately prioritizing tasks that needed to be run based on those that were most interactive. No significant server aspects were running on the machine, so there was no impact from the high load average on other clients or machines.

So, although the tool indicates that the CPU was fully utilized, it does not indicate what the system was doing or why it was so busy. And, if the response time for the users of the system was acceptable, there may not be any reason to probe more deeply into the system's operation.

However, this chapter would be uninteresting if we stopped there. Quite often, simple tools like `uptime` are a user's quick way to attempt to account for any perceived slowness in an application's response time. If the load average for the system indicates that the response time may be caused by an overloaded processor (or processors), a variety of other tools can be used to narrow down the cause of the load.

To drill down a bit further into how the processors are being used, we'll look at three tools that provide us with a variety of different insights about the CPU utilization: `vmstat`, `iostat`, and `top`. Each of these commands has a different focus on system monitoring, but each can be used to get a different perspective on how the processor is being utilized. In particular, the next step would be to understand if the processor is primarily spending time in the operating system (often referred to as kernel space) or in the application (often referred to as user space), or if the processor is idle. Further, if the processor is idle, understanding why it is idle is key to any further performance analysis. A processor can be idle for a number of reasons. For instance, the most obvious reason is that a process cannot run. This may sound too obvious, but if a component of the workload, such as a particular process or task, is not running, performance may be impacted. In some cases, caching components or fallback mechanisms allow some applications to continue to run, although with degraded throughput. As an example, the Internet domain name service is often configured to consult