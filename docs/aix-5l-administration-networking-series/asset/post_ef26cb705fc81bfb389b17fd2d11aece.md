
## 4. Process and Thread Properties

| Process Properties | Thread Properties |
| :--- | :--- |
| pid | tid |
| ppid | Stack |
| uid | Scheduling policy |
| gid | Scheduling priority |
| cwd | Pending signals |
| Process environment | Blocked signals |
| Process statistics | Thread-specific data |
| Signal actions |  |
| File descriptors |  |

Exception. Asynchronous signals such as `kill(2)` are delivered to only one thread in a process. The signal will be delivered to a thread that has initiated a `sigwait(3)` for the particular signal number or to a thread that does not have it blocked. Disabling signals at the process level to protect a critical code section in a thread may not work as expected in that the signal may be delivered to a thread executing on another processor.

The AIX lock instrumentation is provided to maintain cache coherency between threads running on multiple processors. The lock state of the system can be queried using the `lockstat` command if this facility has been enabled by `bosboot` options. Since the AIX kernel is aware of its UP versus MP run mode status, MP-specific lock requests are ignored in a UP environment to shorten code paths. Application developers may then write software exclusively for MP environments that is nonetheless supported under UP configurations.

```bash
# bosboot -a -L  <---------- Create a boot image with MP lock support
# lockstat -a  <------ Display system lock usage statistics
```

## Scheduling and Dispatching

It's probably obvious by now that changes to the AIX scheduler were required to support threads. As the dispatchable units of work, threads are assigned a priority from 0 to 127. Each level is represented by a run queue. The scheduler periodically scans the run queues and recalculates priority in accordance with processor use history for those tasks not running at a fixed priority. Note that some functions such as `nice` that affect queue priority still operate on the process as a whole rather than an individual thread.

The AIX dispatcher had to be changed to facilitate the way in which threads are allocated to available processors. When a thread is bound to a processor, in what is termed processor affinity, the highest priority thread may not be the next one available to be dispatched. The system experiences fewer cache misses if a thread can be dispatched to the same processor on which it last ran. Conversely, overall processor utilization is improved if threads can be scheduled on any available processor. The AIX dispatcher implements what has been termed **opportunistic affinity**. An attempt will be made to run a thread on the same processor on which it last ran if that processor is available. The `bindprocessor()` routine is available for those instances when a programmer would like to enforce processor affinity for a code section.

```bash
# bindprocessor <proc-id> <processor> — Bind process to processor
```

The `bootinfo` command can be used in early AIX 4-to-AIX 5 systems to determine whether the platform is MP capable. Note that `bootinfo` is included but not supported starting with AIX version 4.2.

```bash
# bootinfo -z — Display MP capability for the current platform
```

Along with general thread support, three scheduling options are available. SCHED_RR, SCHED_FIFO, and SCHED_OTHER. The SCHED_RR enforces strict round-robin scheduling, SCHED_FIFO uses a fixed-priority, first-in, first-out ordering. SCHED_FIFO does not support preemption and is not timesliced. A thread must either block or yield the processor when running under the SCHED_FIFO scheduler. The third option, SCHED_OTHER, represents the standard AIX scheduling algorithm, where task priority degrades with CPU usage.

## Run Queues

Each CPU on the system has its own set of run queues in AIX 4.3.3 and higher. For AIX 5L, an additional set of global run queues has been added. With AIX version 4, the system has 128 run queues, specified as 0–127. On a SMP machine, each processor has its own set of run queues. Having a run queue on each processor makes it easier for the scheduler to find which thread to allow to run next. The scheduler scans the bit mask to determine which bit is set for a ready-to-run state on a single run queue as opposed to a huge global run queue.

With AIX 5L, the run queues have been increased from 127 run queues per processor to 255 run queues per processor. Additionally, AIX 5L has added a global run queue that can point fixed-priority threads to any processor on the system. To have all fixed-priority processes use the global run queue, you must use the `schedtune` command to set the GLOBAL attribute to 1 (one).

## CPU Timeslice for a Thread to Run

Since AIX 5L uses the SCHED_OTHER scheduling policy, the discussion will follow this path. Under this scheduling policy, a running thread can use the CPU for a full timeslice. By default, one timeslice is 10 ms. Not all threads get the opportunity for the full timeslice because an interrupt can cause the thread to be placed on the tail of the run queue. An interrupt can be caused by a clock interrupt, or it can arise from some other source such as disk I/O or network adapter traffic. The reason behind the thread interrupt is that interrupts always have priority over a running thread.

How a thread gets on the run queue is a complex algorithm that places a penalty on threads that have recently been running. The formula is recalculated every clock tick for the currently running thread:

```text
Priority Value = Base Priority + Nice Value + CPU Penalty Based on Recent CPU Usage
```

Where:
- Base Priority = 40 (PUSER)
- Nice Value = 20 (Default)

```text
CPU Penalty = CPU Usage * R (Where R is 0.5 by default)
```

The CPU usage for all processes is calculated once every second. The CPU penalty is calculated on every clock tick, 10 ms by default. When a thread just comes out of the CPU, it is penalized. Through all of these calculations, some work actually does get done. The threads that were penalized work their way back up to the front of the run queue and get more CPU time. The overall throughput is much higher with the SCHED_OTHER scheduling policy than with SCHED_RR or SCHED_FIFO.

## MORE ABOUT THE KERNEL

In this chapter, we cover the basics of the AIX 5L kernel. At the last AIX 5L and NUMA-Q conference in Atlanta, I went to an AIX 5L Kernel Internals presentation. The intensity of the discussion was at a very detailed level, and the handout was about 60 pages of eight-point type. There is a lot more to the kernel than was presented in this chapter. Please refer to the IBM Redbook Web site for details on specifics of the kernel. Here you can find some good Redpieces and white papers that go into great detail on various internal components of the AIX 5L kernel.

```text
http://www.redbooks.ibm.com
```

## CHECKLIST

The following is a checklist for the key points in the kernel:

- AIX 5L provides a scalable 64-bit kernel that can support very large application workloads executing on 64-bit hardware.
- The scalability of the 64-bit kernel is primarily due to the larger kernel address space.
- The AIX kernel is dynamically extensible, meaning that new device drivers and other system extensions can be added or changed on a running system without requiring a kernel rebuild or system reboot.
- A new device can be plugged into a running system and made immediately available for use by updating ODM information with the `cfgmgr` command.
- Any system activity requires a process to run to execute the activity. Each process on a running system consists of one or more threads. Threads provide the means of overlapping, multiplexing, and parallelizing operations within a process.
- Multiple threads allow the system to service requests from multiple user processes at the same time.
- The AIX lock instrumentation is provided to maintain cache coherency between threads running on multiple processors. The lock state of the system can be queried using the `lockstat` command if this facility has been enabled by `bosboot` options.
- Each CPU on the system has its own set of run queues in AIX 4.3.3 and higher. With AIX version 4, the system has 128 run queues per processor, specified as 0–127. AIX 5L has 255 run queues per processor.
- For AIX 5L, adds a set of global run queues that can point fixed-priority threads to any processor on the system.
