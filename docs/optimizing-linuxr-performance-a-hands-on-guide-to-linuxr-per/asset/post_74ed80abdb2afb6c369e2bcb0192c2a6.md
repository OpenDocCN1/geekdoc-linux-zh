
## 1.2. Outline of a Performance Investigation

This section outlines a series of essential steps as you begin a performance investigation. Because the ultimate goal is to fix the problem, the best idea is to research the problem before you even touch a performance tool. Following a particular protocol is an efficient way to solve your problem without wasting valuable time.

### 1.2.1. Finding a Metric, Baseline, and Target

The first step in a performance investigation is to determine the current performance and figure out how much it needs to be improved. If your system is underperforming, you may decide that it is worth the time to investigate. If the system is performing close to its peak values, it might not be an investigation. Figuring out the performance values allows you to set reasonable performance expectations and gives you a performance goal, so that you know when to stop optimizing. You can always tweak your system just a little, and with no performance target, you can waste a lot of time squeezing out that extra percent of performance, even though you may not need it.

### 1.2.1.1 Establish a Metric

To figure out you have finished, you must create or use an already established metric of your system's performance. For example, if you are optimizing a Web server, you would choose "serviced Web requests per second." If you do not have an objective to measure the performance, it can be nearly impossible to determine whether you are making any progress as you tune the system.

### 1.2.1.2 Establish a Baseline

After you figure out you are measuring the performance of a particular system or application, it is important to determine your current performance levels. Run the application and record its performance before any tuning or optimization; this is called the baseline value, and it is the starting point for the investigation.

### 1.2.1.3 Establish a Target

After you pick a metric and baseline for the performance, it is important to pick a target. This target guides you to the end of the performance hunt. You can indefinitely tweak a system, and you can always get it a little better with more and time. If you pick your target, you will know when have finished. Pick a reasonable goal, the following are starting points:

- *Find results with a similar configuration and ask for their performance measurements— This is an ideal situation. If you can find a similar system that performs better, not only will you be able to pick a target for your system, you may also be able to work with that person to determine your configuration is slower or how your configurations differ. Using another system as a reference can come immensely useful when investigating a problem.
- *Find results of industry standards benchmarks— Many Web sites compare benchmark results of various aspects systems. Some of the benchmarks can be achieved only with a heroic effort, so they might not represent realistic use. However, many benchmark systems have the configuration for particular results. These configurations can provide clues to help you tune the system.
- *Use hardware with a different OS or application— It may be possible to run a different application on your system with a similar function. For example, if you have two Web servers, and one performs slowly, try a different one to see if it performs better. Alternatively, try running the same application on a different operating system. If the system performs better in either of these cases, you know that your original configuration has room for improvement.

## 1.3. Chapter Summary

Hunting a performance problem should be a satisfying and exciting process. If you have a good method in place to research and analyze, it will be repaid back many times as you hunt the problem. First, determine whether other people have similar problems; if they, try their solutions. Be skeptical of what they tell you, but look for others with experience of a similar problem. Create a reasonable metric and target for your performance hunt; the metric enables you to know when you have finished. Automate performance tests. Be sure to save tests and configuration information when you generate them so that you can review the results later. Keep your results organized and record any research and other information that you find that relates to your problem. Finally, periodically review your notes to find information that you might have missed the first time. If you follow these guidelines, you will have a clear goal and a clear procedure to investigate the problem.

This chapter provided a basic background for a performance investigation, and the following chapters cover the Linux-specific performance tools themselves. You learn how to use the tools, what type of information they can provide, and how to use them in combination to find performance problems on a particular system.

## Chapter 2. Performance Tools: System CPU

This chapter outlines the system-wide Linux performance tools. These tools are your first line of defense when tracking a performance problem. They can show you how the overall system is performing and which areas are misbehaving. This chapter discusses the statistics that these tools can measure and how to use the individual tools to gather those statistics. After reading this chapter, you should

- Understand the basic metrics of system-wide performance, including CPU usage
- Understand which tools can retrieve these system-wide performance metrics

## 2.1. CPU Performance Statistics

Each system-wide Linux performance tool provides different ways to extract similar statistics. Although no tool displays all the statistics, some of the tools displays the same statistics. Rather than describe the meaning of the statistics multiple times (for each tool), we review them once before the tools are described.

### 2.1.1. Run Queue Statistics

In Linux, a process can be runnable or blocked waiting for an event to complete. A blocked process may be waiting for data from an I/O device or the results of a system call. If a process is runnable, means that it is competing for the CPU with the other processes that are also runnable. A runnable process is not necessarily using the CPU, but when the Linux scheduler is deciding which process to run, it picks from the list of runnable processes. When these processes are runnable, but by waiting to use the processor, they form a called run queue. The longer the queue, the more processes wait in line.

The performance tools commonly show the number of processes that are runnable and the number of processes are blocked waiting for I/O. Another common system statistic is that load average. The load on a system is the total amount of runnable and blocked process. For example, if two processes were running and three available to run, the system's load would be five. The load average is the amount of load over a given amount of time. Typically, the load average is over 1 minute, 5 minutes, and 15 minutes. This enables you to see how load changes over time.

### 2.1.2. Context Switches

Most modern processors can run only one process at a time. Some processors, such as hyperthreaded processors, can actually run more than one simultaneously,Linux treats them as multiple single-threaded processors. To create the illusion that a given process runs multiple tasks simultaneously, the Linux kernel constantly switches between different processes. The switch between processes is called a context switch, which it happens, the CPU saves all the context information from the old process and retrieves all the context information for the new process. The context contains a large amount of information that Linux tracks for each process, including, among others, which instruction pointer is, which memory it has allocated, and what files the process has open. These switching contexts can involve moving a large amount of information, and the context switch can be expensive. It is good to minimize the number of context switches if possible.

To avoid context switches, it is important to know how they happen. First, context switches can result from kernel scheduling. To guarantee that each process receives a fair share of processor time, the kernel periodically interrupts and, if appropriate, the scheduler decides to start another process rather than the current process every this periodic interrupt or occurs. It is possible that your system will interrupt per seconds per architecture and kernel timer. One way is to check how often the interrupt is to use /proc/interrupts to determine the number of interrupts that have occurred over an amount of time. This is demonstrated in Listing 2.1.

# Listing 2.1.

```
root@localhost asm-i386# cat /proc/interrupts | grep timer
; sleep 10 ; cat /proc/interrupts | grep timer
0: 24060643 X-TIMER timer
0: 24070993 X-TIMER timer
```

In Listing 2.1, we will ask the kernel to show how many times the timer has fired, with ten seconds, and