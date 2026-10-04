# 指令清单19.15 Optimizing Keil 6/2013 (ARM mode)

```
02 OC C0 E3    BIC    R0, R0, #00200
01 09 80 E3    ORR    R0, R0, #04000
1E FF 2F E1    BX     LR
```

BIC是递减类的“反码）逻辑与”将第一个操作数与第二个操作数的反码（非求运算的结果，进行逻辑与比）x86指令集“逻辑与”与指令多作了一次非运算，ORR是“逻辑或指令”，与x86“逻辑或”的作用相同。

# 19.2.3 ARM + Optimizing Keil 6/2013 (Thumb mode)

# 指令清单19.16 Optimizing Keil 6/2013 (Thumb mode)

```
01 21 89 03    MOVS   R1, #04000
08 43ORRS    ORR    R1
49 11ASRS    ASRS   R1, #5      ; generate 0x20 and place to R1
88 43BICS    BICS   R0, R1
70 47             BX     LR
```

编译器借用了算术右移指令，BL 0x4000>>5生成0x20。与直接对寄存器进行立即数数值（0x200）比较，这种算术指令的opcode比较较短。

所以，后面的ASRS（算术右移）指令通过计算0x4000>>5得到0x20。

# 19.2.4 ARM + Optimizing Xcode (LLVM) + ARM mode

# 指令清单19.17 Optimizing Xcode 4.6.3 (LLVM) (ARM mode)

```
42 OC C0 E3    BIC    R0, R0, #04200
01 09 80 E3    ORR    R0, R0, #04000
1E FF 2F E1    BX     LR
```

这段代码由LLVM优化后的。原始代码大应该是：

```
REMOVE_BIT (rt, 0x4200);
SET_BIT (rt, 0x4000);
```

它确实完成所需功能。但是哪来的0x4200？或许，LLVM优化功能对原有指令进行了再加工，或许这是为了负得的。总之这段代码没有质量问题。

有时候编译器确实会做这种类型的代码处理，详细情况请参见第91章。

使用Xcode 4.6.3进行优化编译而生成的代码也非常相似，本文将不再介绍。