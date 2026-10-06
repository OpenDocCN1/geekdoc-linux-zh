# 28 CHAPTER 1 The Linux/ARM Embedded Platform

such as the resulting sequence of effective addresses is favorable for the cache. This means that whenever the same nearby addresses are accessed, the time between accesses should be minimized. This often requires substantial changes to the structure of nested loops.

The primary method for accomplishing this is through loop transformations, such as loop interchange, loop fusion, loop tiling. In order to track load and store stalls, the programmer must be able to monitor the number of references and misses on the last-level cache.

This chapter describes the performance counters to keep track of cycles, instructions, cache references, and cache misses. The cycle will provide information about execution time, the ratio of instructions to cycles will provide CPL, and the ratio of cache misses to references will provide cache miss rate. Note that the total CPI includes the stall cycles from branches, data dependencies, and cache misses, although there is no way to discriminate each type of stall. There is enough information to make optimization decisions, and understand how code transformations perform.

On a final note: the ARM11 and ARM Cortex-A9 PMUs can count dependency stalls, but this event is no longer supported (countable) in the Cortex A15 PMU. In order to remain consistent across all our target processors, this chapter will not use this particular counter.

# 1.9 RUNTIME PROFILING WITH PERFORMANCE COUNTERS

Most modern processors contain a set of registers called performance counters that can be programmed to count specific events that may be of interest for understanding program performance or diagnosing problems. The most commonly used performance counter is the cycle counter, which is a simple counter that increments every cycle. The cycle counter can be used to provide timing information at the granularity of a single clock cycle.

# 1.9.1 ARM performance monitoring unit

In addition to a cycle counter, most processors also offer a set of flexible counters that can be programmed to count events such as cache misses, instruction executions, floating-point instruction executions, or branch mispredictions. These counters, as well as the associated logic used to program each counter with a specific event, are called the performance monitoring unit (PMU).