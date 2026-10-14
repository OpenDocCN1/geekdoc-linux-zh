
然而，手动检查二进制文件被证明是一项复杂且模糊的任务。库有助于访问 ELF 文件中的信息，提供了分析函数。要使用这些函数，必须包含文件 `<libelf.h>` 并在编辑链接时添加选项 `-elf`。

# 3.4 库

## 3.4.1 库的功能

库构成了将几个对象文件聚集的简单手段。发现两种类型的库：

- 静态：在链接编辑期间，库代码与可执行代码集成；
- 动态：库代码在程序执行时加载。

动态库极度地减少了磁盘空间，但依赖内存，因为动态内存只加载一次，且代码可以在所有需要它的应用程序之间共享。最后，当加载动态库时，内核负责映射该库。

## 3.6.1.1 通过名称识别的系统调用实现

系统调用是通用的并被分配有一个唯一的编号。该编号可以在 `asr/unististd.h` 文件找到。例如，系统调用 `open` 的编号为 5。该名称定义在汇编文件 `arch/i386/kernel/entry.S` 中，名为 `sys_open`。

C 库提供了执行系统调用的函数，这些函数带有系统调用的名称。要执行系统调用，只需要调用相应的函数即可。

在内核源码程序中，系统调用采用以下标准形式：

```c
asmlinkage int sys_name(argument list)
{
    /* System call code */
}
```

参数数量必须在 0 到 5 之间。关键字 `asmlinkage` 是定义在 `linux/linkage.h` 文件中的宏：

```c
#ifdef _cppplus
#define asmlinkage extern "C"
#else
#define asmlinkage
#endif
```

当进程执行系统调用时，它会调用 C 库中相应的函数。该函数处理参数并将进程切换到内核态。

对于 x86 架构，到内核态的转换是通过以下方式：

- 系统调用参数被放置在特定的处理器寄存器中；
- 通过调用 `0x80` 软件中断触发陷阱；
- 此陷阱触发到内核态的转换：进程执行源文件 `arch/i386/kernel/entry.S` 中定义的系统调用函数 `sys_call`；
- 该函数使用系统调用编号（传输到 `eax` 寄存器）作为 `sys_call_table` 表的索引，该表包含了系统调用地址，并调用与系统调用对应的内核函数；
- 当该函数返回时，`sys_call` 返回给调用者；随后进程返回用户态。

尽管此文件位于专门针对 x86 架构的子目录下，但也存在其他架构的文件。

# 在 Linux 下开发

## 3.6.1.2 创建系统调用

为了完全理解系统调用的工作原理，可以创建一个。要创建的系统调用包含三个参数，对前两个参数进行乘法，并将结果放在第三个参数中。

首先，需要“声明”该系统调用，并为它分配一个编号。Linux 2.0 版本包含 164 个系统调用。因此，系统调用 `show_mult` 的编号为 164（而第一个系统调用 `setup` 的编号为 0）。为了声明要创建的新调用，必须在 `include/asm/unistd.h` 行中添加以下内容：

```c
/* Kernel system calls *
#define _NR_sched_get_priority_min 160
#define _NR_sched_r_get_interval 161
#define _NR_nanosleep 162
#define _NR_mremap 163
```

```c
/* System calls added */
#define _NR_show_mult 164
```

然后，在文件 `arch/i386/kernel/entry.S` 中：

```asm
/* Kernel SYMBOL calls */
.long SYMBOL_NAME(sys_sched_get_priority_min) /* 160 */
.long SYMBOL_NAME(sys_sched_rr_get_interval)
.long SYMBOL_NAME(sys_nanosleep)
.long SYMBOL_NAME(sys_mremap)
```

```asm
/*Initial value of number of calls */
/* /.space (NR_syscalls-163)*4 */
```

```asm
/* System name added */
.long SYMBOL_NAME(sys_show_mult)
.space (NR_syscalls-164)*4
```

在此阶段，所有允许执行系统调用的链接已就绪，剩下的工作就是实现它。系统调用代码可以集成到内核文件 `kernel/sys/s.c` 中，该文件收集了许多系统调用。添加的代码如下：

```c
asmlinkage int sys_show_mult(int x, int y, int *res)
{
    int error
```

或者在架构的 `entry.S` 文件中。

### 内核操作

```c
int compute

/* Checking the validity of the variable res */
error = verify_area(VERIFY_WRITE, res, sizeof(*res));
if (error)
    return error;

/* calculation of the value */
compute = x*y;

/* copy into the user memory zone for the result */
put_user(compute, res);

printf("Value computed : %d x %d = %d \n", x, y, compute);

/* Call terminated */
return 0;
```

一旦内核重新编译并重启机器，就可以测试已实现的系统调用。为了使用此系统调用，需要声明一个运行它的函数。事实上，该函数在 C 库中并不存在，需要显式声明它。头文件 `syscall.h` 中声明了几个有助于定义此类函数的宏指令。当系统调用接受三个参数时，必须使用宏指令 `syscall3`。

### showmult.c

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

/* showmult.c */
int syscall3(int x, int y, int *res)
{
    int error;

    /* Checking the validity of the variable res */
    error = verify_area(VERIFY_WRITE, res, sizeof(*res));
    if (error)
        return error;

    /* calculation of the value */
    compute = x*y;

    /* copy into the user memory zone for the result */
    put_user(compute, res);

    printf("Value computed : %d x %d = %d \n", x, y, compute);

    /* Call terminated */
    return 0;
}

int main()
{
    int res;
    int ret;

    ret = syscall3(_NR_show_mult, 5, 6, &res);
    if (ret == 0) {
        printf("Result: %d\n", res);
    } else {
        printf("Error: %d\n", ret);
    }
    return 0;
}
```

## 3.6.1.3 返回码

内核在执行系统调用会检测错误。在这种情况下，返回 -1。为了让调用进程确定原因，C 库提供了全局变量 `errno`。该变量包含错误码。

头文件 `<errno.h>` 定义了表示错误的众多常量。在后续章节中将提供可能返回的错误码详细列表。

变量 `_sys_nerr` 错误码的数量。`_sys_errlist` 包含描述错误的字符串。

## 3.6.1.2 工具函数

内核包含现在需要介绍的一些工具函数。虽然这些函数在后面的章节会有描述，但我们需要知道它们是如何工作的才能理解内部函数的描述。

## 3.6.1.3 地址空间操作

内核态进程的地址空间与用户态不同。因此，无法直接访问作为参数传递给系统调用的数据。Linux 提供了几个访问这些数据的函数：

```c
verify_area(int type, const void *addr, unsigned long size);
```
