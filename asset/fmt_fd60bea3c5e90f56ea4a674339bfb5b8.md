
上述程序使用了两条 BIC 指令清除 `0x234` 对应的位。因为立即数 `0x1000` 和 `0x234` 无法封装在同一指令里。

## 19.2.6 ARM64: Optimizing GCC (Linaro)

ARM64 的编译器可以直接使用 AND 指令，不用 BIC 指令。

### 指令清单19.18 Optimizing GCC (Linaro)

```assembly
add w0, w0, -513
orr w0, w0, 1384
ret
```

## 19.2.7 ARM64: Non-optimizing GCC (Linaro)

关闭优化选项后，GCC 生成的代码中有指令，功能相同。

### 指令清单19.19 Non-optimizing GCC (Linaro)

```assembly
sub sp, #32
str w0, [sp, #12]
ldr w0, [sp, #12]
str w0, [sp, #28]
add w0, w0, -513
orr w0, w0, 1384
str w0, [sp, #28]
ldr w0, [sp, #28]
add sp, #32
ret
```

## 19.2.8 MIPS

### 指令清单19.20 Optimizing GCC (Linaro)

```asm
f:
    ori a0, 0x4000
    li v0, 0xFFFFFD
    jr ra
    and v0, a0, v0
```

`ORI` 是 OR 指令。后面的 AND 不是因为它涉及的立即数 `0xFFFFFD` 太长，无法封装在同一指令里。所以编译器把这个数值赋值给 `V0` 寄存器，然后与其他寄存器进行 AND 运算。

## 19.3 位移

C/C++ 的位移运算符是 `<<`。x86 指中有左移的 `SHL` 和右移的 `SHR`。位移操作常用于实现“2 的 n 幂”有关的乘法和除法运算。有关介绍参见书籍的 16.1.2 节和 16.2.1 节。位移指令可用于特定位置的提取或隔离，用途广泛。

## 19.4 在 FPU 上设置位

FPU 存储数据的 IEEE 754 格式如下：

### exponent mantissa or fraction (S–sign)

最高位 MSB 为符号位。是否在未使用 FPU 指令的前提下改变数的符号呢？

```c
#include <stdio.h>

float my_abs(float i) {
    unsigned int tmp = *(unsigned int*)&i & 0x7FFFFFFF;
    return (float*)&tmp;
}

float set_sign(float i) {
    unsigned int tmp = *(unsigned int*)&i | 0x80000000;
    return (float*)&tmp;
}

float negate(float i) {
    unsigned int tmp = *(unsigned int*)&i ^ 0x80000000;
    return (float*)&tmp;
}

int main() {
    printf("_my_abs: %s\n");
    printf("%f\n", my_abs(123.456));
    printf("%f\n", my_abs(-123.456));
    printf("_set_sign: %s\n");
    printf("%f\n", set_sign(123.456));
    printf("%f\n", set_sign(-123.456));
    printf("_negate: %s\n");
    printf("%f\n", negate(123.456));
    printf("%f\n", negate(-123.456));
}
```

使用 C/C++ 指令之后，我们不必在 CPU 和 FPU 的寄存器之间传递数据再进行数学运算了。本节列举了三个位操作函数：清除 MSB 符号位的 `my_abs()` 函数、设置符号位的 `set_sign()` 函数以及求正负值函数 `negate()`。

```assembly
; rl=1
LSLS r1,r1,#31
; rl=1<<31=0x80000000
ORRS r0,r0,r1
; r0=r0 ! 0x80000000
BX lr
ENDP

negate PROC
MOVS r1,#1
; rl=1=
LSLS r1,r1,#31
; rl=1<<31=0x80000000
BORS r0,r0,r1
; r0=r0 ^ 0x80000000
BX lr
ENDP
```

ARM的模式指令都是16位指令。由于单条指令无法封装太大的数据，所以编译器使用了 `MOVS/LSLS` 指令对传递常量 `0x80000000`。这种赋值操作受限于数学机制：

然而，`my_abs` 的指令允许的，它做的运算是 `(i<<1)>>1`。虽然看上去是画蛇足，但是在执行“输入变量<<1”的运算时，最高位被舍弃了。而在执行“运算结果>1”的语句时，根据右移规则则最高位变为零，而其他各位数值将归位。借助 `LSLS/LSRS` 指令，该函数清除了最高位位MSB。

Optimizing GCC 4.6.3 (Raspberry Pi, ARM mode)

指令清单19.26 Optimizing GCC 4.6.3 for Raspberry Pi (ARM mode)

```assembly
my_abs
; copy from S0 to R2:
FMRS R2, S0

; clear bit:
BIC R3, R2, #0x80000000
; copy from R3 to S0:
FMSR S0, R3
BX LR
```

```assembly
set_sign
; copy from S0 to R2:
FMRS R2, S0

; do OR:
ORR R3, R2, #0x80000000
; copy from R3 to S0:
FMSR S0, R3
BX LR
```

```assembly
negate S0 to R2:

; copy from S0 to

FMRS R2, S0

; do ADD:

ADD R3, R2, #0x8000000

; copy from R3 to S0:

FMSR S0, R3

BX LR
```

在QEMU的仿真环境中启动Raspberry Linux即可模拟ARM FPU。所以上述程序使用S-字母寄存器存储浮点数，而不是使用R-字母寄存器。

`FMRS` 指令用于寄存器GPR和FPU之间的数据交换。

上述程序中的 `my_abs()` 函数和 `set_sign()` 函数在寄存器中中断。但是 `negate()` 函数在应该出现XOR指令的地方使用了ADD指令。

> >其实“ADD register, 0x80000000”和“XOR register”是等效指令，只是特别直观而已。整个函数用于变更最高位的值。在数学上，1000与任意整数相加，运算结果的最后一位仍然和被加数的最后三位相同。例如，1234567+10000=1244567，的最后四位与第一个数的最后四位相同。以二进制形式来看，0x80000000就是10000000000000000000000000000000，只有最高位是1。因此，当0x80000000与任意整数相加时，运算结果的最后31位还是被加数的最后31位，最高位变化。对于这个特定的加数来说，ADD指令和XOR指令可以替换。这种替换的必要并不明显，但整个程序是没有问题的。

# 19.5 校验检验

我们介绍一个算术变量的二进制制中有多少个1的函数。这种函数操作“population count/点数”函数。在支持SSE的x86 CPUs的指令集，甚至有直接对应的POPCNT指令。

```c
#include <stdio.h>

#define IS_SET(flag, bit) ((flag) & (bit))

int f(unsigned int a) {
    int i;
    int rt=0;
    for (i=0; i<32; i++) {
        if (IS_SET(a, (1<<i))) {
            rt++;
        }
    }
    return rt;
}

int main() {
    f(0x12345678); // test
}
```

在这个循环里，计数变量的取值范围是0~31。因此“`1<<`”表达式的取值范围是0到0x80000000，用类语言解释，它的含义就是“将数字1左移一位”。“1<<”将“1”逐一逼近32位数字的每一位，同时将其他位置零。

这段程序里，1<<可能产生的值：

| C/C++表达式 | 二进制 | 十进制数 | 十六进制数 |
|---|---|---|---|

| 1<<0 | $2^0$ | 1 | |
| 1<<1 | $2^1$ | 2 | |
| 1<<2 | $2^2$ | 4 | |
| 1<<3 | $2^3$ | 8 | |
