
以 'A' 的编码作为输入参数。该输入参数被压入堆栈。因此，同一函数调用的汇编代码如下所示：

### **程序 7.5**

```assembly
MOV EBX, 65
PUSH EBX
MOV EDX, 0
IN EAX, [DX]
ABC: CMP EAX, 1    ;
     JE FIN        ;如果 EAX = 1，则结束。
     INC EDX        ;使用 EDX 作为计数器。
     CALL HAF       ;这是子程序调用！
     CMP EBX, 0     ;EBX = 0 表示 EAX 是奇数
     JE ODD         ;
     MOV EAX, EBX   ;如果不是，则 EBX 是 EAX 的一半
     JMP ABC        ;
ODD: MOV EBX, EAX   ;将 EAX 乘以 3 并加 1
     ADD EAX, EBX   ;
     ADD EAX, EBX   ;
     INC EAX
     JMP ABC        ;
FIN: MOV EAX, EDX   ;EDX 包含最终计数。
     MOV EDX, 1
     OUT [DX], EAX
     RET
```

### **程序 7.6**

```c
#include <ctype.h>

main()
{
    int x,y;

    x = 65; /* x = 'A' */
    y = tolower(x); /* y = 'a' */
}

CALL tolower
ADD ESP, 4
```

尽管使用堆栈存储返回值似乎是一个自然的想法，但更常见的做法是使用寄存器。在针对 x86 架构的 GNU C 中，返回的整数值存储在 EAX 寄存器中。不同语言在子程序还是主程序负责从堆栈中弹出参数方面存在差异。在 Fortran、Basic 和 Pascal 中，由子程序弹出堆栈，但在 C 中由调用程序执行此操作。这就是刚才展示的调用程序中 `ADD ESP, 4` 指令的原因。

语言在参数压入堆栈的顺序上也存在差异。C 语言从右侧开始压入参数。假设我们定义了一个整数幂函数 `ipow()`：

```c
int ipow(int base, int exponent);
```

调用此函数以计算 $2^3$ 的汇编代码如下所示：

```assembly
MOV EBX, 3
PUSH EBX
MOV EBX, 2
PUSH EBX
CALL ipow
ADD ESP, 8
```

在此调用之后，结果 `ipow(2, 3) = 8` 将存储在 EAX 寄存器中。

### 7.3.1 全局汇编指令

在由 GNU 编译器生成的 .o 文件中，诸如 `printf` 或 `tolower` 等需要外部链接的符号在符号表中的编码方式不同。如果没有这种特殊编码，GNU 链接器将忽略这些符号，导致链接失败。为了获得这种特殊编码，汇编语言源代码必须特别指示哪些符号需要接受这种处理。GNU 汇编器和 Edlinas 都识别一条汇编器指令，该指令将使汇编器在符号表中将符号编码为可用于链接。其语法是

```assembly
.globl symbol
```

在 NASM 中，语法为：

```assembly
global symbol
```

### 7.3.2 从 C 调用汇编

如果从 C 调用 `half` 子程序，它将无法正常工作，因为它不在 EAX 寄存器中返回值。此外，它也没有压入其使用的寄存器。在下面的代码中，由于 ECX 被使用，且调用程序可能将其用于其他用途，因此 ECX 被压入堆栈。我们还需要使用全局指令使函数名称可见。

我们刚刚编写了一个汇编函数，可以从 C 程序中调用。C 程序会将调用参数存储在堆栈上。它将被埋在调用程序压入的返回地址以及刚刚压入的 ECX 内容之下。这两项在堆栈上占用八个字节，因此调用参数的访问地址为 ESP + 8。结果存储在 EAX 中，而不是 EBX。要在 Edlinas 中保存对象代码为 .o 文件，请使用 o 键。要使用 NASM 生成对象代码文件，请输入

### 程序 7.7

```assembly
        global half ; 或在 Edlinas 中使用 .globl
half:   PUSH ECX      ; ECX 被使用，因此压入。
        MOV ECX, [ESP + 8]
                                  ; 栈顶 + 2 个整数
        MOV EAX, 0
AGN:    INC EAX       ; 统计减法次数
        SUB ECX, 2    ; 反复减去 2
        JG AGN
        JZ DUN        ; 结果为偶数
        MOV EAX, 0    ; 不是偶数。
DUN:    POP ECX
        RET
```

```bash
linuxbox$ nasm -f elf half.asm
```

`-f elf` 开关指定对象代码文件的格式，在当前的 Linux 中为 elf。第 8 章将进一步讨论此格式。

程序 7.8 是一个调用函数 `half()` 的 C 程序，其汇编代码显示在程序 7.7 中。如果程序 7.8 保存在文件 `collatz.c` 中，则要对其进行编译并与 `half()` 链接，请对这两个文件使用 `gcc`

```bash
linuxbox$ gcc collatz.c half.o
```

## 7.4 递归

在递归中，计算的大部分工作由参数传递机制完成。

递归定义通常可以很容易地转换为计算上有效（即使效率不高）的程序。这通常使用斐波那契数列来说明。

```text
fib(k) =
   1                    如果 k < 2
   fib(k - 1) + fib(k - 2)   其他情况。
```

程序 7.9 展示了如何将此递归定义转换为 C 代码。在汇编语言中，只要记住除 EAX 外使用的寄存器必须被压入，就可以轻松编写此代码。程序 7.10 展示了如何仅使用 ECX 和 EAX 来实现。要从 C 测试此程序，可以使用像程序 7.11 这样的小型调用程序。要使用 Edlinas 测试此类程序，还需要初始化堆栈，如程序 7.3 的第一行所示。

### 程序 7.8

```c
main()
{
    int count,x,y;
    count = 0;

    printf("Enter a number:  ");
    scanf("%d", &x);

    while(x != 1)
    {
        count = count + 1;
        y = half(x); /* 这是子程序调用！ */
        if(y != 0)
            x = y;
        else
            x = 3*x + 1;
        printf("\n x = %d.", x);
    }
    printf("\n There were %d iterations.\n\n", count);
}
```

### 程序 7.9

```c
int fib(int k)
{
    int d;

    if(k < 2)
        d = 1;
    else
        d = fib(k-1) + fib(k-2);

    return d;
}
```

### 程序 7.10

```assembly
        global fib
fib:  PUSH ECX          ; 让我们可以访问 ECX
      MOV EAX, [ESP + 8]  ; 访问参数
      CMP EAX, 2          ; 如果 k < 2
      JAE ELS             ;
      MOV EAX, 1          ; 将返回值放入 EAX
      JMP DUN
ELS:  DEC EAX             ; 获取 k-1
      MOV ECX, EAX        ; EAX 将被覆盖！
      PUSH EAX            ; 传递 k-1 作为参数
      CALL fib            ; 获取 EAX 中的 fib(k-1)
      ADD ESP, 4          ; 清除参数
      DEC ECX             ; 获取 k-2
      PUSH ECX            ; 传递 k-2 作为参数
      MOV ECX, EAX        ; 将 fib(k-1) 放入 ECX
      CALL fib            ; 获取 EAX 中的 fib(k-2)
      ADD ESP, 4          ; 清除参数
      ADD EAX, ECX        ; 将两个部分结果相加
      POP ECX             ; 恢复原始值
      RET
```

### 程序 7.11

```c
main()
{
int x, y;
;
printf("Enter a number: ");
scanf("%d", &x);
;
y = fib(x);
;
printf("%d\n", y);
}
```

# 第 8 章. Linux 用户程序

在第 6 章开头提到，Linux 用户程序中使用的内存地址不是真实的内存地址。主要原因是 Linux 需要防止用户直接访问内存。参见图 8-1。

![](img/a3d6758e6e21b80b35e1b981ecbc1234_98_0.png)

Linux 是一个多任务系统。多任务系统拥有许多用户作业和一个操作系统，它们都在同时运行。在某个作业可以覆盖属于另一个作业的内存的机器上，多任务系统是不可能实现的。多任务需要内存保护。Linux 使用分页来实现内存保护系统。

分页最初被设计为一种节省内存的系统。Linux 也使用它来节省内存以及进行内存保护。分页通过拦截用户机器代码中遇到的每次内存访问来工作。换句话说，用户程序中的每个内存引用都会变成内存访问请求，该请求需要经由分页系统进行审批。这意味着分页对内存访问拥有控制权。为了实现这一点，处理器必须内置分页功能。

8086 和 80286 处理器都不支持分页。第一个支持分页的 Intel 处理器是 80386。

## 8.1 多任务

在多任务操作系统出现之前，计算机程序是按顺序执行的，即一个接一个。前面的程序未完成，后面的程序就无法开始执行。像这样按顺序运行程序的操作系统被称为*批处理*操作系统。多任务系统允许程序轮流使用处理器。一个名为*调度器*的操作系统程序充当裁判，强制用户程序相互让出控制权，即使它们尚未完成。在任何给定时刻，可能有许多用户程序正在轮流等待处理器时间。这些程序中的每一个都称为*任务*或*进程*。必须区分程序和进程，因为一个程序可以被多个用户同时调用多次。程序的每个独立实例就是一个进程。在 Linux 中，我们可以使用以下命令列出进程

```bash
linuxbox$ ps aux
```

或者，为了进行更详细的检查，我们可以探索 `/proc` 目录。

像 Linux 这样的多任务系统不断地对其处理器资源进行调配，将它们在进程之间传递。每当进程从处理器上被移除时，它都必须保存其当前状态。保存工作的一部分是由硬连线例程完成的，该例程在 x86 执行*任务切换*时运行。它将所有当前寄存器保存到内存中称为*任务状态段*的区域。任务状态段保存了当前未运行任务的冻结状态。每个任务都有自己独立的任务状态段。这些任务状态段使得从一个任务切换到另一个任务成为可能。**图 8-2** 展示了任务状态段的基本布局，包括所有通用寄存器的空间，以及一个称为 *CR3 寄存器* 的寄存器。图中未标记的部分在第 13 章中讨论。

**图 8-2. 任务状态段**

| 偏移量 | 值 |
| :----- | :----- |
| 0 | |
| 4 | |
| 8 | |
| 12 | |
| 16 | |
| 20 | |
| 24 | |
| 28 | CR3 |
| 32 | EIP |
| 36 | EFLAGS |
| 40 | EAX |
| 44 | ECX |
| 48 | EDX |
| 52 | EBX |
| 56 | ESP |
| 60 | |

