
)。如果它们是 `unsigned char` 或 `uint8_t` 型数据，那么此处就会成为 MOVZX 指令。

## OllyDbg + 字段单字节对齐

这种情况下，整个结构的各个变量在内存中依次排列，如图 21.4 所示。

![](img/a13a81a53f805f55074b2e5d2ec754b6_554_0.png)

图21.4 OllyDbg: 在调用 printf() 函数之前

## 21.4 ARM

Using Keil 6/2013 (Thumb mode)

# 使用 Keil 6/2013（开启优化选项）、Thumb 模式编译上述程序可得下所示的代码。

 指令清单 21.21 Optimizing Keil 6/2013 (Thumb mode)

```
.text:0000003E    exit ; CODE XREF: f+16
.text:0000003E 05 B0    ADD  SP, SP, #0x14
.text:00000040 00 BD    POP   (PC)
.text:00000280            f
.text:00000280        var_1 = -0x18
.text:00000280        a = -0x14
.text:00000280        b = -0x10
.text:00000280        c = -0xC
.text:00000280        d = -8
.text:00000280
.text:0000028F 05 B5    PUSH {R0-R3, LR}
.text:00000292 21 B0    SUB  SP, SP, #4
.text:00000284 04 98    LDR  R0, [SP,#16] ; d
.text:00000286 02 9A    STR  R2, [SP,#8] ; b
.text:00000288 00 90    STR  R0, [SP]
.text:0000028A 68 46    MOV  R0, SP
.text:0000028C 03 7B    LDR  R3, [R0,#12] ; c
.text:0000028E 01 79    LDR  R1, [R0,#4] ; a
.text:00000290 59 00    ADR  R0, #aBCDD ; "a=d; b=c;c=d;"
.text:00000292 05 F0 AD FF BL   _printf
.text:00000296 2D E6    exit
```

本机被调用函数返回的是结构体类型，不是结构体的指针。由于 ARM 利用寄存器传递函数的前 4 个参数，编译器 R0~R3 寄存器将存储 `printf(d)` 函数的全部参数。

LDRB 从内存加载 1 个字节转换为 32 位符号数，用于从结构体中提取字段 `d`。它相当于 x86 中的 MOVZX 指令。

注意，在函数退出时，它借用了另一个函数名！这种借助 B 指令跳转到此处完全不是相同的函数现象，应当是因为两个函数的局部栈使用了相同的空空间。或许由于这两个函数在启动时的对齐内存（相同部分排列了 7~5-0x14 的数据域），导致退出语句也完全相同缘故，再加上它们内部存储的地址的因素，所以编译器进行了这种处理。确实，退出不会影响程序。JMP 指令只占 2 个字节，而标准的跳转占用 4 个字节。

ARM + Optimizing Xcode 4.6 (LLVM) (Thumb mode)

# 指令清单 21.22 Optimizing Xcode 4.6 (LLVM) (Thumb mode)

```
var_C = -0xC

PUSH     (R7, LR)
MOV      R7, SP
SUB      SP, SP, #4
MOV      R9, R1;
MOV      R1, R0;
MOVW     R0, #0xF1; "a=%d; b=%d; c=%d; d=%d\n"
SXB      R1, R1; ; 备 a
MOVW     R0, #0
STR      R3, [SP]; ; 供 printf() 调用
ADD      R0, PC; ; 格式化字符串
SXB      R3, R2; ; 备 c
MOV      R2, R9; ; 备 b
BL       _printf
ADD      SP, SP, #4
POP      (R7)
```

SXB（Signed Extend Byte）对应 x86 的 MOVZX 指令，但是它处理寄存器的数据，不能直接对内存操作。程序中的其余指令与前一个一样，本文将重复一遍。

## 21.43 MIPS

# 指令清单 21.23 Optimizing GCC 4.4.5 (IDA)

```
f:
2 var_18 = -0x18
4 var_10 = -0x10
5 var_4 = -4
6 arg_0 = 0
7 arg_4 = 4
8 arg_8 = 8
9 arg_C = 0xC
10:
11 $a0=a
12 $a1=b
13 $a2=d
14 $a3=d
15 lui      $gp, (_gnu_local_gp >> 16)
16 addiu    $sp, -0x28
17 la       $gp, (_gnu_local_gp & 0xFFFF)
18 sw       $sp, 0x28+var_4
19 sw       $gp, 0x28+var_10
20 ; prepare byte from 32-bit big-endian integer:
21 sra      $t0, $a0, 24
22 move     $v1, $a1
23 ; prepare byte from 32-bit big-endian integer:
```
```
24 sra      $v0, $a2, 24
```
```
25 lw       $t9, (_gp & 0xFFFF)
```
```
26 sw       $a0, 0x28-arg_0
```
```
27 sw       $a0, (_LCO) >> 16 # "a=d; b=c; c=d; d=\n
```
```
28 sw       $a3, 0x28-var_1
```
```
29 sw       $a1, 0x28-arg_4
```
```
30 sw       $a2, 0x28-arg_8
```
```
31 sw       $a3, 0x28-arg_C
```
```
32 la       $a0, (_LCO & 0xFFFF) # "a=d; b=c; c=d; d=%n
```
```
33 move     $a1, $t0
```
```
34 move     $a2, $v1
```
```
35 jal       $t9
```
```
36 move     $a3, $v0; delay slot
```
```
37 lw       $ra, 0x28-var_4
```
```
38 or       $at, $zero; load slot, NOP
```
```
39 jr       $ra
```
```
40 addiu    $sp, $sp, 32
```
```
41 $LCO: :ascii="a=%d; b=%d; c=%d; d=%d"
字段被安置于 a0~a3 寄存器中，又重新赋值于 a1~a3 寄存器中给 printf() 函数。为了特殊的，上述程序使用了两次 SRA（Shift Right Arithmetic）指令，而 SRA 指令用于制备 char 型的数据。这是什么呢？MIPS 架构采用大端（big-endian），参见手册第 31 章，此外 Debian 也使用大端。当使用 char 型数据时，占据 32 位。因此，当 char 型扩展为 32 位时，必须移动位移指令不能使用逻辑位移指令。

## 21.4 其他

传递结构体时（不是结构体的指针）的过程相当于依次传递结构体的字段。也就是说，如果结构体字段不变，那么 f() 函数源代码改写为：

```
void f(char a, int b, char c, int d) {
    printf("a=%d; b=%d; c=%d; d=%d\n", a, b, c, d);
}
```
经过上述，编译器生成的不会变化。

