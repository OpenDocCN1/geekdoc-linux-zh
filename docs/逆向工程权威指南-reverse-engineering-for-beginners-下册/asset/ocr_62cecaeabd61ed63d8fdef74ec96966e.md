...

```
.text:C019F68 TST R6, #040 ; jumpable C019F00 default
case:
.text:C019F6C BNE loc_C01A128
.text:C019F70 LDR R2, [R4,#0x10]
.text:C019F74 ADD R12, #8
.text:C019F78 LDR R3, [R4,#0xC]
.text:C019F7C MOV R0, R4
.text:C019F80 STR R12, [R11,#var_50]
.text:C019F84 LDRB R3, [R2,R3]
.text:C019F88 MOV R2, R8
.text:C019F8C CMP R3, #0
.text:C019F90 ORNE R1, #1
.text:C019F94 STNE R1, [R4,#0x24]
.text:C019F98 ANDS R3, #6, #0x200000
.text:C019F9C MOV R1, R12
.text:C019FA00 LDR R3, [R4,#0x24]
.text:C019FA04 ANDNE R3, #1
.text:C019FA08 ERNE STR R3, [R11,#var_54]
.text:C019FB00 SUB R3, R11,#var_38
.text:C019FB04 BL lookup_fast
.text:C016A128 loc_C016A128 ; CODE XREF
do_last.isra.14+DC
.text:C016A128 MOV R0, R4
.text:C016A12C BL complete_walk
```

TEST指令的功能与x86平台的TEST指令相同。

显而易见，程序在某一条条件下调用lookup_fast() 函数，而在另一个条件下调用complete_walk() 函数。这种行为do_last()函数的源代码。

这里的汇编宏0_CREATE等于0x40。

# 19.2 设置 / 清除特定

本节将围绕这个程序进行讨论：

```
#include <stdio.h>

#define IS_SET(flag, bit) ((flag) & (bit))
#define SET_BIT(var, bit) ((var) |= (bit))
#define REMOVE_BIT(var, bit) ((var) &= ~(bit))

int f(int a) {
    int rt=a;
    SET_BIT(rt, 0x4000);
```