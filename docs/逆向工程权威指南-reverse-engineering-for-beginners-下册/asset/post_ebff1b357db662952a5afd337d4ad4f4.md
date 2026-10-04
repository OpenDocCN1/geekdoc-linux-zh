
```
jal      float_rand
addiu   $s0, 1
lw      $gp, 0x28+var_18($sp)
; convert value we got from float_rand() to double type
; (printf() need it):
cvt.d.s $f2, $f0
lw      $t9, (printf & 0xFFFF)($gp)
mfcl    $a3, $f2
mfcl    $a2, $f3
jalr    $t9
move    $a0, $s2
bne     $s0, $s1, loc_104
move    $v0, $zero
lw      $ra, 0x28+var_4($sp)
lw      $s2, 0x28+var_8($sp)
lw      $s1, 0x28+var_C($sp)
lw      $s0, 0x28+var_10($sp)
jr      $ra
addiu   $sp, 0x28 ; branch delay slot

$LCL1:   .ascii "%f\n<0>
$LCO0:   float 1.0
```

上述程序样例出现了无实际意义的指令。17.5.6节解释了这种情况了，本节不再对其进行复述。

## 22.1.3 ARM (ARM mode)

指令清单22.3 Optimizing GCC 4.6.3 (IDA)

```
float_rand

STMFD SP!, (R3,LR)
BL      my_rand
; R0=pseudorandom value
FLDS    S0, =1.0
; S0=1.0
BIC     R3, R0, #0xFF00000
BIC     R3, R3, #0x800000
ORR     R3, R3, #0x3F800000
; R3=pseudorandom value & 0x007ffff | 0x3f800000
; copy from R3 to FPU (register S15).
; it behaves like bitwise copy, no conversion done:
FMSR    S15, R3
; subtract 1.0 and leave result in S0:
FSUBS   S0, S15, S0
LDMFD SP!, (R3,PC)
```

# flt_5C    DCFS 1.0

```
main
STMFD  SP!, {R4,LR}
MOV     R0, #0
BL      time
BL      my_srand
MOV     R4, #0x64 ; 'd'
```

```
loc_78
BL      float_rand
;=pseudandom value
LDR     R0, =aF ; "%f"
; convert float type value into double type value (printf()
; need it):
```

```
FCVTDS  D7, S0
; bitwise copy from D7 into R2/R3 pair of registers (for
printf()):
FMRRD   R2, R3, D7
BL      printf
SUBS    R4, R4, #1
BNE     loc_78
MOV     R0, R4
LMFD    SP!,{R4,PC}
```

```
aF DCB "%f",0xA,0
```

通过objdump工具对上程进行分析，看到objdump所显示的FPU指令与IDA所示的指令并不一致。这大概是因为IDA与binutils的研发人员使用的是不同的指令手册。不管原因如何，同一个FPU会有不同对应名称的情况存在。

## 指令清单22.4 Optimizing GCC 4.6.3 (objdump)

```
0000038 <float_rand>:
38:     e92d408c    push {r3, lr}
3c:     ebffffe    bl      10 <my_rand>
40:     ed9f0a05    vldr    s0, [pc,#20] ; 5c
<float_rand+0x24>
44:     e3c034ff    bic     r3, r0, #-16777216
0xff000000
48:     e3c33502    bic     r3, r3, #8388608 ; 0x0800000
4c:     e38335fe    orr     r3, r3, #106535216 ;
0x3f80000
50:     ee073a90    vmov    s15, r13
54:     ee37c0a0    vsub.32  s0, s15, s0
58:     e8bd8008    pop     {r3, pc}
```

5c:    3f800000    svccc    0x00800000

```
00000000 <main>:
0:    e92d4010    push    {r4, lr}
4:    e3a00000    mov     r0, #0
8:    ebfffffe    bl      0 <time>
c    ebffffff    bl      0 <main>
10:   e3a00064    mov     r4, #100      ; 0x64
14:   ebffffff    bl      38 <main+0x38>
18:   e59f01b8    ldr     r0, [pc,#24]  ; 38
<main+0x38>
1c:   eeb77ac0    cvt.f64.32    d7, s0
20:   ec532b17    vmov    r2, d7
24:   ebffffff    bl      0 <printf>
28:   e2544001    subs    r4, r4, #1
2c:   affffff8    bne     14 <main>
30:   e1a00000    mov     r0, r4
34:   eb8d8010    pop     {r4, pc}
38:   00000000
    float_rand() 函数地址5c的指令和main()函数38的指令都是随机噪声。

## 22.2 计算机精度

单精度点数的“机器精度”指的是相对误差的上限。因此，浮点数的数据位越多，误差越小。而单精度类型的最高精度为2^-23=1.19e-7，双精度double类型的最高精度为2^-52=2.2e-16。所以计算某数值的机器精度可能的。

```
#include <stdio.h>
#include <stdint.h>

union uint_float {
    uint32_t i;
    float f;
};

float calculate_epsilon(float start)
{
    union uint_float v;
    v.f=start;
    v.i++;
    return v.f-start;
}

void main() {
    printf("%g\n", calculate_epsilon(1.0));
}
```

解析IEEE754格式的浮点数，利用这种数据结构把float数据的部分转为整数。显然，这可能造成溢出，把最高位的进到浮点数的部分。

## 22.2.1 x86

```
tv30 = 8
_v = 8
_start = 8
fld PTR _start[esp-4] ; 冗余代码
fst PTR _v[esp-4] ; 冗余代码
inc PTR _v[esp-4]
fsub PTR tv30[esp-4] ; 冗余代码
fld PTR tv30[esp-4] ; 冗余代码
ret
_calculate_epsilon
```

上述程序的第二个FST指令是冗余：没有理由把输入值在同一个地址存储两次。这是编译器的问题：它决定变量的存储地址和参数用的栈内分配到同一个地址。接下来的指令把输入值的部分当作处理。处理结果的中间值被当作IEEE754数据传递给FPU。FSUB指令计算值，最后返回值存储到之中。程序中最后两条FST/FLD指令没有实际作用。编译器未能相应的优化。

## 22.2.2 ARM64

把数据类型扩展为64位的程序如下。

```c
#include <stdio.h>
#include <stdint.h>

union uint_double {
    uint64_t i;
    double d;
} uint_double;

double calculate_epsilon(double start)
{
    uint_double v;
    v.d=start;
    v.i++;
    return v.d-start;
}

void main() {
    printf("%g\n", calculate_epsilon(1.0));
}
```

ARM64平台的指令不能直接在FPU的D寄存器里进行加法运算。因此输入值需从D0寄存器复制到GPR，在那里进行运算并把结果复制到D1寄存器，从而从FPU里进行减法。

## 指令清单22.6 Optimizing GCC 4.9 ARM64

```
calculate_machine_epsilon:
    fmov x0, d0      ; load input value of double type into x0
    add x0, x0, 1   ; X0++
    fmov d1, x0      ; move it to FPU register
    fsub d0, d1, d0  ; subtract
    ret
```

可见上述x64程序使用了SIMD指令。有关介绍参见本书的27.4节。

## 22.2.3 MIPS

面向MIPS平台的编译器使用MTC1（Move To Coprocessor 1）指令将GPR的数据传递给FPU寄存器。

指令清单22.7 Optimizing GCC 4.5.4 (IDA)

```
calculate_machine_epsilon
    mfcl $v0, $f12
    or $at, $zero ; NOP
    addiu $v1, $v0, 1
    mtcl $v1, $f2
    jr $ra
    sub.s $f0, $f2, $f12 ; branch delay slot
```

## 22.2.4 本章小结

本章程序使用的技巧，在实际程序中出现的概率并不大。这些技巧可以充分演示IEEE 754型数据和C/C++ UNION型数据结构的特点。

## 22.3 快速平方根计算

浮点数解释的另一个名的算法，是快速平方根计算。

指令清单22.8 取自http://go.yurichev.com/17364的源代码

```c
/* Assumes that float is in the IEEE 754 single precision floating point format
* and that int is 32 bits. */
float sqrt_approx(float z)
{
    int val_int = (int*)&z; /* Same bits, but as an int */
    /*
    * To justify the following code, prove that
    * (((val_int / 2^m) - b) / 2) + b) * 2^m = ((val_int - 2^m) / 2) + ((b + 1) / 2)
    */
*where
* b = exponent bias
* m = number of mantissa bits
*/
val_int -= 1 << 23; /* Subtract 2^m. */
val_int >> 1; /* Divide by 2. */
val_int += 1 << 29; /* Add ((b + 1) / 2) * 2^m. */
return *(float*)&val_int; /* Interpret as float */
```

作为一个练习，你可以尝试编译这个函数，理解它是如何工作的。这一个非常有名的计算 $\sqrt{}$ 的算法因为Quake III中变得流行。该算法的描述和源代码参见http://go.yurichev.com/17364。

- Pseudorandom number generator,伪随机数生成。
- 参考了网络文章 http://wordpress.com/2010/09/how-to-generate-floating-point-numbers-efficiently.

## 第23章 函数指针

函数指针和其他指针之间太大区别。它代表代码段的起始地址。函数指针（地址）以参数的形式传递给另一个函数，用来调用指针时，这种指针就是“回调函数”。此类指针主要应用场景：

- 标准C库里的qsort()函数
- UNIX系统里的信号(Signals)。
- 启动线程的CreateThread和pthread_create()(POSIX)。
- Win32的多种函数，例如EnumWindows()[
- Linux内核。例如，Linux以回调方式调用系统：http://kernel.org/source/include/fs.h。
- GCC插件：https://www.gnu.org/linedocs/gcc-API.html。
- Linux窗口程序定义。当键盘接收到特定键时，对应的快捷方式通过调用相应的函数。参见https://github.com/cdown/dwm/config.def

## 23.1 MSVC

使用MSVC 2010（启用选项/Ox/GS/-MD）编译上述程序，可得到下述汇编指令（为了重点而精简）。

## 指令清单2.1 Optimizing MSVC 2010: /GS- /MD

```
_a$ = 8 ; size = 4
_b$ = 12 ; size = 4
_comp PROC
    mov eax, DWORD PTR _a$[esp-4]
    mov ecx, DWORD PTR _b$[esp-4]
    mov eax, DWORD PTR [eax]
    mov ecx, DWORD PTR [ecx]
    mov eax, eax
    cmp eax, ecx
    jne SHORT $LN4@
    xor eax, eax
    ret
LN4@:
    xor edx, edx
    cmp eax, ecx
    setge dl
    lea eax, DWORD PTR [edx+edx-1]
    ret
_comp ENDP

_numbers = -40 ; size = 40
_argc$ = 8 ; size = 4
_argv$ = 12 ; size = 4
_main PROC
    push esp, 40 ; 00000028H
    push esi
    push OFFSET _comp
    push 4
    lea eax, DWORD PTR _numbers$[esp+52]
    push 10 ; 000000aAH
    push eax
    mov DWORD PTR _numbers$[esp+60], 1892 ; 00000764H
    mov DWORD PTR _numbers$[esp+64], 45 ; 0000002dH
    mov DWORD PTR _numbers$[esp+68], 200 ; 000000c8H
    mov DWORD PTR _numbers$[esp+72], -98 ; ffffffe9e
    mov DWORD PTR _numbers$[esp+76], 4087 ; 00000ff7H
    mov DWORD PTR _numbers$[esp+80], 5 ; 00000005H
    mov DWORD PTR _numbers$[esp+84], -12345 ; fffff7cH
    mov DWORD PTR _numbers$[esp+88], 1087 ; 000004FH
    mov DWORD PTR _numbers$[esp+92], 88 ; 00000058H
    mov DWORD PTR _numbers$[esp+96], -100000 ; fffe7960H
    call qsort
    add esp, 16 ; 00000010H
```

我们来看这段程序：

```c
/* Sorting int with qsort */
#include <stdio.h>
#include <stdlib.h>

int comp(const void *_a, const void *_b) {
    const int *a=(const int *)a;
    const int *b=(const int *)b;
    if (*a==b)
        return 0;
    else if (*a < *b)
        return -1;
    else
        return 1;
}

int main(int argc, char *argv[]) {
    int numbers[10]={189245,200,-98407,5,-12345,108788,-100000};
    int i;
    /* Sort the array */
    qsort(numbers,10,sizeof(int),comp);
    for (i=0;i<9;i++)
        printf("Number = %d\n",numbers[i ]);
    return 0;
}
```