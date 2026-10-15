
其中 `0x7B` 就是十进制 `123`。在采用小端字节序的平台上（例如 `x86-64`），第一个字节就是 `0x7B`。但是 `MIPS` 采用的大端字节序，数值最高的字节排列在前。正是因为 `MIPS` 硬件平台可能采用不同的字节序，所以 `MIPS Linux` 分为大端和小端。一种字节序平台上编译出来的程序不可能在另一种字节序平台上运行。本节介绍了 `MIPS` 大端字节序的特征。

## 31.4 双端

`ARM`, `PowerPC`, `SPARC`, `MIPS`, `IA64` 等 `CPU` 采用双端模式（`Bi-endian`），可以在小端字节序和大端字节序之间切换。

## 31.5 转换字节序

`BSWAP` 指令可在汇编层面转换字节序。`TCP/IP` 数据的封装规范采用大端字节序，所以采用小端字节序的平台就需要专门的转换字节序函数。常用的字节序转换函数是 `htons()` 和 `ntohs()`。

在 `TCP/IP` 的术语里，大端字节序又称为“网络字节序（`Network Byte Order`）”，主机的字节序叫作“主机字节序”。`x86` 和其他平台的主机字节序是小端字节序，但是 `IBM POWER` 等服务器系列均采用大端字节序。因此，在主机字节序为大端字节序的平台上使用 `htonl()` 或 `htons()` 函数转换字节序，其实不会发生真正意义的字节重排。

[1] Debian 网站提供下载：`https://people.debian.org/~urel/qemu/`

# 第32章 内存布局

`C/C++` 把内存划分为若干区域，主要的内存区域有：

- 全局内存空间，又称为（全局）静态存储区 `static memory allocation`。不需要全局变量和静态变量明确划分存储空间，全局变量、全局数组等。

使用加法 `ADD` 而不是减法 `SUB`。我们注意到程序中有一行指令是“`ADD EAX,-32`”，它用来实现 `EAX` 寄存器中减去 `32` 的目的。程序没有采用指令“`SUB EAX,32`”，也就是说程序使用了 `EAX=EAX+(-32)` 的算法，而不是采用 `EAX=EAX-32` 的算法。是否值得这么做的，笔者并不能完全确定。

为了实现“乘以5”的运算使用了 `LEA` 指令：`lea ccx,DWORD PTR[ecax+*4]` 使得“*4”和“*5”是相等的。但是指令运行速度比 `IMUL` 快。另外还可以使用指令 `SHL EAX,2` 和 `ADD EAX,EAX` 来代替。确实有些编译器是这样做的。

这里用到了乘法代替除法的技巧。参见第41章。

如果主函数 `main()` 没有明确的返回，在程序退出时，它的返回值为0。`C99` 标准中规定：“如果 `main` 函数没有通过明确的 `return` 指令声明其返回，那么它就会默认返回0”。当然这项准则仅适用于主函数 `main()`。虽然 `MSVC` 并未完全遵循 `C99` 标准，但是允许部分编译器遵循了这一标准。这里指的 `C99` 标准是 `ISO07,P.5.1.2.3`。

## 35.1.2 x64 架构下的 MSVC 2012 优化

`x64` 的代码和 `x86` 的代码大体相同。只是每次调用 `exit()` 函数后，有一个 `INT 3`。

```
xor     ecx, ecx

call    QWORD PTR __imp_exit

int     3
```

`INT 3` 是调试器 `debugger` 的断点设置不会。

程序执行 `exit()` 函数之后，它就不会再回到原程序，而是直接退出了。编译器默认是，在发生异常退出的情况下，通常人们使用调试器分析异常情况吧。

## 35.2 浮点数运算

```c
#include <stdio.h>
#include <stdlib.h>
int main()
{
    double celsius, fahr;
    printf("Enter temperature in Fahrenheit:\n");
    if (scanf("%lf", &fahr)!=1) {
        printf("Error while parsing your input\n");
        exit(0);
    }
    celsius = 5 * (fahr-32) / 9;
    if (celsius<273) {
        printf("Error: incorrect temperature!\n");
        exit(0);
    }
    printf("Celsius: %lf\n", celsius);
}
```

`MSVC 2010 x86` 采用的 `FPU` 指令。

指令清单35.2 `MSVC 2010x86` 优化

```
$4038 DB 'Enter temperature in Fahrenheit:', 0AH, 00H
$4040 DB '%lf', 00H
$4041 DB 'Error while parsing your input', 0AH, 00H
$4043 DB 'Error: incorrect temperature!', 0AH, 00H
$4044 DB 'Celsius: %lf', 0AH, 00H
```

```
__real@c071100000000000 DQ 0c07110000000000r ; -273
__real@0402200000000000 DQ 0402200000000000r ; 9
__real@0401400000000000 DQ 0401400000000000r ; 5
__real@0404000000000000 DQ 0404000000000000r ; 32
```

```
__fahr$ = -8 ; size = 8
_main PROC
    sub esp, 8
    push esi
    mov esi, DWORD PTR __imp_printf
    push OFFSET $4038 ; 'Enter temperature in
Fahrenheit:'
    push esi
    call ; call printf()
    lea eax, DWORD PTR _fahr$[esp+16]
```

```
push      eax
push      OFFSET $SG4040    ; '%lf'
call      DWORD PTR __imp_scnaf
add       esp, 12               ; 
000000cH
cmp       eax, 1
je        SHORT $LN2@main    ; 'Error while parsing
      OFFSET $SG4041    ; 'your input'esi
call                      ; call printf()
add       esp, 4
push      0
call      DWORD PTR __imp_exit
$LN2@main:
fld       QWORD PTR _fahr$esp[12]
fsub      QWORD PTR _real@4040000000000000 ; 32
mfmul     QWORD PTR _real@4014000000000000 ; 5
div       QWORD PTR _real@4022000000000000 ; 9
fld       QWORD PTR _real@c071100000000000 ; -273
fcomp     ST(1)
fnstsw ax
test      ah, 65               ; 0000041H
je        SHORT $LN1@main
push      OFFSET $SG043    ; 'Error: incorrect
temperature!'esi
call                      ; call printf()
stp      ST(0)
add       esp, 4
sub       esp, 8
fstp      QWORD PTR [esp]
push      OFFSET $SG044    ; 'Error: %lf'
call      esi
add       esp, 12               ; 000000C return 0 - by C standard
xor       eax, eax
pop       esi
add       esp, 8
ret       0
$LN1@main:
_main ENDP
```

但 `MSVC 2012` 分配的是 `SIMD` 指令。指令清单35.3 `MSVC 2012 x86`
