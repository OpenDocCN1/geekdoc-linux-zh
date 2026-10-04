
## 64.5 64位下的x86

### 64.5.1 Windows x64

64位环境下的参数传递方法在某种程度上与fastcall函数比较相似：头部四个参数由寄存器RCX、RDX、R8和R9传递，而其余的参数都通过栈传递。调用函数必须预留32个字节或者464位的存储空间，以便被调用函数保存四个参数。小型函数可以仅凭寄存器获取所有参数，而大型函数就可能需要保存这些传递参数的寄存器，把它们腾出来供后续指令使用。

调用函数负责调整指针指向其初始状态。

此外，Windows x86-64系统的DLL文件也采用了这种调用规范。虽然，Win32系统遵循的是stdcall规范，但是Win64系统遵循的是Win64规范，不再使用stdcall规范。

以下程序例：

```
#include <stdio.h>

void fl(int a, int b, int c, int d, int e, int f, int g)
{
    printf("%d %d %d %d %d %d %d\n", a, b, c, d, e, f, g);
}

int main()
{
    fl(1,2,3,4,5,6,7);
}
```

> 指令清单64.6 MSVC 2012 /0b

```
$SG2937 DB    '%d %d %d %d %d %d %d', 0AH, 00H

main    PROC
    sub         rsp, 72              ; 00000048H
    mov         DWORD PTR [rsp+48], 7
    mov         DWORD PTR [rsp+40], 6
    mov         DWORD PTR [rsp+32], 5
    mov         r9d, 4
    mov         r8d, 3
```

```
mov edx, 2
mov ecx, 1
call f1

xor eax, eax
add rsp, 72      ; 00000048H
ret 0
main
    ENDP
```

```
a$ = 80
b$ = 88
c$ = 96
d$ = 104
e$ = 112
f$ = 120
g$ = 128
f1      PROC
```

```
$LN3:
    mov     DWORD PTR [rsp+32], r9d
    mov     DWORD PTR [rsp+24], r8d
    mov     DWORD PTR [rsp+16], edx
    mov     DWORD PTR [rsp+8],  ecx
    sub     rsp, 72              ; 00000048H

    mov     eax, DWORD PTR g$[rsp]
    mov     DWORD PTR [rsp+56], eax
    mov     eax, DWORD PTR f$[rsp]
    mov     DWORD PTR [rsp+48], eax
    mov     eax, DWORD PTR e$[rsp]
    mov     DWORD PTR [rsp+40], eax
    mov     DWORD PTR [rsp+32], eax
    mov     r9d, DWORD PTR c$[rsp]
    mov     r8d, DWORD PTR b$[rsp]
    lea     eax, DWORD PTR a$[rsp]
    mov     rcx, OFFSET FLAT:$SSG2937
    printf
```

```
    add     rsp, 72              ; 00000048H
    ret
ENDP
```

从以上的程序，我们可以清楚地看到7个参数的传递过程。程序通过寄存器传递前4个参数、再通过栈传递了其余3个参数。f1()函数通过序言部分的指令，把参数的四个寄存器的值存储到“暂存空间/scratch space”里——这正是暂存空间的正确用法。编译器无法实现确定缺少了这4个寄存器之后，后续代码是否还有足够的寄存器可用，所以会将这4个寄存器的数据保管起来，方便后续接这4个寄存器。Win64调用规范约定：应由调用方函数配置空间被调用方函数使用。

## 指令清单64.7 优化的MSVC 2012/ob

```
$SG2777 DB

a$  = 80
b$  = 88
c$  = 96
d$  = 104
e$  = 112
f$  = 120
g$  = 128
f1  PROC

$LN3:
    sub     rsp, 72              ; 00000048H
    mov     eax, DWORD PTR g$[rsp]
    mov     DWORD PTR [rsp+56], eax
    mov     eax, DWORD PTR f$[rsp]
    mov     DWORD PTR [rsp+48], eax
    mov     eax, DWORD PTR e$[rsp]
    mov     DWORD PTR [rsp+40], eax
    mov     DWORD PTR [rsp+32], eax
    mov     r9d, DWORD PTR c$[rsp]
    mov     r8d, DWORD PTR b$[rsp]
    lea     eax, DWORD PTR a$[rsp]
    mov     rcx, OFFSET FLAT:$SG2777
    call

    add     rsp, 72              ; 00000048H
    ret
ENDP

PROC
    sub     rsp, 72              ; 00000048H
    mov     edx, 2
    mov     ecx, 1
    mov     eax, DWORD PTR g$[rsp]
    mov     DWORD PTR [rsp+56], eax
    mov     eax, DWORD PTR f$[rsp]
    mov     DWORD PTR [rsp+48], eax
    mov     eax, DWORD PTR PTR$[rsp]
    mov     DWORD PTR [rsp+40],], eax
    mov     DWORD PTR [rsp+32], eax
    mov     r9d, DWORD PTR c$[rsp]
    mov     r8d, DWORD PTR b$[rsp]
    lea     eax, DWORD PTR a$[rsp]
    mov     rcx, OFFSET FLAT:$SG2777
    printf

    add     rsp, 72              ; 00000048H
    ret
ENDP

PROC
    sub     rsp, 72              ; 00000048H
    mov     edx, 2
    mov     DWORD PTR [rsp+48], 7
    mov     DWORD PTR [rsp+40], 6
    mov     DWORD PTR [rsp+32], 5
    mov     r9d, 4
    mov     r8d, 3
    mov     edx, 2
    mov     ecx, 1
    call f1

    xor eax, eax
    add rsp, 72              ; 00000048H
    ret
ENDP
```

即使使用编译器的优化选项，编译器仍然生成基础指令；只是不再分配上面的“零空间”。另外，我们看到：在启用选项之后，MSVC 2012 将一条指令合并了。这种指令能够提升效率。

## 64.5.1 64位的Windows:在C/C++中传递指针

C/C++编译器会使用RCX寄存器传递this指针、用RDX寄存器传递所需的第一个参数。对于这个例子，可以查看本书的5.1.1节。

### 64.5.2 64位的Linux

64位Linux传递参数的方法和64位Windows方法几乎相同。区别在于，64位Linux使用6个寄存器（RDX, RSI, RCX, R8, R9）传递前几个参数，而64位Windows只利用4个寄存器传递参数。另外，64位Linux程序没有上面的零空间概念。如果被调用函数的寄存器数量紧张，就可以用栈存储参数，相关寄存器腾出来。

## 指令清单64.8 优化的GCC 4.7.3

```
.LC0:
    .string "%d %d %d %d %d"
f1:
    sub     rsp, 40
    mov     eax, DWORD PTR [rsp+48]
    mov     DWORD PTR [rsp+8], r9d
    mov     r9d, ecx
    mov     DWORD PTR [rsp], r8d
    mov     ecx, esi
    mov     r8d, edx
    mov     esi, OFFSET FLAT:.LC0
    mov     edx, edi
    mov     edi, 1
    mov     DWORD PTR [rsp+16], eax
    xor     eax, eax
    call   __printf_chk
    add     rsp, 40
ret
main:
    sub     rsp, 24
    mov     r9d, 6
    mov     r8d, 5
    mov     DWORD PTR [rsp], 7
    mov     ecx, 4
    mov     edx, 3
    mov     esi, 2
    mov     edi, 1
    call    rsp
    add     rsp, 24
    ret
```

在上述指令操作AX寄存器的时候，它把数据写到了RAX寄存器的低32位（即EAX）而没有操作整个64位寄存器。这是因为在操作寄存器的低32位的时候，该寄存器的高32位会被清零。或者，这只是x86代码迁移到x86-64平台时的懒。

## 64.6 单/双精度返回值

除了Win64规范以外所有的通用规定：当返回值为单/精度浮点数据时，被调用函数返回值应当通过FPU寄存器ST(0)传递返回值。而Win64规定：被调用函数返回值应当通过XMM0寄存器的低32位（float）或64位寄存器返回单/精度浮点数据（double）。

## 64.7 修改参数

C/C++和其他其他语言的编程人员可能都遇到这样一个问题：如果被调用函数修改了传入参数的值，将会发生什么情况？答案十分：外来参数都是通过栈传递的，因此被调用函数修改的是栈里的数据。在被调用函数退出以后，调用函数不会再访问自己传递给别人的参数。

```
#include <stdio.h>

void f(int a, int b)
{
    a=a+b;
    printf("%d\n", a);
}
```

### 6.9 MSVC 2012

```
a$ = 8          ; size = 4
b$ = 12         ; size = 4
PROC
push     ebp
mov      ebp, esp
mov      eax, DWORD PTR _a$[ebp]
add      eax, DWORD PTR _b$[ebp]
mov      DWORD PTR _a$[ebp], eax
mov      ecx, DWORD PTR _a$[ebp]
push     ecx
push     OFFSET $SG2938 ; '%d', 0aH
call    _printf
add      esp, 8
pop      ebp
ret      0
ENDP
```

由此可见，只要这些参数不是C++的引用或指针，理论上讲，在被调用函数结束后，调用函数能够获取被调用函数修改的参数。

## 64.8 指针型函数

我们可以给函数分配一个指针，把它传递给其他函数：

```
#include <stdio.h>

// located in some file
void modify_a (int *a);

void f (int a)
{
    modify_a (&a);
    printf("%d\n", a);
}
```

要是看了下面的汇编代码，我们很难理解这段程序是如何运行的。变量地址通过栈传递了一个函数。

```
#include <iostream>
#include <thread>

thread_local int tmp=3;

int main() 
{
    std::cout << tmp << std::endl;
};
```

接下来，我们使用MinGW GCC 4.8.1编译它，不要用MSVC 2012进行编译。在分析可执行文件的PE之后就会发现，变量tmp被分配到TLS专用的数据保存区域了。

## 第65章 线程本地存储

线程本地存储 (Thread Local Storage, TLS) 是一种线程内部共享的数据交换区域。每个线程都可以在这个区域保存它们要在内部共享的数据。一个著名的例子是C语言的全局变量errno。对于errno类的全局变量，如果多线程进程的某一个对其进行了修改，那么这个变量就会影响到所有的线程。显然和实际需求相符，因此全局变量errno必须保存在TLS中。

为解决这个矛盾，C++ 11标准新增了一个限定符thread_local。它能将指定变量和特定的线程联系起来。由它限定的变量被初始化，并且会被存在TLS中。

## 65.1 线性同发生器（改）

本书第20章的随机数生成函数其实有一个瑕疵；在多线程运行时，它是不安全的。原因在于：它有一个内部的变量，它可能会同时被不同的线程读取或修改。

### 65.1.1 Win32系统

未初始化的TLS数据

我们可以对这种增加全局变量限定符_declspec(thread)，这样它就能被分配到TLS中。请注意下代码的9行。

```
#include <stdint.h>
#include <windows.h>
#include <winnt.h>

dendeclspec( thread ) uint32_t rand_state;
void my_rand (uint32_t init)
{
    rand_state=init;
}
int my_rand ()
{
    rand_state=rand_state*RNG_a;
    rand_state=rand_state+RNG_c;
    return rand_state & 0x7fff;
}
```

ARM64下的GCC也使用了相同传递参数。只是在这个平台上，这个空间被称为“寄存器（内容）保存区（Register Save Area）”。

### 指令清单64.11 优化的MSVC 2012（64位）

```
$SG2994 DB    '%d', 0aH, 00H

a$ = 48
f  PROC
    mov     DWORD PTR [rsp+8], ecx ; save input value
    sub     rsp, 40
    lea     rcx, QWORD PTR a$[rsp] ; get address of value
    and pass it to()
    call    modify_a
    mov     edx, DWORD PTR a$[rsp] ; reload value from
    lea     rcx, OFFSET:$SG2994 ; '%d'
    call    printf
    add     rsp, 40
    ret
ENDP
```

### 指令清单64.12 优化的GCC 4.9.1（64位）

```
.LC0:
    .string "%d\n"
f:
    sub     rsp, 24
    mov     DWORD PTR [rsp+12], edi ; store input value
to the local stack
    lea     rdi, [rsp+12] ; take an address of
the value and pass it to modify_a()
    call    modify_a
    mov     edx, DWORD PTR [rsp+12] ; reload value from
the local stack and pass it to printf()
    mov     esi, OFFSET:.LC0 ; '%d'
    mov     edi, 1
    xor     eax, eax
    call    __printf_chk
    add     rsp, 24
    ret
```

### 指令清单64.13 优化的GCC 4.9.1 ARM64

```
f:
    stp     x29,x30, [sp,-32]
    add     x29, sp, 0      ; setup FP
    add     x1, x29, 32      ; calculate address of
variable in Register Save Area
    str     w0, [x1-4]     ; store input value there
    mov     x0, x1           ; pass address of variable to
the modify_a()
bl     modify_a
ldr    w1, [x29,28]    ; load value from
the variable
and pass it to printf()
adrpr  x0, .LC0 ; '%d'
add    x0, x0, :lo12::LC0
bl     printf()      ; call printf()
ldp    x29, x30, [sp], 32
ret
.LC0: .string "%d\n"
```
