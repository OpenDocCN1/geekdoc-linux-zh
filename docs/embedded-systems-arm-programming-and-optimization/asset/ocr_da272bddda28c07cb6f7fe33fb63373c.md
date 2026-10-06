# 2.9 Optimization #2: Reducing CPI 85

```
asm ("fmacs s3, s9, s2\n\t" : : "s3");
asm ("fmacs s4, s9, s3\n\t" : : "s4");
asm ("fmacs s5, s9, s4\n\t" : : "s5");
asm ("fmacs s6, s9, s5\n\t" : : "s6");
asm ("fmacs s7, s6\n\t" : : "s7");
asm ("fsts s7,[mem]\n\t" : : [mem]="m (d[i++])",
```

Before each, each line of code has a dependency. Our objective is to construct a software pipeline with nine stages, corresponding to each instruction after the load-multiply. The prolog will begin by executing all but the last instruction for iteration 0, leaving s7 with the final value to store into the d array. Then it will execute all the last instructions, leaving register s6 with its value for iteration 2, and so on.

In order to implement the double buffer technique (in which a set of eight registers will turns holding the raw coefficients and the running sum of the polynomial value), unroll the loop by 2 as the previous implementation.

Load from one value of the x array each iteration of the outer loop. However, since the software pipeline is executing all seven fmac instructions in the same body, it is necessary to maintain seven different values from the x array at all times. To do this use registers s9-s15. These values must be shifted with respect to the fmac instructions on every iteration of the outer loop. Our main loop will perform two unrolled bodies of the original outer loop, perform this shift by changing the code.

After this, use the fcopy instruction to rearrange the values appropriately. fcopy copies the contents of a register between two floating-point registers. Its latency is four.

```
for (i=0;i<N/4;i+=2) {
    asm ("fsts s7,[mem]\n\t" : : [mem]="m (d[i])");
    asm ("fmacs s23, s10, s6\n\t" : : "s23");
    asm ("fmacs s22, s11, s5\n\t" : : "s22");
    asm ("fmacs s21, s12, s4\n\t" : : "s21");
    asm ("fmacs s20, s13, s3\n\t" : : "s20");
    asm ("fmacs s19, s14, s2\n\t" : : "s19");
    asm ("fmacs s18, s15, s1\n\t" : : "s18");
}
```