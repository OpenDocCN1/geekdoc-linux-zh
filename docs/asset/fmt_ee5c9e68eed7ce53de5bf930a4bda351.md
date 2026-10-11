
```asm
        global half ; or    .globl in Edlinas
half:
        PUSH ECX        ; ECX is used, so push it.
        MOV ECX,  [ESP +  8]
                        ; Stack top + 2 integers

        MOV EAX,  0
        INC EAX         ; Count the subtractions
AGN:
        SUB ECX,  2     ; Repeatedly subtract 2
        JG AGN          ;
        JZ DUN          ; It comes out even
        MOV EAX,  0     ; It's not even.
DUN:
        POP ECX
        RET
```

```bash
$ linuxbox$ nasm -f elf half.asm
```

`-f elf` 开关指定了目标代码文件的格式，在当前 Linux 中为 `elf`。第 8 章将进一步讨论此格式。

程序 7.8 是一个调用函数 `half()`（其汇编代码如程序 7.7 所示）的 C 程序。如果将程序 7.8 保存在文件 `collatz.c` 中，则要对其进行编译并与 `half()` 链接，请对这两个文件使用 `gcc`：

```bash
$ linuxbox$ gcc collatz.c half.o
```

## 7.4 递归

在递归中，计算的大部分工作由参数传递机制完成。

递归定义通常可以很容易地转化为计算上有效（即使不是最高效）的程序。这通常用斐波那契数来说明。

$$
fib(k) = \begin{cases}
1 & \text{if } k < 2 \\
fib(k - 1) + fib(k - 2) & \text{otherwise.}
\end{cases}
$$

程序 7.9 展示了如何将这种递归定义转化为 C 代码。在汇编语言中，只要我们记住除 `EAX` 外使用的寄存器必须被推送，就可以轻松地编写此代码。程序 7.10 展示了我们如何仅使用 `ECX` 和 `EAX` 来实现。要从 C 测试此程序，可以使用像程序 7.11 这样的小调用程序。要使用 Edlinas 测试此类程序，也需要像程序 7.3 的第一行所示那样初始化栈。

### 程序 7.8

```c
main()
{
    int count, x, y;
    count = 0;

    printf("Enter a number:  ");
    scanf("%d", &x);

    while(x != 1)
    {
        count = count + 1;
        y = half(x); /* This is the subroutine call! */
        if(y != 0)
            x = y;
        else
            x = 3*x + 1;
        printf("\n x = %d.", x);
    }
    printf("\n There were %d iterations.\n\n.",count);
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

```asm
    global fib
fib:    PUSH ECX          ; Gives us access to ECX
        MOV EAX, [ESP + 8]
                        ; Access parameter
        CMP EAX, 2          ; if k < 2
        JAE ELS           ;
        MOV EAX, 1        ; Put the return value in EAX
        JMP DUN
ELS:    DEC EAX           ; Get k-1
        MOV ECX, EAX      ; EAX will be overwritten!
```

`PUSH EAX` ; 将 `k-1` 作为参数传入

`CALL fib` ; 在 `EAX` 中获取 `fib(k-1)`

`ADD ESP, 4` ; 移除参数

`DEC ECX` ; 得到 `k-2`

`PUSH ECX` ; 将 `k-2` 作为参数传入

`MOV ECX, EAX` ; 将 `fib(k-1)` 放入 `ECX`

`CALL fib` ; 在 `EAX` 中获取 `fib(k-2)`

`ADD ESP, 4` ; 移除参数

`ADD EAX, ECX` ; 将两个部分结果相加

`POP ECX` ; 恢复原始值

`RET`

### 程序 7.11

```c
main()
{
  int x, y;
  ;
  printf("Enter a number:  ");
  scanf("%d", &x);
  ;
  y = fib(x);
  ;
  printf("%d\n", y);
}
```

# 第 8 章。LINUX 用户程序

在第 6 章开头曾指出，Linux 用户程序中使用的内存地址并非真实的物理内存地址。主要原因在于 Linux 需要防止用户直接访问内存。参见图 8-1。

![](img/165a4f637c5eaccb372f5a82ca458a05_98_0.png)

Linux 是一个多任务系统。多任务系统包含许多用户作业和一个操作系统，它们都在同时运行。在任何一个作业都可能覆盖其他作业所属内存的机器上，多任务系统是不可能实现的。多任务需要内存保护机制。Linux 使用分页 `Paging` 来实现内存保护系统。

分页最初被设计为一种节约内存的系统。Linux 也将其用于此目的以及内存保护。分页通过拦截用户机器代码中遇到的每次内存访问来工作。换句话说，用户程序中的每个内存引用都会转化为内存访问请求，这些请求必须经过分页系统的“办公桌”批准。这意味着分页系统获得了对内存访问的控制权。为了实现这一点，处理器内部必须集成了分页功能。

`8086` 和 `80286` 处理器都不支持分页。第一个支持分页的 Intel 处理器是 `80386`。

## 8.1 多任务

在多任务操作系统出现之前，计算机程序是按顺序执行的，即一个接一个地运行。在前面的程序完成之前，后面的程序无法开始执行。像这样串行运行程序的操作系统被称为*批处理*操作系统。多任务系统允许程序轮流使用处理器。一个称为*调度器*的操作系统程序充当裁判，强制用户程序即使未完成也要相互让出资源。在任何给定时刻，可能有许多用户程序正在轮流等待处理器时间。这些程序中的每一个都被称为*任务*或*进程*。必须区分程序和进程，因为一个程序可能被多个用户同时调用多次。程序的每个独立实例就是一个进程。在 Linux 中，我们可以使用 `linuxbox$ ps aux` 命令来列出进程。或者，为了进行更详细的检查，我们可以浏览 `/proc` 目录。

像 Linux 这样的多任务系统不断调节其处理器资源，将资源从一个进程传递给另一个进程。每次进程从处理器上被抢占时，它必须保存其当前状态。保存工作的一部分是由硬件例程完成的，当 x86 执行*任务切换*时，该例程会被执行。它将所有当前寄存器保存到内存中一个称为*任务状态段*的区域。任务状态段保存了当前未运行的任务的冻结状态。每个任务都有自己独立的任务状态段。这些任务状态段使得从一个任务切换到另一个任务成为可能。图 8-2 展示了任务状态段的基本布局，包括所有通用寄存器的空间，以及一个称为 `CR3 寄存器`的寄存器。图中一些未标记的空间将在第 13 章中讨论。

![](img/165a4f637c5eaccb372f5a82ca458a05_99_0.png)

## 8.2 分页

如第 4 章 4.2 节所述，x86 I/O 地址不经过处理。如果 `DX` 寄存器包含诸如 `FC30H` 这样的数值，那么执行 `IN AL, [DX]` 指令会直接将 `DX` 的 16 位内容应用到地址总线上。

`FC30H = 1111 1100 0011 0000`

因此在地址总线上我们得到：

高 16 位仅为 0。

另一方面，内存地址的处理方式并非如此直接。执行 `MOV AL, [0FC30H]` 不会导致相同的位被泵送到地址总线上。内存地址要经过一个两步过程。

1. 分段
2. 分页

只有在这个过程结束时，并且一切都正常的前提下，才会生成一个可以泵送到地址总线上的物理地址。由于 Linux 不使用分段，对其的讨论推迟到第 12 章。

### 8.2.1 虚拟内存
