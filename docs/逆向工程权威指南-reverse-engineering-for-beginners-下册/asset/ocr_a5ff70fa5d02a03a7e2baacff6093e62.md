ARM系统用寄存器组合R0-R1返回64位值。其中，返回值的高32位存储在R0寄存器中，低32位存储于R0寄存器中。

# 指令清单24.2 Optimizing Keil 6/2013 (ARM mode)

```
||f|| PROC
LDR r0,|L0.12|
LDR r1,|L0.16|
BX lr
ENDP
|L0.12|
|L0.16|
DCD 0x90abcdef
DCD 0x12345678
```

# 24.1.3 MIPS

MIPS系统使用VO-V1 ($-$2)寄存器对传返回64位值。其中，返回的高32位存储在V0 ($2)寄存器中，低32位存储于V1 ($3)寄存器中。

# 指令清单24.3 Optimizing GCC 4.4.5 (assembly listing)

```
li $3,-1867841536 #0xffffffff90ab0000
li $2,305397760 #0x12340000
ori $3,$3,0xcdef
j $31
ori $2,$2,0x05678
```

# 指令清单24.4 Optimizing GCC 4.4.5 (IDA)

```
lui $v1,0x90AB
lui $v0,0x1234
li $v1,0x90ABCDEF
jr $ra
li $v0,0x12345678
```

# 24.2 参数传递及加减运算

本节围绕下列程序进行演示。

```
#include <stdint.h>
uint64_t f_add (uint64_t a, uint64_t b)
```