
| 706 | 252 | 4 | 962 | 3c2 a.out |

上述程序的结果表明，自动数组不会占据数据段或 BSS 段。

### 堆

堆是动态内存（通过 `malloc()` 等函数获取）的来源。随着在堆上分配内存，进程的地址空间会随之增长。堆通常紧接数据段的 BSS 区域之后。

### 栈

栈段是分配局部变量的地方。局部变量是指所有在函数体左大括号（或其他左大括号）内部定义的变量，且未定义为 `static`。此外，栈还用于存储函数参数，以及编译器生成的“不可见”账目信息、函数返回值以及表示从函数返回到调用者的返回地址。存储在栈上的变量在包含它们的函数返回时会“消失”；栈空间会被后续的函数调用重用。

# Linux 简介：安装与编程

当程序运行时，初始化的数据区、BSS 和堆区域通常被放置在一个连续的区域内：数据段。栈段和代码段与数据段分开。

### 18.2.12 strip 命令

该命令会丢弃对象文件中的符号。它修改对象文件本身，而不是写入带有不同名称的修改副本。它也可以用于归档文件。对于简单程序，这可以显著缩小可执行文件的大小。当然，在执行 `strip` 命令后，生成的可执行文件可以毫无困难地运行。

```bash
strip a.out
```

如果我们想用 `-o` 选项将结果写入另一个文件。

```bash
strip a.out -o a      # 文件 "a" 是剥离后的可执行文件
strip -s a.out -o a   # 从可执行文件中移除所有符号
strip -g a.out -o a   # 从可执行文件中移除调试信息
```

使用 `-l` 命令检查执行 `strip` 命令前后的可执行文件大小，以查看文件大小的变化。

`strip` 会从对象（可执行）文件中移除程序的变量和函数等符号。（当程序运行时，这些符号不会被加载到内存中。）这可以为大型程序节省大量的磁盘空间，但如果发生核心转储，则将无法进行调试。（在现代系统中，这并不值得费此周折；不要使用 `strip`。）即使删除了符号，文件仍然比加载到内存中的要大，因为对象文件格式保留了关于程序的额外数据，例如它可能使用的共享库（如果有）。

### 18.2.13 as 命令

也可以创建汇编代码（从 C 源码），然后生成对象代码，最后生成可执行代码。

```bash
gcc -S file.c           # 创建 file.s
as file.out -o file.o   # 创建对象文件 file.o
gcc file.o              # 创建可执行文件 a.out
```

通过在命令行提示符输入 `a.out` 即可执行该程序。

如果需要，可以在生成的汇编程序中添加一些汇编程序（下一章将详细讨论这一点）。

### 18.2.14 ld 命令

该命令会打印命令行给出的每个程序所需的共享库。此外，如果我们在命令行中指定了共享库名称，它会显示它使用了哪些共享库。

## 在 Linux 下编译 C 和 C++ 程序

例如 `ldd /usr/lib/lynx` 输出如下内容：

```
libncurses.so.5 => /usr/lib/libncurses.so.5 (0x40033000)
libssl.so.4 => /usr/lib/libssl.4 (0x40072000)
libcrypto.so.4 => /usr/lib/libcrypto.so.4 (0x400a7000)
libc.so.6 => /usr/lib/libc.so.6 (0x40200000)
libz.so.1 => /usr/lib/libz.so.1 (0x40198000)
libresolv.so.2 => /usr/lib/libresolv.so.2 (0x401a6000)
libssapi_krb5.so.2 => /usr/kerberos/lib/libssapi_krb5.so.2 (0x401b9000)
libkrb5.so.3 => /usr/kerberos/lib/libkrb5.so.3 (0x401cc000)
libcrypto.so.3 => /usr/kerberos/lib/libcrypto.so.3 (0x4022a000)
libcom_err.so.3 => /usr/kerberos/lib/libcom_err.so.3 (0x4023a000)
libdl.so.2 => /usr/lib/libdl.so.2 (0x4023c000)
```

`ldd /usr/lib/libncurses.so.5` 输出如下内容：

```
libc.so.6 => /lib/ts/libc.so.6 (0x40200000)
/lib/id-linux.so.2 => /lib/id-linux.so.2 (0x40000000)
```

### 18.2.15 创建动态可执行文件和静态可执行文件

默认情况下，`gcc` 创建动态可执行文件。通常，生成文件的大小比静态链接的要小。

# Linux 简介：安装与编程

```c
nullc:c (in function ff)
nullc:c:5:2: 在返回前未释放新的存储空间 p
检测到内存泄漏。本地分配的存储空间在最后一个引用丢失之前未释放。（使用 -mustfreeish 抑制警告）
nullc:4:27: 创建了新的存储空间 p
nullc:4:6: 变量 p 已声明但未使用
变量已声明但从未使用。在声明前使用 /*@unused@*/ 可以抑制该警告。（使用 -varuse 抑制警告）
nullc: (in function main)
nullc:9:6: 函数可能会修改观察者 p: p
使用 observer 声明的存储可能被修改。observer 存储不可被修改。（使用 -modobserver 抑制警告）
nullc:8:9: 存储 p 变为 observer
nullc:9:6: Observer 存储作为唯一参数传递：free (p)
observer 存储传递到了非 observer 引用。（使用 -observervents 抑制警告）
nullc:8:9: 存储 p 变为 observer
nullc:10:16: 变量 p 在释放后被使用
内存在释放后被使用（通过作为唯一参数传递或赋值给任何全局变量）。使用 -userleased 抑制警告）
nullc:9:6: 存储 p 已释放
nullc:11:2: 声明返回 int 的函数中没有返回的路径
在声明返回值的函数中，有一条路径没有 return 语句。这意味着执行可能会向下穿透，而不向调用者提供有意义的结果。（使用 -noret 抑制警告）
```

## 18.2.18 cc1 命令的使用

我们可以直接执行 `cc1` 命令。然而，它需要一个 "a.i" 文件，即预处理后的文件。它提供如下的统计数据。

```bash
/usr/lib/gcc-lib/i386-redhat-linux/cc1 a.i
```

### 输出

main

| 执行时间（秒） | usr | sys | wall |
| :--- | :--- | :--- | :--- |
| 预处理 | 0.01 (6 %) | 0.00 (0 %) | 0.01 (6 %) |
| 解析 | 0.01 (6 %) | 0.00 (0 %) | 0.01 (6 %) |
| 流程分析 | 0.01 (6 %) | 0.00 (0 %) | 0.01 (6 %) |
| 模式切换 | 0.01 (6 %) | 0.00 (0 %) | 0.01 (6 %) |
| 全局分配 | 0.01 (6 %) | 0.00 (0 %) | 0.01 (6 %) |
| 寄存器栈 | 0.01 (6 %) | 0.00 (0 %) | 0.01 (6 %) |
| 其他 | 0.01 (6 %) | 0.00 (0 %) | 0.01 (6 %) |
| **总计** | **0.16** | **0.01** | **0.17** |

## 在 Linux 下编译 C 和 C++ 程序

## 18.3 可变数量参数的函数

大多数年轻的 C 程序员都好奇，C 标准库开发者是如何编写出诸如 `printf()`、`scanf()` 这样接受可变数量参数的函数的。此外，当编写函数时，参数的数量未知或不是常量时，实现这样一个函数通常也是很有需要的。

```c
int f(int, ... ) {

}
```

为了实现这一点，必须包含 `<stdarg.h>` 头文件中定义的函数。这引入了一个新类型 `va_list`，以及三个操作该类型对象的函数，分别称为 `va_start`、`va_arg` 和 `va_end`。

在操作可变参数列表之前，必须调用 `va_start`，其原型为：

```c
void va_start(va_list ap, int parmn);
```

`va_start` 宏初始化 `ap` 以供函数 `va_arg` 和 `va_end` 后使用。`va_start` 的第二个参数 `parmn` 是函数定义中可变参数列表中最后一个参数的标识符（紧邻 `, ...` 之前的那个）。标识符 `parmn` 不能使用 `register` 存储类或作为函数声明，只能作为数组类型。

可以通过重复调用 `va_arg()` 来访问所提供的参数。这很奇特，因为返回的值是由宏的参数决定的。注意，这无法作为真正的函数来实现，只能作为宏。它的定义为：

```c
type va_arg(va_list ap, type type);
```

每次调用此宏都会从参数列表中提取下一个参数并作为指定类型的值（如果下一个参数不是指定的类型，则行为是未定义的）。在此需注意避免由算术转换引起的问题。对 `va_arg` 的第二个参数使用 `char` 或 `short` 总是错误的：这些类型会提升为带符号 `int` 或无符号 `int`，且 `float` 会转换为 `double`。注意，`char`、`short` 和无符号位域是否提升为 `unsigned int` 取决于实现，这增加了使用 `va_arg` 的复杂度。这可能是出现意想不到微妙之处的领域；只有时间会给出答案。

如果在没有后续参数的情况下调用 `va_arg`，行为也是未定义的。

当处理完所有参数后，应该调用 `va_end` 函数。这可以防止提供的 `va_list` 被进一步使用。如果没有调用 `va_end`，行为是未定义的。

以下示例展示了 `va_start`、`va_arg` 和 `va_end` 的用法：

```c
#include <stdlib.h>
#include <stdarg.h>
#include <stdio.h>

int AVG(int count, ...) {
    va_list ap;
    int i;
    va_start(ap, count);
    for (i = 0; i < count; i++) {
        i += va_arg(ap, int);
    }
    va_end(ap);
    return i;
}

int main() {
    printf("Average: %d\n", AVG(3, 10, 20, 30));
    exit(0);
}
```

# Linux 简介：安装与编程

在我们的这个小型示例中，很难注意到速度的提升，但当有几十个文件、每个文件包含几百行源代码时，节省的时间是非常显著的；更不用说更大的项目了。

## 18.5 main() 如何在 Linux 上执行的

在之前的章节中，我们解释了如何编译 C 语言程序以及其他工具的使用。在接下来的段落中，我们尝试回答一个问题：Linux 如何执行 `main()` 的？在 Linux 上，我们的 C 语言 `main()` 函数是由 GCC、libc 和 Linux 二进制加载器的协同工作执行的。建议也阅读“Linux 下的汇编语言”章节。我们将使用下面的简单 C 程序（"simple.c"）来演示它的工作原理。

```c
int main() {
  return(0);
}
```

```bash
gcc -o simple simple.c
```

为了查看可执行文件中包含的内容，让我们使用 "objdump"。关于该命令的更多将在后续章节讨论。

```bash
objdump -f simple
```

```
simple: file format elf32-i386
architecture: i386, flags 0x00000112:
EXEC_P, HAS_SYMS, D_PAGED
start address 0x0804482d0
```

从输出中我们可以理解该文件是 "ELF32" 格式，起始地址是 "0x080482d0"。

ELF 是 Executable and Linking Format（可执行与链接格式）的缩写。它是 Unix 系统使用的多种对象和可执行文件之一。对于我们的讨论，ELF 的有趣之处在于它的头部格式。每个 ELF 可执行文件都有如下 ELF头部。ELF 的细节在单独的章节中给出。

```c
typedef struct {
  unsigned char e_ident[EI_NIDENT]; /* 幻数和其他信息 */
  Elf32_Half e_type;      /* 对象文件类型 */
  Elf32_Half e_machine;    /* 架构 */
  Elf32_Word e_version;     /* 对象文件版本 */
  Elf32_Addr e_entry;      /* 入口虚拟地址 */
  Elf32_Off e_phoff;       /* 程序头表文件偏移 */
  Elf32_Off e_shoff;       /* 节头表文件偏移 */
  Elf32_Word e_flags;       /* 处理器特定标志位 */
  Elf32_Half e_ehsize;      /* ELF 头部大小（字节） */
  Elf32_Half e_phentsize;   /* 程序头条目大小 */
  Elf32_Half e_phnum;       /* 程序头表条目数量 */
  Elf32_Half e_shentsize;   /* 节头表条目大小 */
  Elf32_Half e_shnum;       /* 节头表条目数量 */
  Elf32_Half e_shstrndx;    /* 节头字符串表索引 */
  Elf32_Half e_edr;
};
```

在上面的结构中，“e_entry”字段是可执行文件的起始地址。

**起始地址 "0x080482d0" 是什么**

对于这个问题，让我们反汇编机器语言 "simple"。有几种工具可以反汇编可执行文件。我们也将使用 objdump 来此目的。

```bash
objdump --disassemble simple
```

输出有点长，但我们不会显示 objdump 的所有输出。我们的意图是查看地址 0x080482d0 处的内容。以下是输出：

```
080482d0 <_start>:
080482d0: 31 ed      xor %ebp,%ebp
080482d2: 5e        pop %esi
080482d3: 89 e1      mov %esp,%ecx
080482d5: 83 e4 f0    and 0xffffff,%esp
080482d8: 50        push %eax
080482d9: 54        push %esp
080482da: 52        push %edx
080482db: 68 20 84 08 04 push $0x08048420
080482e0: 68 74 02 04 push $0x08048274
080482e5: 51        push %ecx
080482e6: 56        push %esi
080482e7: 68 d0 83 04 08 push $0x080483d0
080482ec: e8 cb ff ff  call 080482bc <init+0x48>
080482f1: f4        hlt
080482f2: 89 f6      mov %esi,%esi
```

知道汇编语言的人可以理解可执行文件起始地址包含某种启动例程 "_start"。它清空寄存器，将某些值推入栈并调用一个函数。根据这条指令，栈帧应该看起来像这样：

# 栈顶

```
--------------------
0x080482d0
--------------------
esi
--------------------
ecx
--------------------
0x08048274
--------------------
0x08048420
--------------------
edx
--------------------
esp
--------------------
eax
```

如果你仔细查看 objdump 的反汇编输出，你可以发现推入栈的地址是函数的地址。总结一下：

- 0x080482d0: 这是我们 main() 函数的地址。
- 0x08048274: _init 函数。
- 0x08048420: _fini 和 _init 是初始化/终止函数。

让我们从反汇编中查找 0x080482bc：

```
080482bc: ff 25 48 95 04 jump *0x08049548
```

这里 `*0x08049548` 是一个指针操作，跳转到存储在 0x08049548 处的地址。

# 在 Linux 下编译 C 和 C++ 程序

## 栈布局

初始的栈布局非常重要，因为它提供了访问程序命令行环境的接口。以下是程序启动时栈上内容的图（图 18.6）：

| 列 | 描述 |
| :--- | :--- |
| argc | [dword] 参数计数器（整数） |
| argv[0] | [dword] 程序程序名（指针） |
| argv[1] | |
