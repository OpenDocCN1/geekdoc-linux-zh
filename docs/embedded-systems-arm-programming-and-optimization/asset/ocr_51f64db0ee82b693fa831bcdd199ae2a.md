# 2.9 Optimization #2: Reducing CPI 81

input in the following seven cycles will be stalled due to a data dependency. Likewise, the latency of loads instruction is four cycles (assuming a cache hit). The latency of the store instruction is system dependent.

Stalls can be avoided or the number of stalls can be reduced if the processor can identify and move other, nondependent instructions between dependencies. This technique is called dynamic out-of-order scheduling. Modern processors, including some embedded processors such as the ARM Cortex-A15, offer this feature.

Dynamic out-of-order scheduling introduces two additional types of dependencies, write-after-read and write-after-write, which the processor must resolve through the use of register renaming. Register renaming requires the addition of additional registers and additional datapaths to supply these registers. Also, dynamic scheduling relies on maintaining a buffer to hold a window of potential instructions as well as another buffer to keep track of all in-flight instructions and their original ordering (called the reorder buffer). These resources are limited, especially for embedded processors, and place constraints on the extent to which the processor can reorder instructions. As a result, any effort by the programmer or compiler to preprocess—or statically schedule—instructions in the program to separate dependent instructions could potentially improve performance, even for processors that support dynamic scheduling. One way to do this is through software pipelining, in which a loop is transformed in a way that its body is comprised of instructions from different loop iterations. This does not remove dependencies, but it separates dependent instructions. This often comes at the cost of additional registers for holding intermediate registers

# 2.9.1 Software pipelining

Consider the following loop:

```
1: For i = 0 to n-1[
2: r0 = load A[i]
3: r0 = r0 + C
4: A[i] = store r0]
```

In this case, there are RAW dependencies between each pair of instructions in the loop body. Assume the latency of load and add is three cycles. This would give the following instruction schedule, assuming a single-issue, in-order processor: