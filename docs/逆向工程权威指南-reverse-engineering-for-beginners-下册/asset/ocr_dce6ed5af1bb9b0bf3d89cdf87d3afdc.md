S字符寄存器用于处理单精度点数据。简单来说，S字符寄存器用于存储单精度浮点，而D字符寄存器用于处理双精度浮点。详细规格请参阅B. 3.3。

本例中的两个浮点数都用IEEE 754的格式存储在内存中。

望文来说，VLDR和MOV指令是操作D字符寄存器的LDR和MOV指令。这些V字符的指令和D字符的寄存器，不仅能够处理浮点类型数据，而且可以用于SIMD（NEON）运算。

即使涉及浮点运算，它还是ARM平台的配置，还会通过ARM规范的S字符寄存器传递参数；双精度浮点数据是64位数据，对于每次传递一个双精度浮点数据就需要两个S字符寄存器。

“MOV D17, R0, R1”与指令从R0和R1读取64位数据的两个部分，并将最终值存储在D17寄存器中。

“MOV R0, R1, D16”与上述指令的作用相反。它把D16寄存器的值（64位）分解成两个32位数字，并分别存储到R0和R1寄存器。

后面出现的DIV、VMUL、VADD都是浮点运算指令，不再介绍。

使用Xcode生成Thumb-2的代码，会跟这段程序相同。

# 17.5.3 ARM: Optimizing Keil 6/2013 (Thumb mode)

```
f
PUSH    {R3-R7,LR}
MOVS    R7, R2
MOVS    R4, R3
MOVS    R5, R0
MOVS    R6, R1
LDR     R2, =0x66666666;4.1
LDR     R3, =0x40106666
MOVS    R0, R7
MOVS    R1, R4
BL      __aeabi_dmul
MOVS    R7, R0
MOVS    R4, R1
LDR     R2, =0x51EB8581F;3.14
LDR     R3, =0x400910EB8
MOVS    R0, R5
MOVS    R1, R6
BL      __aeabi_ddiv
MOVS    R2, R7
MOVS    R3, R4
BL      __aeabi_dadd
POP     {R3-R7,PC}
```