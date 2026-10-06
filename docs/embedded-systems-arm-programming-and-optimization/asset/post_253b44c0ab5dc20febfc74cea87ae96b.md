
## 1.8 Code Optimization Objectives 27

For example, the following sequence of instructions performs a sequence of two dependent double-precision add instructions, because the second instruction cannot begin execution until the value of d0 is computed by the first instruction.

```
1 faddd d0,d2,d4
2 faddd d4,d0,d2
```

In this case, the second instruction cannot enter the execute pipeline until the completion of the first instruction completes. The time between the first instruction and the initiation of the second instruction is spent executing stalls. Most floating-point programs contain many of these types of dependencies leading to data dependency stalls and resulting in low utilization of the floating-point functional units.

Reducing the number of stalls is generally accomplished by rearranging the order of instructions in the code, allowing the latency of floating-point instructions to be "hidden" by executing other, non-dependent floating-point instructions in the meantime.

Processors that perform aggressive dynamic scheduling—also called out-of-order execution—can do this automatically at runtime without needing to change the program code. However, most embedded processors, including those from ARM, cannot afford the cost of this, in terms of chip reality or power consumption, so they have limited or no capability for dynamic scheduling.

Chapter 2 describes how to use optimization techniques to hide the latency of floating-point instructions and reduce the number of data dependencies using double buffering, software pipelining, and SIMD instructions.

Another way to reduce the effect of floating-point latency is to convert floating-point instructions into fixed-point instructions. Fixed-point representation allows the usage of fractional numbers using the lower-latency functional units. The main drawback of this approach is a reduction in the dynamic range, or the ratio between the largest- and smaller-magnitude numerical values that can be represented. Luckily, many graph Chapter 2 explores this technique as well.

Load and store stalls are linked to the effectiveness of the processor’s cache, but can be reduced by changing the order in which data is accessed in memory. The goal is to increase the locality of the accesses. To do this, the programmer or compiler must arrange the order of load and store instructions such as the resulting sequence of effective addresses is favorable for the cache. This means that whenever the same nearby addresses are accessed, the time between accesses should be minimized. This often requires substantial changes to the structure of nested loops.

The primary method for accomplishing this is through loop transformations, such as loop interchange, loop fusion, loop tiling. In order to track load and store stalls, the programmer must be able to monitor the number of references and misses on the last-level cache.

This chapter describes the performance counters to keep track of cycles, instructions, cache references, and cache misses. The cycle will provide information about execution time, the ratio of instructions to cycles will provide CPL, and the ratio of cache misses to references will provide cache miss rate. Note that the total CPI includes the stall cycles from branches, data dependencies, and cache misses, although there is no way to discriminate each type of stall. There is enough information to make optimization decisions, and understand how code transformations perform.

On a final note: the ARM11 and ARM Cortex-A9 PMUs can count dependency stalls, but this event is no longer supported (countable) in the Cortex A15 PMU. In order to remain consistent across all our target processors, this chapter will not use this particular counter.

## 1.9 RUNTIME PROFILING WITH PERFORMANCE COUNTERS

Most modern processors contain a set of registers called performance counters that can be programmed to count specific events that may be of interest for understanding program performance or diagnosing problems. The most commonly used performance counter is the cycle counter, which is a simple counter that increments every cycle. The cycle counter can be used to provide timing information at the granularity of a single clock cycle.

### 1.9.1 ARM performance monitoring unit

In addition to a cycle counter, most processors also offer a set of flexible counters that can be programmed to count events such as cache misses, instruction executions, floating-point instruction executions, or branch mispredictions. These counters, as well as the associated logic used to program each counter with a specific event, are called the performance monitoring unit (PMU).

## 1.9 Runtime Profiling with Performance Counters 29

The performance counters are a limited hardware resource that must be shared by all programs and users, so the OS must be responsible for arbitrating access to the counters. In addition, a user may want to count more events than there are physical counters, for multiplexing access to the counters. Also, multic processors will often have a PMU in each core, so inconsistent results may arise when a program inadvertently reaches the counters of different cores. As such, the OS must be responsible for maintaining per-process counter states across all cores. This also includes not incrementing the per-process counters during the times when the process is suspended by the OS, despite the fact that the hardware counters would still be counting.

For these reasons, the OS must manage the PMU on behalf of the users. In fact, the processor will actually use user code from directly accessing the counters (registering as an invalid instruction exception). Users are forced to access the PMU through the OS using system calls.

### 1.9.2 Linux Perf-Event

Linux provides an abstraction layer for PMU management called perf_event. In addition to interfacing with the PMU, perf_event is also capable of keeping track of software events such as context switches and page faults. Unfortunately, as of this writing, perf_event is not fully implemented for the ARM11 processor of the Raspberry Pi. Appendix A describes how to patch the kernel to add support.

When more counters are requested than physically available, perf_event uses a technique called multiplexing. In this case, the kernel enables a subset of the requested counters, enabling a subset at regular intervals. This allows the hardware counters to statistically sample the time the user requests the counters to be enabled. When the user requests, perf_event will report the number of cycles the user enabled the counter and the number of cycles the counter was actually enabled. These values are called time enabled and time running. The user can extrapolate the actual count by scaling the reported count by the ratio of these values.

In order to use perf_event, the user instantiates each counter using the system call named perf_event_open. One can use the standard Posixioctl() function to enable, disable, and reset it, and the read() function to read its state.

When opening a counter, the user must fill in a "struct perf_event_attr" structure to configure the counter. The two most important fields of this structure are the .type field and .config field. When counting hardware

## 1.9.3 Performance counter infrastructure

events, there are only two valid types: PERF_TYPE_HARDWARE and PERF_TYPE_RAW. PERF_TYPE_HARDWARE is a platform-independent mechanism for specifying a set of common events, while PERF_TYPE_RAW allows you to specify a processor-specific encoding to count.

In order to use perf_event, it is easy to develop a set of reusable functions to measure the performance of various aspects of program execution. This will include functions for initialization, result printing, resetting the counters (named "tick"), and reading the state of the performance counters named "tick".

Begin by adding the necessary header files and constant definitions of our five counters:

```c
#include <stdio.h> // needed for printf()
#include <stdlib.h> // needed for malloc() and RAND_MAX
#include <string.h> // needed for memset()
#include <math.h> // needed for floating point 
#include <sys/time.h> // needed for gettimeofday()
#include <unistd.h> // needed for pid_t type
#include <sys/ioctl.h> // needed for ioctl()
#include <asm/unistd.h> // needed for perf_event 
syscall
#include <linux/perf_event.h> // needed for perf_event
#define CYCLES 0
#define INSTRUCTIONS 1
#define CACHEREFS 2
#define CACHEMISSES 3
```

Next, write an explicit C wrapper to invoke the system call to open a specific performance counter using perf_event:

```c
long perf_event_open(struct perf_event_attr *hw_event,
pid_t pid,
int cpu.
```
