# CHAPTER 6 Introduction to Profiling

A high percentage in the L2, L3, or Memory Bound categories suggests that cache isn't being utilized effectively. A high percentage in the L1 Bound category suggests that too many memory loads and stores are occurring.

# Core bound

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