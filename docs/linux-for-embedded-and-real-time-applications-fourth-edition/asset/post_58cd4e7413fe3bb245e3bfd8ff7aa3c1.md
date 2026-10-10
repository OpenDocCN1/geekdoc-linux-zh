
## Chapter Outline

- Hard versus Soft Real-Time
- Why Linux is Not Real-Time
- Measuring Latency: Cyclctest
- Improving Linux Latency
- Two Approaches
- Preemption Improvement
- Interrupt Abstraction
- A Third Way: Xenomai
- Working With PREEMPT_RT
- Wrap Up
- Resources

> You can put racing stripes on a bulldozer but it won’t go any faster.
> Victor Yodaiten

We briefly reviewed the concept of real-time programming in Chapter 1, The embedded and real-time space. Let me repeat the quote I included there:

> A real-time system is one in which the correctness of the computations not only depends upon the logical correctness of the computation but also upon the time at which the result is produced. If the timing constraints of the system are not met, system failure is said to have occurred.
> Donald Gillies in the Real-time Computing FAQ

To put it another way, a late answer is a wrong answer. And remember, real-time does not necessarily mean real fast. It means fast enough, but more importantly, reliably fast enough. In practice, this means we can establish an upper bound on the time it takes the system to respond to an event. This is called latency.

### Hard versus Soft Real-Time

Real-time systems can be classified as either hard real-time or soft real-time. The primary difference between them is the consequences of missing a scheduling deadline. In hard real-time, the scheduling deadline must be met every single time. Missing the deadline means the system has failed, possibly with catastrophic consequences.

A good example of hard real-time is a fly-by-wire flight control system where a computer intervenes between the pilot and the engine and control surfaces. The control algorithm depends on precisely timed samples of airspeed, altitude, rate of climb or descent, and so on. If these samples are late, the algorithm can become unstable and the plane crashes.

Soft real-time can tolerate missing a deadline occasionally, if an average latency is maintained. The scheduling deadline is more of a goal than an absolute. A good example of soft real-time is the network of automated teller machines. “Come on,” I hear you say, “the ATM network isn’t real-time.” Oh yes it is, because when you put your card in that machine, you expect a response within a few seconds. So the designers of the ATM network have set a goal of responding in, say, 5 seconds. But they are not going to get terribly upset if occasionally it takes a few seconds longer. After all, what’s the worst that can happen? You get annoyed.

### Why Linux is Not Real-Time

Linux was conceived and built as a general-purpose multiuser operating system in the model of Unix. The goals of a multiuser system are generally in conflict with the goals of real-time operation. General purpose operating systems are tuned to maximize average throughput even at the expense of latency, while real-time operating systems attempt to minimize, and place an upper bound on, latency, sometimes at the expense of average throughput.

There are several reasons why standard Linux is not considered suitable for real-time use:

- “Coarse-grained Synchronization”: This is a fancy way of saying that kernel system calls are not preemptible. Once a process enters the kernel, it cannot be preempted until it is ready to exit the kernel. Actually, this is no longer the case. Much kernel code is now preemptible, and preemption is a kernel configuration option.
- Paging: The process of swapping pages in and out of virtual memory is, for all practical purposes, unbounded. We have no way of knowing how long it will take to get a page off of a disk drive, and so we simply cannot place an upper bound on the time a process may be delayed due to a page fault.
- “Fairness” in Scheduling: Reflecting its Unix heritage as a multiuser time-sharing system, the conventional Linux scheduler does its best to be fair to all processes. Thus, the scheduler may give the processor to a low priority process that has been waiting a long time, even though a higher priority process is ready to run. It should be noted, though, that the scheduler has improved substantially over the years to the point where standard Linux could be considered soft real-time.
- Request Reordering: Linux reorders I/O requests from multiple processes to make more efficient use of hardware. For example, hard disk block reads from a lower priority process may be given precedence over read requests from a higher priority process in order to minimize disk head movement or improve the chances of error recovery.
- “Batching”: Linux will batch operations to make more efficient use of resources. For example, instead of freeing one page at a time when memory gets tight, Linux will run through the list of pages, clearing out as many as possible, delaying the execution of all processes.

Years ago the consequences of these issues in using Linux, or even Windows on a PC, were noticeable. Back in the day, moving the mouse while executing a compute-intensive function like rendering a complex graphics image would cause the mouse to occasionally stop and then jump, because the compute- or I/O-bound process had the CPU locked up. With today’s high speed, multicore processors coupled with the vastly improved Linux scheduler, this is not nearly as noticeable.

The net effect of all these characteristics is that we cannot put an upper bound on the latency that a user task or process may encounter. By definition this is not real-time.

### Measuring Latency: Cyclctest

There is a tool called `cyclictest` that measures latency. The basic operation of cyclictest is relatively trivial, as shown in Listing 17.1. The program sleeps for some interval and when it wakes up, it gets the actual time and computes the difference, or latency, from what the time should be. It reports minimum, “actual,” average, and maximum latency.

```
clock_gettime(&now)
next = now + interval

while (!shutdown)
{
    clock_nanosleep(&next);
    clock_gettime(&now);
    diff = calcdiff (now, next);
    # update stat-> min, max, total latency, cycles
    # update the histogram data
    next += interval;
}
```

Listing 17.1 Cyclctest algorithm.

The `cyclictest` binary is hard to find, so you will have to build it from sources. Follow these steps:

```
git clone git://git.kernel.org/pub/scm/linux/kernel/git/cirkh/lms/rt-tests.git
cd rt-tests
make NUMA=0
su
./cyclictest -S
```

By default, `cyclictest` requires a package called `libnuma-dev`, where NUMA stands for Non-Uniform Memory Access. Most PCs do not implement NUMA, and so do not need the library otherwise. `NUMA=0` allows `cyclictest` to build without it.

The default behavior of `cyclictest` is to run one thread on each processor core at the lowest priority. Here is the result I get on my dual-core laptop where only one processor is dedicated to my Linux VM running CentOS 7 (kernel version 3.10.0-327.el7.x86_64):

```
# /dev/cpu_dma_latency set to 0us
policy:/other:/other: loadavg: 0.24 0.06 0.2/316 6204
T: 0 ( 6204) P: 0 I: 1000 C: 10948 Min: 11 Act: 625 Avg: 304 Max: 18988
```

Latencies are reported in microseconds, so my system reported a minimum latency of 11 microseconds, average of 304, and a maximum of almost 19 milliseconds.

Of course, the system is fairly lightly loaded right now. We can introduce an artificial load. Under `samples/src` is a directory `load50/`. Have a look at the file `load50.c`. This is a trivial program that forks off 50 processes that just spin. The number of processes forked is an argument to the program with a default value of 50.

Make the `load50` program, start `cyclictest` in one shell window, then run `load50` in another shell. You should see the maximum latency go up dramatically. On my system with a load of 20, the maximum went up to 3.5 seconds. I'm not sure I believe that. There may be a problem with the program.

### Improving Linux Latency

There are some things we can do to improve the latency of standard Linux. Specifically, we can change the kernel's “scheduling policy” and process priority for cyclictest, and we can lock the process's memory image into RAM so it won't be paged out.

The default scheduling policy, called `SCHED_OTHER`, uses a fairness algorithm and gives all processes using this policy priority 0, the lowest priority. This is fine for “normal” processes. The alternate scheduling policies are `SCHED_FIFO`, and `SCHED_RR`. These are intended for time-critical processes requiring lower latency. Processes using these alternate
