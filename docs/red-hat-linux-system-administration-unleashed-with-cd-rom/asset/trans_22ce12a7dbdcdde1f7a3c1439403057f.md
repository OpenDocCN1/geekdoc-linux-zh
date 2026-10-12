
The two utilities that allow you to perform job automation under Red Hat Linux were covered in detail; they are the at and cron utilities. You should be able to use either of those utilities to automate jobs, using at for one-time tasks and cron for regular tasks. I believe that you will find both utilities to be very helpful in your system administration duties.

在 Red Hat Linux 下允许你执行作业自动化的两个实用程序已详细讲解；它们是 at 和 cron 实用程序。你应该能够使用其中任一实用程序来自动化作业，使用 at 处理一次性任务，使用 cron 处理定期任务。我相信你会发现这两个实用程序在系统管理职责中非常有帮助。

Finally, this chapter looked at debugging cron jobs, a useful skill for any Red Hat Linux system administrator to master. Things can go wrong with cron jobs and because they execute automatically, it can be difficult to isolate problems.

最后，本章探讨了调试 cron 作业，这对任何 Red Hat Linux 系统管理员来说都是一项需要掌握的有用技能。cron 作业可能会出现问题，而且由于它们会自动执行，因此很难隔离问题。

In closing, I hope you have gained some useful knowledge and skills from this chapter and that you can find new and interesting ways of automating your system administration tasks.

最后，我希望你能从本章获得一些有用的知识和技能，并且能够找到新颖有趣的方式来自动化你的系统管理任务。

## System Tuning and Kernel Building

系统调优与内核构建

### PART X

### PART X

### In This Part
- 34 Tuning Your Linux System 1047
- 35 Customizing the Linux Kernel 1081
- 36 Centennial School District, Portland, Oregon 1135

### 本部分
- 34 调优你的 Linux 系统 1047
- 35 自定义 Linux 内核 1081
- 36 Centennial School District, Portland, Oregon 1135

## Tuning Your Linux System

调优你的 Linux 系统

### In This Chapter
- General Areas of Tuning 1049
- Weighing Costs and Benefits 1052
- Understanding Performance Measurement Techniques 1055
- Understanding Network Performance 1067
- Memory and Swap Space 1068
- Swap Space Priorities 1071
- Swap Partitions Versus Swap Files 1074
- Tunable Parameters in /proc 1075
- Using echo to Alter System Behavior 1078

### 本章中
- 调优的一般领域 1049
- 权衡成本与收益 1052
- 理解性能测量技术 1055
- 理解网络性能 1067
- 内存和交换空间 1068
- 交换空间优先级 1071
- 交换分区与交换文件 1074
- /proc 中的可调参数 1075
- 使用 echo 修改系统行为 1078

Linux systems require a great deal of maintenance and care. Performance tuning is the art of making a Linux system operate at its best possible level. This chapter focuses on performance considerations including techniques, costs and benefits, memory, swap space and priorities, swap partitions, and manipulating the /proc filesystem (the interface to the Linux Kernel).

Linux 系统需要大量的维护和保养。性能调优是让 Linux 系统以最佳可能水平运行的艺术。本章重点关注性能考虑，包括技术、成本和收益、内存、交换空间及优先级、交换分区，以及操作 /proc 文件系统（Linux 内核的接口）。

Among the many chores and tasks a systems administrator must perform, tuning is definitely one of the most rewarding (perhaps second to installation activities). Tuning means that the administrator has taken the time and effort to make sure the system operates at a level of acceptable performance. Most often this can be measured by the user's experience. For example, a terminal user who is on the local network expects immediate response from listing files, whereas a programmer expects a certain time to elapse while compiling a project he is working on. Over time, the administrator will develop an affinity for how the system should perform at different time intervals and periods.

在系统管理员必须执行的众多杂务和任务中，调优绝对是最有回报的（或许仅次于安装活动）。调优意味着管理员花时间和精力确保系统以可接受的性能水平运行。最常可以通过用户体验来衡量。例如，本地网络上的终端用户期望列出文件时立即响应，而程序员则期望在编译正在处理的项目时花费一定的时间。随着时间的推移，管理员将形成对系统在不同时间间隔和时段应如何表现的亲和力。

All systems, including Linux, require some degree of performance tuning. Perhaps not immediately, but it is rare that a system's tasks do not grow to the point where the system's performance must be examined. As the system's functions become more complex, require more processor time, and put more demand on memory and disk I/O, tuning becomes an important factor in the growth and well-being of the system.

所有系统，包括 Linux，都需要一定程度的性能调优。也许不是立即需要，但很少有系统的任务不会增长到必须检查系统性能的地步。随着系统功能变得更加复杂，需要更多的处理器时间，并对内存和磁盘 I/O 提出更高要求，调优成为系统成长和健康的重要因素。

Users are what ultimately matter. Linux provides a strong base to operate from (as do HURD and many commercial versions of UNIX). However, no system will ever operate at the level users expect it to. What users expect and what they receive is very important. Of all people, a systems administrator should expect (and sympathize with) what the user wants. Just because you like Linux does not mean the average user does; you must forget how you perceive the system and see how the users perceive it. Many users outright dislike UNIXish systems. This is where tuning takes its shape, beating what is expected by delivering what is real and giving your system as much power as it can have. This is the essence of performance tuning.

用户才是最终重要的。Linux 提供了强大的运行基础（HURD 和许多商业版 UNIX 也是如此）。然而，没有任何系统能达到用户期望的水平。用户期望什么以及他们实际获得什么非常重要。在所有人中，系统管理员应该期望（并同情）用户想要什么。仅仅因为你喜欢 Linux 并不意味着普通用户也喜欢；你必须忘记你对系统的感知，看看用户如何感知它。许多用户 outright 讨厌类 UNIX 系统。这就是调优发挥作用的地方，通过提供真实的东西超越期望，并让你的系统发挥出尽可能大的能力。这就是性能调优的本质。

Tuning a system sounds great, but what are some of the aspects of tuning, or perhaps more appropriately, where are the aspects of tuning and what does a systems administrator have to take into account when approaching bottlenecks and other performance issues? Let's take that two-part question and address the first half, general areas of tuning.

调优系统听起来很棒，但调优有哪些方面，或者更恰当地说，调优的方面在哪里，系统管理员在处理瓶颈和其他性能问题时需要考虑什么？让我们把这个两部分的问题拿出来并先解决第一部分，一般调优领域。

## General Areas of Tuning

一般调优领域

Problems come in three major areas, two of which (I/O and CPU) are nearly directly related (it is important to note that all three are related in one way or another). The three general areas are

问题主要出现在三个大领域，其中两个（I/O 和 CPU）几乎直接相关（需要注意的是，这三者以某种方式相互关联）。三个一般领域是

- CPU
- I/O (disk writes and reads)
- Memory (excessive paging—related to disk I/O)

- CPU
- I/O（磁盘写入和读取）
- 内存（过度分页——与磁盘 I/O 相关）

Initially, these seem relatively simple. If it is the CPU, how can better load balancing be achieved? Perhaps with another CPU or faster chipset? If it is excessive paging, the answer may be more memory or a change in how swapping is done. If it is I/O, a change in how disks are arranged and formatted may be required. What if it is a specific user or process that is causing performance issues? How do you ascertain whether an I/O problem is in the disks or swapping? Note the use of perhaps, maybe, and if in this paragraph thus far. That is how performance monitoring is—a great deal of “ifs” until the problem is eventually found and rectified.

最初，这些看起来相对简单。如果是 CPU，如何实现更好的负载均衡？也许需要另一个 CPU 或更快的芯片组？如果是过度分页，答案可能是增加内存或改变交换方式。如果是 I/O，可能需要改变磁盘的排列和格式化方式。如果是特定用户或进程导致性能问题怎么办？如何确定 I/O 问题出在磁盘还是交换上？请注意迄今为止本段中 perhaps、maybe 和 if 的使用。这就是性能监控的方式——在问题最终被找到并纠正之前，有大量“如果”。

## Specific Tuning Aspects and Questions

具体调优方面和问题

Well, it gets worse. Along with the aforementioned rudimentary questions you have to take into account when attacking a performance issue, there are a handful of more complex (yet succinctly related) questions that come into play as well.

好吧，情况更糟。除了在处理性能问题时必须考虑的上述基础问题外，还有一些更复杂（但简洁相关）的问题也会出现。

## What Is a Bottleneck?

什么是瓶颈？

Aside from the more obvious portion of a beer bottle, in system’s terms a bottleneck is anything that slows down the system to a point where it is readily apparent (or not so readily apparent).

除了啤酒瓶中更明显的部位外，在系统术语中，瓶颈是指任何使系统减慢到明显（或不那么明显）程度的东西。

A readily apparent bottleneck might be something like users saying they listed a directory and it took two minutes to list ten entries.

一个明显的瓶颈可能是用户说他们列出了一个目录，花了两分钟才列出十个条目。

A not so readily apparent bottleneck (or as I like to call them, “creeping death”) are those that are potential bottlenecks. A case in point might be the gradual increase of use on an ftp server. Although it is still running fast now, after a certain point in time it will become quite apparent that it is too slow.

一个不那么明显的瓶颈（或我喜欢称之为“creeping death”）是那些潜在的瓶颈。一个例子可能是 ftp 服务器使用量的逐渐增加。虽然它现在运行仍然很快，但在某个时间点之后，很明显它会变得太慢。

## Frequency of Bottlenecks

瓶颈频率

How often does a particular bottleneck occur? This is a very big question that pertains mostly to user inquiries. More often than not, you may discover later that there was no cause for alarm because the user was doing something that was not routine or that was a one-time, isolated incident. Some good examples of this are when a user improperly invokes a command or application, when a user is trying a new way of performing some task, or when a user is trying something completely new. This can happen a great deal in very progressive environments where change is the norm. Such an environment, for example, is one in which new systems and methods are being developed and brought online rapidly. Sometimes, users may not even be aware of them until they start wondering why a job is taking so long.

特定瓶颈发生的频率如何？这是一个非常重要的问题，主要涉及用户询问。很多时候，你后来可能会发现没有引起警报的原因，因为用户做的事情不常规或是一次性、孤立的事件。一些很好的例子是用户错误调用命令或应用程序时，用户尝试以新的方式执行某项任务时，或用户尝试完全新事物时。在变化是常态的非常进步的环境中，这可能会经常发生。例如，这样的环境是新系统和方法被快速开发并上线。有时，用户可能甚至不知道它们，直到他们开始想知道为什么一个作业花费这么长时间。

## Bottleneck Location

瓶颈位置

Where exactly is the bottleneck occurring? This will be examined later in this chapter in the section “Performance Measurement Techniques,” but it is worth glancing at now. Is the bottleneck staring at you right now? If so, you may want to investigate it as soon as possible. Prolonged, easily identifiable bottlenecks should at least be made known so that users and/or managers might better understand that there is a problem, that you know what it is, and that you will identify a recourse. Sometimes bottlenecks can mask other bottlenecks or are a result of another bottleneck. Figuring which is happening can be puzzling, especially when you consider it can be only one of three general areas. Where this is seen most often is between paging and disk I/O.

瓶颈到底发生在什么地方？这将在本章“性能测量技术”部分后面进行探讨，但现在值得一看。瓶颈现在正盯着你吗？如果是这样，你可能希望尽快调查它。持续的、易于识别的瓶颈至少应该被告知，以便用户和/或管理人员更好地理解存在问题，你知道问题是什么，并且你将确定补救措施。有时瓶颈会掩盖其他瓶颈或是由另一个瓶颈导致。弄清楚哪种情况正在发生可能会令人困惑，尤其是考虑到它只能是三个一般领域之一时。最常看到这种情况的地方是在分页和磁盘 I/O 之间。

## Bottleneck Duration

瓶颈持续时间

Is the bottleneck sustained? This is a very important and often overlooked factor about performance—a “take it with a grain of salt” issue. When a user complains that the system is sluggish or perhaps you look at a quick snapshot of the CPU and notice high usage, how long does it really last? Is it long enough to become apparent to other users? A prime example of this might be a user compiling a program. Of course, to the user and even to the system it will appear to be very resource-intensive—but how long does it take to finish and what sort of system-level impact is it having?

瓶颈是否持续？这是关于性能的一个非常重要且经常被忽视的因素——一个“要持保留态度”的问题。当用户抱怨系统缓慢或你查看 CPU 的快速快照并注意到高使用率时，它到底持续多久？它持续时间足够长以至于对其他用户变得明显吗？一个典型的例子可能是用户编译程序。当然，对用户甚至对系统来说，它看起来会非常消耗资源——但完成需要多长时间，以及它对系统级有什么影响？
