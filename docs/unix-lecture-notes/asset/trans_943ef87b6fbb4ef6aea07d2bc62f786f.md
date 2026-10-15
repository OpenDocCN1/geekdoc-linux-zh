

![](img/edd55012c780b4e999320d08ab27959e_377_0.png)

## 图 7.3：ELF 文件的重叠视图。

readelf 命令可用于检查可执行文件。

```
$ readelf [options] elffile ...
```

显示的信息取决于命令行上提供的选项。使用 -a，可提供所有信息。-h 选项以人类可读的形式显示 ELF 头的内容：

```
$ readelf -h /bin/bash
ELF Header:
Magic: 7f 45 4c 46 01 01 01 00 00 00 00 00 00 00 00
Class: ELF32
Data: 2's complement, little endian
Version: 1 (current)
OS/ABI: UNIX - System V
ABI Version: 0
Type: EXEC (Executable file)
Machine: Intel 80386
Version: 0x1
Entry point address: 0x805c7b0
Start of program headers: 52 (bytes into file)
Start of section headers: 733864 (bytes into file)
Flags: 0x0
Size of this header: 52 (bytes)
Size of program headers: 32 (bytes)
```

```
Number of program headers: 8
Size of section headers: 40 (bytes)
Number of section headers: 32
Section header string table index: 31
```

从此输出可以看出，ELF 头包含有关可执行文件格式的信息：32 位、2 的补码、面向 Intel 80386 的 UNIX System V。它还包含程序头的位置（文件中的字节 52）和节头表的位置（文件中的 733864 字节）。

file 命令使用 ELF 头来提供其输出：

```
$ file /bin/bash
/bin/bash: ELF 32-bit LSB executable, Intel 80386, version 1 (SYSV),
dynamically linked (uses shared libs), for GNU/Linux 2.6.9, stripped
```

你可以尝试一些可执行文件，看看能学到多少关于可执行程序结构的信息。

请注意，上面输出中可执行文件的入口点地址为 0x805c7b0。这是 bash 可执行文件中第一个可执行指令的地址。起始虚拟地址不是 0。在现代 UNIX 系统中，起始地址总是在 0x8048000 之后。更低的地址被保留供系统使用。其中的一个原因是，当程序在调试器下运行时，调试器将在较低地址中运行。

图 7.4 显示了来自 ELF 标准的一个版本的假设可执行文件的虚拟地址。请注意，在此示例中，文本段不在虚拟地址空间的开头，并且每个段根据需要进行填充，以便在 0x1000（4096）字节边界上对齐，因为页面大小为 4096 字节。还请注意，数据段和未初始化数据段跟在文本段之后。

## 7.6.8 显示虚拟内存边界的程序

在本节中，我们将借助我在进程间通信书籍 [1] 中找到并随后修改的程序来探索进程的虚拟地址空间。它显示其可执行映像的虚拟地址空间中不同组件的边界。该程序声明了以下类型的内存对象：

- 全局、已初始化指针变量：`cptr`
- 全局未初始化字符串：`buffer1`
- main 程序中的自动变量：`i`
- main 程序的参数：`argc`、`argv`、`envp`
- main 程序中的静态未初始化局部变量：`diff`
- 主函数 `main()`
- 非主函数 `showit()`

![](img/edd55012c780b4e999320d08ab27959e_379_0.png)

- 自动指针变量，动态分配：`buffer2`
- 非主函数中的自动变量：`num`

它以十六进制和十进制虚拟地址显示每个对象的位置。这些对象的位置将位于前面描述的文本、数据和栈段位置所指定的范围内。例如，未初始化的全局 `buffer1` 和已初始化的全局 `*cptr` 的位置将在数据段的第一和最后一个地址之间，一个在 bss 中，另一个不在。剩余的变量各自精确定位特定段的位置：“Hello World”、指针变量 `cptr` 本身、全局符号 `main()` 和 `showit()`，以及 `showit()` 中的局部变量 `num` 和 `buffer2`。局部变量的位置，理论上在运行时栈上，将显示该栈在虚拟内存中的位置。

三个外部整型变量 `etext`、`edata` 和 `end` 在 C 库中在全局范围内定义，可被任何 C 程序访问。它们是三个特定段的边界：

| 变量 | 描述 |
|---|---|
| `etext` | `etext` 的地址是程序文本之后的第一个位置。 |
| `edata` | `edata` 的地址是已初始化数据区域之后的第一个位置。 |
| `end` | `end` 的地址是未初始化数据区域之后的第一个位置。 |

`etext` 的值是对可执行映像大小的上限。已初始化和未初始化数据区域是常量和全局变量存储的区域。未初始化数据

> 它们可能被声明为宏。

