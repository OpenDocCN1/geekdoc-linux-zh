

以下是实现过程的描述:

SAR算术右移[11]，算术右移31是带符号的操作。有符号的最高有效位MSB就是符号位。也就是说，如果MSB的值为1（原始数是负数），那么右移31位后，不管原来的数是什么，得到的结果都是0xffffffff。如果MSB的值为0（原始数是正数或零），那么最后的结果就会零。执行完SAR，返回被存储在EDX寄存器中。“XOR指令（寄存器），.0xffffffff，相当于位求非的逻辑或运算；由于这条指令就变成了完成补码法（加一）运算；由于SUB的指令就是减一（加一）运算，得到绝对值，因为此时EDX寄存器的值是0xffffff——十进制的“-1”。有两个操作的逻辑运算和递减运算，请参阅本书第30章。

因此，当操作是负数的时候，最后两条运算指令会对源操作进行处理。在符号位的值为零、零零和正数的情况下，最后两条指令不会调整源操作的值。

有关于本例的详细细节，请调查参考书籍[War02, pp. 2-4]的相关介绍。GCC或许鉴了现有的成熟算法，或许这它是自己推演的计算结果。

## 45.2 ARM64的GCC 4.9 移位

GCC 4.9 for ARM64的编译方式和GCC for x64的编译方式相似，只是它使用的是自己CPU平台的64位寄存器而已。由于ARM64可以通过参数传递符ASR的指令完成位移运算，因此GCC 4.9 for ARM64比GCC的指令少。

指令清单45.2 ARM64下的GCC 4.9优化

```
my_abs:
; sign-extend 32-bit value to X0 64-bit register:
  sxtw w0, w0
  eor x1, x0, x0, asr 63
; X1=X0^(X0>>63) (shift is arithmetical)
```

```
sub x0, x1, x0, asr 63
; X0=X1-(X0>>63)=X0^(X0>>63)-(X0>>63) (all shifts are
arithmetical)
ret
```

[1] 原文为左移。

## 第46章 变长参数函数

像printf()和scanf()类的函数可以处理不同数量的输入参数。这种函数又是如何访问参数的呢？

### 46.1 计算术平均值

如果编写一个计算术平均值的函数，那么就需要函数的参数声明部分指定所有的外部参数。但是C/C++的变长参数函数却无法先知道外部参数的数量。为了方便起见，我们用“-1”作为最后一个参数其他参数的结束符。

C语言标准函数的头文件stdarg.h定义了变长参数的处理方法（宏）。刚才提到的printf函数和scanf()函数都使用了这个文件提供的宏。

```
#include <stdio.h>
#include <stdarg.h>

int arith_mean(int v, ...)
{
    va_list args;
    int sum=0, count=1, i;
    va_start(args, v);

    while(1)
    {
        i=va_arg(args, int);
        if (i==-1) // terminator
            break;
        sum=sum+i;
    }
```

```
count++;
}
    va_end(args);
    return sum/count;
};
int main()
{
    printf("%d\n", arith_mean (1, 2, 7, 10, 15, -1 /* terminator*/));
}
```

变长参数函数按照常规函数参数的方法从外部传来的第一个参数。后，借助stdarg.h提供的var_arg宏调用其剩余参数，依次求得各参数之和，最终计算其平均值。

### 46.1.1 cdecl调用规范

指令清单46.1 MSVC 6.0优化

```
_v$ = 8
_arith_mean PROC NEAR
    mov eax, DWORD PTR _v$[esp-4] ; load 1st argument
into sum
    push esi
    mov esi, 1                   ; count=1
    lea edx, DWORD PTR _v$[esp]  ; address of the 1st
argument
$L838:
    mov ecx, DWORD PTR [esp+4]   ; load next argument
    add edx, 4                   ; shift pointer to
the next argument
    cmp ecx, -1                  ; is it -1?
    je SHORT $L856                ; exit if so
    add eax, ecx                 ; sum = sum + loaded
argument
    inc esi                      ; count++
    jmp SHORT $L838
$L856:
    ; calculate quotient
    cdq
    idiv esi
    pop esi
    ret 0
```

```
_arith_mean ENDP
```

```
_SG851 DB    '%%d', 0aH, 00H

_main       PROC NEAR
push        -1
push        15
push        10
push        7
push        2
push        1
call        arith_mean
push        eax
push        OFFSET FLAT:$SG851 ; '%d'
call        printf
add         esp, 0
ret
```

main()函数，各项参数从右向左依次传入。第一个入栈的是最后一个参数“-1”，而最后入栈的是第一个参数——格式化字符串。arith_mean()取出第一个参数的值，将其保存在变量sum中。接着，将第二个参数的地址保存在寄存器EDX中，并取出值，与前面的sum相加。如此循环复，直到参数结束。按照这种算法计算出来的结果就是平均值。在调用变长参数时，函数首先要把确定参数长度为数组，再把这个数组传递给函数。这就解释了为什么cdecl调用规范将最后一个参数推入栈会导致找不到第一个参数。

### 46.1.2 基于寄存器的调用规范

细心的读者可能会问，那些优先利用寄存器传递参数的情况？我们就来看吧。指令清单46.2 x64下的MSVC优化

```
$SG013 DB    '%d', 0aH, 00H

v$ = 8
arith_mean PROC
    mov DWORD PTR [rsp+8], ecx      ; 1st argument
    mov QWORD PTR [rsp+16], rdx   ; 2nd argument
    mov QWORD PTR [rsp+24], r8   ; 3rd argument
    mov DWORD PTR [rsp+32], r9   ; 4th argument
    mov DWORD PTR [rsp+40], rsi   ; 5th argument
    mov DWORD PTR [rsp+48], rcx   ; 6th argument
lea rax, [rsp+8]
save 6 register registers in "red zone" in the local stack
mov QWORD PTR [rsp-40], rsi
mov QWORD PTR [rsp-32], rdx
mov QWORD PTR [rsp-16], r8
mov QWORD PTR [rsp-24], rcx
mov esi, 8
mov QWORD PTR [rsp-64], rax
lea rax, [rsp-48]
mov rbd, 1
mov QWORD PTR [rsp-56], rax
jmp .5
.L7:
; work out saved arguments
lea rax, [rsp-48]
mov ecx, esi
add esi, 8
add rcx, rax
mov ecx, DWORD PTR [rcx]
```

在这个程序里，寄存器负责函数的4参数，传递函数剩余的2个参数。函数arith_mean()首次将寄存器传递的参数存放在影空间，把影空间和传递参数的栈合并了一个连续的参数区域！GCC在编译的时候明显添加。它把函数分为两部分：第一部分的指令将寄存器的值保存在“红色带”，并在里面处理；而第二部分指令再处理参数。

指令清单46.3 x64下的GCC 4.9.1优化

```
arith_mean:
lea rax, [rsp+8]
save 6 register registers in "red zone" in the local stack
mov QWORD PTR [rsp-40], rsi
mov QWORD PTR [rsp-32], rdx
mov QWORD PTR [rsp-16], r8
mov QWORD PTR [rsp-24], rcx
mov esi, 8
mov QWORD PTR [rsp-64], rax
lea rax, [rsp-48]
mov rbd, 1
mov QWORD PTR [rsp-56], rax
jmp .5
.L7:
; work out saved arguments
lea rax, [rsp-48]
mov ecx, esi
add esi, 8
add rcx, rax
mov ecx, DWORD PTR [rcx]
```

