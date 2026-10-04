
使用加法 `ADD` 而不是减法 `SUB`。我们注意到程序中有一行指令是“ADD EAX,-32”，它用来实现EAX寄存器中减去32的目的。程序没有采用指令““SUB EAX,32”，也就是说程序使用了 `EAX=EAX+(-32)` 的算法，而不是采用 `EAX=EAX-32` 的算法。是否值得这么做的，笔者并不能完全确定。

为了实现“乘以5”的运算使用了 `LEA` 指令：`lea ccx,DWORD PTR[ecax+*4]` 使得“*4”和“*5”是相等的。但是指令运行速度比 `IMUL` 快。另外还可以使用指令`SHL EAX,2` 和 `ADD EAX,EAX` 来代替。确实有些编译器是这样做的。

这里用到了乘法代替除法的技巧。参见第41章。

如果主函数 `main()` 没有明确的返回，在程序退出时，它的返回值为0。C99标准中规定：“如果main函数没有通过明确的return 指令声明其返回，那么它就会默认返回0”。当然这项准则仅适用于主函数 `main()`。虽然MSVC并未完全遵循C99标准，但是允许部分编译器遵循了这一标准。这里指的C99标准是ISO07,P.5.1.2.3。

## 35.1.2 x64架构下的MSVC 2012优化

x64的代码和x86的代码大体相同。只是每次调用 `exit()`函数后，有一个 `INT 3`。

```
xor     ecx, ecx
call    QWORD PTR __imp_exit
int     3
```

INT 3是调试器debugger的断点设置不会。

程序执行 `exit()`函数之后，它就不会再回到原程序，而是直接退出了。编译器默认是，在发生异常退出的情况下，通常人们使用调试器分析异常情况吧。

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

MSVC 2010 x86采用的FPU指令。

指令清单35.2 MSVC 2010x86优化

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

但MSVC 2012分配的是SIMD指令。指令清单35.3 MSVC 2012 x86

```
$SG4228 DB 'Enter temperature in Fahrenheit:', 0AH, 00H
$SG4230 DB '%lf', 00H
$SG4231 DB 'Error while parsing your input', 0AH, 00H
$SG4233 DB 'Error: incorrect temperature!', 0AH, 00H
$SG4234 DB 'Celsius: %lf', 0AH, 00H
```

```
_real@c071100000000000 DQ 0c07110000000000r ; -273
_real@4040000000000000 DQ 0404000000000000r ; 32
_real@4022000000000000 DQ 0402000000000000r ; 9
_real@4014000000000000 DQ 0401000000000000r ; 5
```

```
_fahr$ = -8             size = 8
_main
    sub esp, 8
    push esi
    mov esi, DWORD PTR __imp_printf
    push OFFSET $SG4228      ; 'Enter temperature in Fahrenheit:'
    call            esi                 ; call printf()
    lea eax, DWORD PTR _fahr$[esp+16]
    push            eax
    push            OFFSET $SG4230      ; '%lf'
    call            DWORD PTR __imp_scanf
    add             esp, 12              ; 000000cH
    cmp             eax, 1
    push            SHORT $LN2@main
    je              OFFSET $SG4231      ; 'Error while parsing your input'
        call            esi                 ; call printf()
        add             esp, 4
        push            esi
        push            0
        call            DWORD PTR __imp_exit
$LN9@main:
$LN2:
    movsd           xmm1, QWORD PTR _real@4040000000000000; ; 32
    subsd           xmm1, QWORD PTR _real@c071100000000000; ; -273
    movsd           xmm0, QWORD PTR _real@4014000000000000; ; 5
    mulsd           xmm1, QWORD PTR _real@4022000000000000; ; 9
    divsd           xmm0, xmm1
    comisd          xmm0, xmm1
    jbe             SHORT $LN1@main      ; 'Error: incorrect temperature!'
        push            OFFSET $SG4233
        call            esi                 ; call printf()
        add             esp, 4
```

```
push        0
call        DWORD PTR __imp__exit
$LN10@main:
$LN1@main:
    sub         esp, 8
    movd        QWORD PTR [esp], xmm    ; 'Celsius: %lf'
    push        $SG4234
    call        esi             ; call printf()
    add         esp, 12        
0000000Ch return 0 - by C9 standard
    xor         eax, eax
    pop         esi
    add         esp, 8
    ret         0
$LN8@ret
```

当然，x86的指令集确实支持SIMD，浮点运算毫无问题。大概是这种方式的计算比较简单，所以微软的编译器分配了SIMD。我们注意到绝对度-273，早就引入了寄存器XMM0。这没关系，编译器不是按照源代码的顺序分配汇编指令。

# 第36章 斐波契数列

计算机方面的教科书里，斐波契数列的规则非常简单：从第三个数开始，数字为前两项之和。因此，常见的斐波契数列：0, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, 233, 377, 610, 987...

36.1 例子

这个程序可以生成不超过21的数列：
```c
#include <stdio.h>

void fib(int a, int b, int limit)
{
    printf("%d\n", a+b);
    if (a+b > limit) {
        return;
    }
    fib(b, a+b, limit);
}

int main()
{
    printf("0\n1\n");
    fib(1, 1, 20);
}
```

指令清单36.1 MSVC 2010 x86

| 地址 | 指令 | size |
|---|---|---|
| 00FD1000 | 55 | PUSH ESP | 4 |
| 00FD1001 | 89 E5 | MOV EBP,ESP | 4 |
| 00FD1003 | 8B EC 04 | MOV [EBP+4] | 4 |
| 00FD1006 | 83 EC 04 | ADD ESP, 04 | 4 |
| 00FD1009 | 55 8B | PUSH EDI PUSH EBP | 4 |
| 00FD100B | 89 D5 | MOV EBP,EBP | 2 |
| 00FD100E | 83 EC 08 | ADD ESP, 08 | 4 |
| 00FD1011 | 8B 45 08 | MOV EDI,[EBP+8] | 4 |
| 00FD1014 | 89 C7 | MOV EAX,EDI | 2 |
| 00FD1016 | 55 | PUSH ESI | 1 |
| 00FD1017 | E8 EB 07 | JUMP SHORT, 00FD1030 | 5 |
| 00FD101C | 89 F6 | MOV ESI,EAX | 2 |
| 00FD101E | 8B 45 0C | MOV EAX,[EBP+12] | 4 |
| 00FD1021 | 83 EC 0A | ADD ESP, 00A | 4 |
| 00FD1023 | 55 | PUSH EBP | 1 |
| 00FD1024 | 89 E5 | MOV EBP,EBP | 2 |
| 00FD1026 | 8B 45 14 | MOV EDI,[EBP+20] | 4 |
| 00FD1029 | 83 EC 10 | ADD ESP, 10 | 4 |
| 00FD102C | 8B 45 18 | MOV EAX,[EBP+24] | 4 |
| 00FD102F | 89 C7 | MOV EAX,EDI | 2 |
| 00FD1031 | 55 | PUSH ESP | 1 |
| 00FD1032 | E8 EB F5 | JUMP SHORT, 00FD1020 | 5 |
| 00FD1037 | 89 F6 | MOV ESI,EAX | 2 |
| 00FD1039 | 8B 45 2C | MOV EAX,[EBP+28] | 4 |
| 00FD103C | 83 EC 1C | ADD ESP, 1C | 4 |
| 00FD103E | 55 | PUSH EBP | 1 |
| 00FD103F | 89 E5 | MOV EBP,EBP | 2 |
| 00FD1041 | 5D | POP ESI | 1 |
| 00FD1042 | 5D | POP EBP | 1 |
| 00FD1043 | C3 | RET | 1 |

我们重点分析这个结构的。我们在lyDbg中加载本例的可执行程序，并跟踪到调用f()函数的那条指令，如图36.1所示。

CPU - main thread, module file

