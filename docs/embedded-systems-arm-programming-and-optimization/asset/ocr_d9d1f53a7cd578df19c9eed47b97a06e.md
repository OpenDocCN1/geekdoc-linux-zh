# 100 CHAPTER 2 Multicore and Data-Level Optimization: OpenMP and SIMD

| Table 2.5 Performance Improvement from NEON SIMD Instructions Versus Software Pipelining |
| Platform | Xilinx Zedboard | NVIDIA Jetson Tegra TK1 |
| CPU | Dual Cortex A9 | Quad Cortex A15 |
| Throughput/efficiency | 1.05 speedup | 1.13 speedup |
| | 45.7% efficiency | 60.0% efficiency |
| CPI | 0.48 speedup (slowdown) | 0.48 speedup (slowdown) |
| Cache miss rate | 0.45 speedup (slowdown) | 0.45 speedup (slowdown) |
| Instructions per flop | 1.30 speedup | 2.36 speedup |

```
```
[x_addr]m"x(x[i]).[next]m"x(i+16]).
[d_addr]m"d(d[i]),[coeff_addr]r"r(coeff_4vector):
"ro0","r1","r2","r3","q1","q2","q3";
```
```

Table 2.5 shows the Cortex A9 and Cortex A15 performance results for the NEON implementation relative to the software pipelined implementation. The data dependencies in the sequence of SIMD NEON instructions stalls that cannot be fully hidden by reordering instructions causes an increase in CPI. Despite this, the reduction in instructions per flop makes up for this loss and allow for a small improvement.

# 2.10.3 NEON intrinsics

Unlike VFP vector instructions, the programmer can use SIMD NEON instructions without using inline assembly language. The header neon.h provides a set of preprocessor wrappers around built-in compiler expressions that allow for the programmer to use C-style semantics to invoke specific NEON instructions. These are called intrinsics.

Intrinsics allow the programmer to use a C-style function to "invoke" a single instruction, meaning that the compiler is forced to use a specific instruction corresponding to the intrinsic. Like inline assembly, intrinsic calls often must generate additional instructions in order to allocate C variables, arrays, and pointers into registers.

An intrinsic version of the code from above is shown below. It achieves roughly the same performance as the inline assembly version of the kernel is much easier to write and requires no inline assembly language.