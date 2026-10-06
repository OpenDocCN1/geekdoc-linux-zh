# 84 CHAPTER 2 Multicore and Data-Level Optimization: OpenMP and SIMD

The new loop will have the following schedule:

| Instruction | Cycle |
|---|---|
| Store A[0] | 6 |
| Add A[1] | 7 |
| Load A[2] | 8 |
| Store A[1] | 10 |
| Add A[2] | 11 |
| Load A[3] | 12 |
| Store A[2] | 14 |
| ... | ... |

The processor will perform with the same CPI as the nonpipelined version of the code executing the prolog and epilog, the loop will begin in cycle 6, the same cycle A[0] was stored before. The loop’s II is now only four cycles, since no stalls are required within the loop and only one is required between iterations to separate each store-add dependency and load-add dependency. The code has achieved a loop speedup of 7/4 and the only cost was one additional.

# 2.9.2 Software pipelining Horner's method

Before pipeling our unrolled Horner’s method kernel, use the floating-point load multiple instruction (fldmias) to consolidate all the individual load instructions into one instruction.

The fldmias instruction loads multiple floating-point values from memory. The registers are listed in braces and may be separated by commas or specified using a hyphen. The registers must be continuously numbered. Note that this instruction requires that the registers be listed after the label, as opposed to the single load/store in which the register is listed first.

Using the fldmias instruction will load each coefficient into separate registers, unlike our original version that reused s0 and s2 when loading the coefficients.

```
asm "fldmias %[mem], [s0,s1,s2,s3,s4,s5,s6,s7]\n\t :"
"[mem]%(&coeff[0]) : "s0", "s1", "s2", "s3", "s4", "s5",
"s6", "s7"
asm "flds s9%%[mem]\n\t : [mem]m"*x([i]) : "s9"
asm "fmacs s1, s9, s0\n\t : : "s1"
asm "fmacs s2, s9, s1\n\t : : "s2";
```