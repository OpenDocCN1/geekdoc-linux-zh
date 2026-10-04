5c:    3f800000    svccc    0x00800000

```
00000000 <main>:
0:    e92d4010    push    {r4, lr}
4:    e3a00000    mov     r0, #0
8:    ebfffffe    bl     0 <time>
c    ebffffff    bl     0 <main>
10:   e3a04064    mov     r4, #100      ; 0x64
14:   ebffffff    bl     38 <main+0x38>
18:   e59f01b8    ldr     r0, [pc,#24]  ; 38
<main+0x38>
1c:   eeb77ac0    vcct.f64.32    d7, s0
20:   ec532b17    vmov    r2, d7
24:   ebffffff    bl     0 <printf>
28:   e2544001    subs    r4, r4, #1
2c:   affffff8    bne     14 <main+0x14>
30:   e1a00000    mov     r0, r4
34:   eb8d8010    pop     {r4, pc}
38:   00000000    mov     r0, r0
```

float_rand() 函数地址地址5c的指令和main()函数地址38的指令都是随机噪声。

# 22.2 计算机精度

单精度浮点数的“机器精度/machine_epsilon”指的是相对误差的上限，即FPU操作的最小值。因此，浮点数的数据位越多，误差越小，精度越高。而单精度浮点类型的最高精度为2^-23=1.19e^-16，而双精度double类型的最高精度为2^-22=2.22e^-16。

所以计算某数值的机器精度是可能的。

```
#include <stdio.h>
#include <stdint.h>

union uint_float {
    uint32_t i;
    float f;
};

float calculate_machine_epsilon(float start)
{
    union uint_float v;
```