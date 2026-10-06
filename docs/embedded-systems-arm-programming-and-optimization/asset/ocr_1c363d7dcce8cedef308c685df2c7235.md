# 82 CHAPTER 2 Multicore and Data-Level Optimization: OpenMP and SIMD

| Instruction | Cycle |
|---|---|n| Load A[0] | 0 |
| Add A[0] | 3 |
| Store A[0] | 6 |
| Load A[1] | 7 |
| Add A[1] | 10 |
| Store A[1] | 13 |
| Load A[2] | 14 |
| Add A[2] | 17 |
| Store A[2] | 20 |
| ... |

In this case, the loop iteration interval (II), or number of cycles per iteration, is seven cycles, giving a CPI of 7/3. This means that four out of seven cycles is a stall.

Software pipelining is a method for interleaving loop iterations in order to separate the dependent instructions. To do this, unroll the loop three times and use different registers in each unrolled loop body:

+   1: For i = 0 to n–1 step 3[
2: r0 = load A[i]
3: r0 = r0 + C
4: A[i] = store r0
5: r1 = load A[i + 1]
6: r1 = r1 + C
7: A[i + 1] = store r1
8: r2 = load A[i + 2]
9: r2 = r2 + C
10: A[i + 2] = store r2

Now take the third instruction from iteration i (line 4), the second instruction from iteration i+1 (line 6), and the first instruction from iteration i+2 (line 8) and form a new loop:

+   1: For i = 0 to n-3[