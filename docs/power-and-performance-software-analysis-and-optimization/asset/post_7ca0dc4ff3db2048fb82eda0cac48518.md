
## 6.2 Top-Down Hierarchical analysis 113

```
$D = IDQ\DSB\UOPS
I = INST\RETIRED.ANY
M = ICACHE\MISSES
S = IDQ\MISSES\UOPS
T = IDQ\MITE\UOPS
U = D + S + T
```

$\mu_{ops}$ from Decoded Iache $\frac{D}{I} \times 100$ (6.3a)
$\mu_{ops}$ from Legacy Decoder Pipeline $\frac{T}{U} \times 100$ (6.3b)
$\mu_{ops}$ from Microcode Sequencer $\frac{S}{U} \times 100$ (6.3c)
$% ICache Misses $\frac{M}{U} \times 100$ (6.3d)

FIGURE 6.3

Front Bound $\mu_{op}$ decomposition (Intel Corporation, 2014).

It may be enlightening to decompose the $\mu_{op}$ delivery by its source. Use Equations 6.3(a)-6.3(c) to determine the percentage of $\mu_{ops}$ delivered from the DSB, MITE, and Microcode Sequencer, respectively. The Microcode Sequencer is used to handle special instructions and situations, which the MITE is unable to handle, that is, it is a software fallback for functionality that isn't implemented in hardware. As a result, the Microcode Sequencer is capable of generating a large number of $\mu_{ops}$.

When interpreting these metrics, a low percentage of delivery from the Microcode Sequencer and a high percentage of delivery from the Decoded Iache is desirable. The Microcode Sequencer is required for delivering certain instructions, so what instructions is responsible, and to avoid them. Each microarchitecture has a series of hardware limitations for the Decoded Icache, so a low percentage of DSB delivery may indicate less than optimal code organization that is triggering one or more of these limitations.

Another metric to consider is the percentage of Icache misses, as shown in Equation 6.3(d). Even a small percentage of Icache misses can have serious repercussions for performance. Typically, Icache misses are the result of bloated code size or branch mispredictions. Common culprits for bloated code size include exclusive loop unrolling, function inlining, and other optimizations that attempt to trade code size for speed.

## CHAPTER 6 Introduction to Profiling

### 6.2.2 BACK END BOUND

After allocation of $\muop$ by the Front End, the Back End is responsible for executing the $\muop$ until it retires. The Back End metric represents the situations where the Front End was able to allocate the maximum number of $\muops$, but the Back End was unable to execute one or more. This is caused by stalls within the Back End that consume resources that would otherwise be needed for the $\muop$ to begin execution.

These types of stalls can be further divided into two categories. The first category, memory stalls, occur when the execution is waiting for a memory resource to become available. The second category, execution stalls, occurs due to issues within the execution pipeline.

The equations in Figure 6.4 provide the percentage of Back End stalls caused by each of these categories.

One of the longstanding challenges in quantifying the impact of memory accesses is accounting for out-of-order execution. This is because the execution pipeline may be able to mask memory latencies by scheduling $\muops$ until those memory resources are available. The CYCLE_ACTIVITY,STALLS_LDM_PENDING PMU event is designed to only count memory accesses whose latencies cannot be masked. This event was added in the Third Generation Core™ microarchitecture, so these newer, processors are capable of a more accurate memory analysis than the Second Generation Intel Core processor family.

Once these metrics identified what issues are contributing to the Back Bound category, another increase in detail is possible.

### Memory Bound

As the names imply, the Memory Bound category quantifies the percentage of cycles the execution pipeline is stalled waiting data loads. As a result of this stall, the maximum number of $\muops$ was able to be allocated. When the Back Bound

```
C = CPU_CLK_UNHALTED_THREAD
E = CYCLE_ACTIVITY,CYCLES NO_EXECUTE
S = CYCLE_ACTIVITY,STALLS_LDM_PENDING
U1 = UOPS_EXECUTED.THREAD:c1
U2 = UOPS_EXECUTED.THREAD:c2
```

```
% EXE = (E + U1 - U2) / C x 100 (6.4a)
% Memory Bound = (S / C) x 100 (6.4b)
% Core Bound = % EXE - % Memory Bound (6.4c)
```

FIGURE 6.4

Back End Bound $\muop$ decomposition (Intel Corporation, 2014).

## 6.2 Top-Down Hierarchical analysis 115

category represents a significant cause of pipeline stalls, and the Memory Bound category is flagged as the underlying cause for the Back End stalls, there are two optimizations available. The first is to correlate these events to a specific algorithm, or related data, and work to reduce that data structure's total memory consumption. The second is to reorganize the relevant data to better utilize the processor's cache. Cache misses can also be caused by the processor entering a deep sleep that power-gates the processor's caches. As a result, exiting this sleep state cache can be costly. Another for cache misses may be the operating system migrating the process to a different processor. Chapter 14 provides more information for optimizing for cache efficiency

Increasing the level of detail on the Memory Bound divides stalls by their level in the memory hierarchy. For more information on the memory hierarchy, Section 14.1. Figure 6.5 provides the equations for calculating the percentage of stalls at each level of the hierarchy.

Note that in Equations 6.5(c) and 6.5(d), the variables M and N are estimations that utilize the L3 latency ratio, variable W. This is required because there is no equivalent STALLS_L3_PENDING PMU for. The Third Generation Intel Core microarchitecture, the recommended value for W is 7 (Intel Corporation, 2014).

```
C = CPU_CLK_UNHALTED.THREAD
H = MEM_LOAD_UOPS_RETIRED.LLC_HIT
M = W x R / H + R
N = HnH + W x R
O = CYCLE_ACTIVITY_STALLS_L1D_PENDING
R = MEM_LOAD_UOPS_MISC_RETIRED.LLC_MISS
S = CYCLE_ACTIVITY_STALLS_LDM_PENDING
T = CYCLE_ACTIVITY_STALLS_L2_PENDING
W = L3 cache latency ratio
```

```
% L1 Bound = S - O / C × 100 (6.5a)
% L2 Bound = O - T / C × 100 (6.5b)
% L3 Bound = T x N / C × 100 (6.5c)
% Memory Bound = T x M / C × 100 (6.5d)
```

Figure 6.5 Memory Bound level decomposition

Memory Bound level decomposition (Intel Corporation, 2014).

## CHAPTER 6 Introduction to Profiling

A high percentage in the L2, L3, or Memory Bound categories suggests that cache isn't being utilized effectively. A high percentage in the L1 Bound category suggests that too many memory loads and stores are occurring.

### Core bound

The Core Bound category quantifies the percentage of cycles the execution pipeline is stalled. These stalls are often caused by μops within the pipeline taking a long time to retire, and tying up resources.

Figure 6.6 provides the formulas for determining what resources in the execution pipeline are overutilized.

Equation 6.6(a) calculates the total percentage of cycles where a Back End resource-utilization overlaps a μop from beginning to execution. If this percentage is significant, Equations 6.6(b)-6.6(f), will further decompose the resource stalls by individual execution resources. If any of these are significant, looking at the code to avoid overutilizing the associated resource.

Equations 6.6(c) and 6.6(b) represent the percentage of cycles where a load or store was ready to be allocated, all of the pipeline load or store buffers were already used, that the μop could not be allocated until one of the loads or stores completes. Equation 6.6(d) represents the percentage of cycles where a new branching μop could not be allocated because the Branch Order Buffer was.

```
A = RESOURCE_STALL.ANY
B = RESOURCE_STALL.BOB
C = CPU_CLK_UNHALTED_THREAD
L = RESOURCE_STALL.LB
O = RESOURCE_STALL.ROB
R = RESOURCE_STALL.RS
S = RESOURCE_STALL.SB
```

| Resource Stalls = A/S × 100 (6.6a) | Stalled Store μop = S/C × 100 (6.6b) | Stalled Load μop = L/C × 100 (6.6c) | Stalled Branch μop = B/C × 100 (6.6d) | Reservation Station Full = A/C × 100 (6.6e) | Reorder Buffer Full = O/C × 100 (6.6f) |

**Figure 6.6** Core Bound cycle decomposition (Intel Corporation, 2014).
