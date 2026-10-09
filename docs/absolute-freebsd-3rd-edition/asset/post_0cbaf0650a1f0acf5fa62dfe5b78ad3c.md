
## 21 SYSTEM PERFORMANCE AND MONITORING

![](img/f11aeb3fa2ed406688e13ccb43ed9dab_758_0.png)

Even if “it’s slow!” isn’t the most dreaded phrase a system administrator can hear, it’s pretty far up on the list. The user doesn’t know why the system is slow and probably can’t quantify or qualify the problem any further than that. It just feels slow. Usually there’s no test case, no set of reproducible steps, and nothing particularly wrong. A slowness complaint can cause hours of work as you dig through the system trying to find problems that might or might not even exist.

One phrase is more dreadful still, especially after you’ve invested those hours of work: “it’s still slow.”

An inexperienced sysadmin accelerates slow systems by buying faster hardware. This exchanges “speed problems” for costly parts and even more expensive time. Upgrades just let you conceal problems without actually using the hardware you already own, and sometimes they don’t even solve the problem at all.

You can frequently solve performance problems by tweaking the software that’s causing the problems. Your WordPress site is slow? Investigate running PHP under memcached or another PHP accelerator. FreeBSD is only one layer of your application stack, so be sure to give the other layers proper attention.

FreeBSD includes many tools designed to help you examine system performance and provide the information necessary to learn what’s actually slowing things down. Some of them, such as dtrace(1), are highly complicated and require extensive knowledge of the system, the software, and a book of their own. Once you understand where a problem is, identifying the solution to the problem becomes much simpler. You might actually need faster hardware, but sometimes shifting system load or reconfiguring software might solve the problem at much less expense. In either case, the first step is understanding the problem.

### Computer Resources

Performance problems are usually caused by running more tasks than the computer can handle. That seems obvious, but think about it a moment. What does that really mean?

A computer has four basic resources: input/output, network bandwidth, memory, and CPU. If any one of them is filled to capacity, the others can’t be used to their maximum. For example, your CPU might very well be waiting for a disk to deliver data or for a network packet to arrive. If you upgrade your CPU to make your system faster, you’ll be disappointed. Buying a whole new server might fix the problem, but only by expanding the existing bottleneck. The new system probably has more memory, faster disks, a better network card, and faster processors than the old one. You have deferred the problem until the performance reaches some new limit. However, by identifying where your system falls short and addressing that particular need, you can stretch your existing hardware much further. After all, why purchase a whole new system when a few gigabytes of relatively inexpensive memory would fix the problem? (Of course, if your goal is to retire this “slow” system to make it your new desktop, that’s another matter.)

Input/output is a common bottleneck. System busses have a maximum throughput, and while you might not be pushing your disk or your network to their limits, you might be saturating the bus by continually bombarding both.

One common cause of system slowdowns is running multiple large programs simultaneously. Not only does disk I/O become saturated, but the processors might spend the majority of their time waiting to swap data between the on-CPU cache and the memory. For example, I once thoughtlessly scheduled a massive database log rotation that moved and compressed gigabytes of data at the same time as the daily periodic(8) run. Since the job required shutting down the main database and caused application downtime, speed was crucial. Both the database job and the periodic(8) run slowed unbearably. Rescheduling one of them made both jobs go more quickly.

FreeBSD has some features that improve performance. Doing lots of cryptographic operations? Use the aesni(4) kernel module. Database is disk bound? Consider the filesystem block size. ZFS pool slow? Maybe you need an add-on cache. Identifying what you should change requires a hard look at the system, however.

We’re going to look at several FreeBSD tools for examining system performance. Armed with that information, we’ll consider how to fix performance issues. Each potential bottleneck can be evaluated with the proper tools. FreeBSD changes continually, so later systems might have new tuning options and performance features. Read tuning(7) on your system for current performance tips.

### WHAT IS NORMAL?

One word you’ll keep tripping over in this chapter is *abnormal*. As the sysadmin, you’re supposed to know what’s normal for your system. It’s somewhat like art; you might not be able to define *normal*, but you need to recognize *abnormal* when you see it. Use these tools regularly when the system is behaving itself so you can have a good idea of which results are out of whack during system slowdowns. Pay attention to your hardware!

### Checking the Network

If you're concerned about network performance, measure it. Consult `netstat -m` and `netstat -s`, and look for errors or places where you're out of memory or buffers. These are instantaneous snapshots, but for the network, you really need to evaluate congestion and latency over minutes, hours, and even days. The network team probably has a tool like Cacti, Zabbix, or Graphite to observe long-term performance.¹ Ask them for information. Combine what these tools provide with your instantaneous snapshots. If the average throughput per minute on your 10-gig Ethernet is only 5 gigabits a second, but your instantaneous measurements show frequent spikes up to the full 10 gigabit, you probably have really bursty connectivity.

Some network cards can better handle a full network in *polling mode*. Polling tells the network card to stop sending frames up to the operating system as they arrive and instead let the operating system visit every so often to collect the frames. Check your network card’s man page to see whether it supports polling. Enable and disable polling with `ifconfig(8)`.

A heavily loaded network might benefit from a different congestion control algorithm. FreeBSD provides several TCP congestion control algorithms. Look for files beginning with `cc_` in `/boot/kernel`; these are congestion control modules. Each has a man page.

View the currently loaded congestion control algorithms with the `sysctl net.inet.tcp.cc.available`.

```shell
# sysctl net.inet.tcp.cc
net.inet.tcp.cc.available: newreno
```

New Reno is the traditional congestion control algorithm. The congestion control kernel modules on this system include CDG, CHD, CUBIC, DCTCP, HD, H-TCP, and Vegas. The H-TCP algorithm is specifically designed for long-distance, high-bandwidth applications. Let’s enable it.

```shell
# kldload /boot/kernel/cc_htcp.ko
# sysctl net.inet.tcp.cc.available
```

We now have H-TCP available in the kernel. Enable it with the net.inet.tcp.cc.algorithm sysctl.

```shell
# sysctl net.inet.tcp.cc.algorithm=http
net.inet.tcp.cc.algorithm: newreno -> http
```

Ultimately, you can’t fit 10 pounds of bandwidth in a 5-pound circuit. If your saturated Ethernet is crippling your applications, turn off unnecessary network services or add more bandwidth.

Other system conditions are much more complicated. Start by checking where the problem lies with vmstat(8).

### General Bottleneck Analysis with vmstat(8)

FreeBSD includes several programs for examining system performance. Among these are vmstat(8), iostat(8), and systat(1). We’ll discuss vmstat(8) because I find it most helpful; iostat(8) is similar to vmstat(8), and systat(1) provides the same information in an ASCII graphical format.

Use vmstat(8) to see the system’s current virtual memory statistics. While the output takes getting used to, vmstat(8) is very good at showing large amounts of data in a small space. Type **vmstat** at the command prompt and follow along.

```
# vmstat
procs memory            page            disks           faults           cpu
 r  b  w  avm    fre    flt re  pi  po     fr  sr ad0 ad1    in   sy     cs us sy id
 8  0  0  1.3G   26G    157   0   1   0    172   1   0   0    12  212    149  0  0 100
```

The vmstat divides its display into six sections: process (**procs**), memory, paging (**page**), disks, faults, and cpu. We’ll look at all of them quickly and then discuss in detail those parts that are the most important for investigating performance issues. This single line represents the average values for the whole time the system has been running. We’ll get more real-time data in the next section.
