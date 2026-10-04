; now result in DO

ARM64处理器的FPU指令集，能够通过FPSCR直接设置APSR。至少，在
链上FPU不再独立于主处理器。此处的CMPE指令负责比较D0和D1寄存器中的
值（即数据的的第一、第二参数），并根据比较结果设置相应的APSR标记位
(N、Z、V)。

FGSEL (Floating Conditional Select) 首先判断条件GT(Greater
Than)是否成立，成立后会选择性复制D0或D1的D0寄存器。需要强调的
是，在进行条件判断的时候，这个指令依据APSR寄存器的标识，而非FPSCR
里的标识进行判断。相比早期的CPU而言，ARM64平台的这种“可直接访问
APSR”的特性是一种优势。

如果条件表达式(GT)为真，那么DO将复制D0的值（即不发生变
化)。如果该条件表达式不成立，则将复制D1寄存器的值。

# Non-optimizing GCC (Liner) 4.9

```
d_max:
    ; insert input arguments in "Register Save Area"
    sub     sp, sp, #16
    str     d0, [sp,8]
    str     d1, [sp]
    ; reload_values
    ldr     x1, [sp,8]
    ldr     x0, [sp]
    fmov    d0, x1
    fmov    d1, x0
    ; D0 - a, D1 - b
    cmpe   d0, d1
    ble     .L76
    ; a>b load D0 (a) into X0
    ldr     x0, [sp,8]
    b       .L74
.L76:
    ; a<=b load D1 (b) into X0
    ldr     x0, [sp]
.L74:
    ; result in X0
    fmov    d0, x0
    ; result in DO
    add     sp, sp, 16
    ret
```

在关闭优化编译之后，编译出来的程序庞大。首先，函数把输入
参数存储到局部寄存器（Register Save Area）。接着把这些值复制到X0/X1
寄存器，再将它们复制到D0/D1、使用CMPE进行比较。虽然这种程序的效