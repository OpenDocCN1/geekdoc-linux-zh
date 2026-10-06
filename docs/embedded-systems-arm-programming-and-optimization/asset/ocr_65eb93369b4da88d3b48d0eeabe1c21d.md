# 92 CHAPTER 2 Multicore and Data-Level Optimization: OpenMP and SIMD

| Table 2.3 Performance Improvement from Software Pipelining Versus Double Buffering |
| | Raspberry Pi | Xilinx Zedboard | NVIDIA Jetson Tegra TK1 |
| | ARM11 | Dual Cortex A9 | Quad Cortex A15 |
| Throughput/efficiency | 2.34 speedup <br>44.4% efficiency | 2.71 speedup <br>44.3% efficiency | 1.62 speedup <br>51.3% efficiency |
| CPI | 1.75 speedup | 2.08 speedup | 1.35 speedup |
| Cache miss rate | 0.91 speedup (slow) | 0.60 speedup (slow) | 0.77 speedup (slow) |
| Instructions per flop | 1.34 speedup | 1.30 speedup | 1.19 speedup |

# 2.10 OPTIMIZATION #3: MULTIPLE FLOPS PER SINGLE INSTRUCTION, MULTIPLE DATA

Nearly all modern processors have the ability to perform multiple independent operations using one instruction. These are called Single Instruction, Multiple Data (SIMD) instructions or vector instructions. SIMD instructions decrease the number of instructions per operation, which increases floating point throughput and decreases cache miss rate.

Some processors, such as the ARM Cortex A9 and A15, provide the ability to issue a SIMD instruction in less than an equivalent number of scalar instructions. These processors have multiple SIMD lanes, in which there are a register file that provide simultaneous access to all the necessary input and output registers. In this case, using SIMD instructions allows multiple operations in a single clock cycle compared to using scalar instructions.

Other processors, such as the ARM11, provide SIMD instructions but they require the same number of cycles to issue as scalar instructions. In other words, it requires n cycles to issue an n-way SIMD instruction, while would also take n cycles to issue n regular one-way instructions. While it may seem that, in this case, using SIMD instructions is pointless, these instructions can still provide benefits by providing for less code size and potentially reducing cache misses, but more importantly hiding the latency required by a dependent chain without SIMD instructions. For example, consider the following loop:

```
for (i=0; i<n; i++) {
fmacs s0, s1, s2 // assume $sl is loop-invariant
fmacs s2, s1, s0 // $s0 depends on the result of
 // the previous instruction

...}
```