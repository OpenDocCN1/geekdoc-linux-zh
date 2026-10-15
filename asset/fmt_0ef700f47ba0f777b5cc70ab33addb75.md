
`ELF` 文件的每个部分都将在 `Linux` 和 `FreeBSD` 上运行；完整代码约 500 行，你可以从归档的 `Git` 仓库中下载。你需要安装操作系统的包仓库。在日常生活中，很少需要手动构建 `ELF`。这个练习仅用于说明。在现实世界中，开发者会使用这样的编译器，根据开发者提供的源代码和信息，以及计算机实际执行的汇编语言命令来生成 `ELF`。因此，我将使用汇编作为描述 `ELF` 格式的手段。图 1 提供了 `ELF` 文件的表示，并展示了它与加载到内存中的 `ELF` 的关系。

# `ELF` 文件的布局

`ELF` 文件包含四个部分：

- `ELF` 文件头
- 一个或多个程序头
- 一个或多个节头
- 一个或多个节

汇编语言的操作级别比 `C` 语言高，所以

# `ELF` 文件头

在列表 1 中，`ELF` 文件头为初学汇编语言的人描述了，`db`

# 列表 2: 程序头

```
01 macro PROGRAM_HEADER,type,offset,version,
address,physical,size,mem_size,alignment
02 {
03 ; 段段类型 = 常见类型
04 ; PT_NULL = 0; PT_LOAD = ;
05 ; PT_DYN = 2; PT_INTERP = 3;
06 ; PT_HDR = 6;
07 ; 类型
08 ; 权限 = 读/写/
09 ; 可执行：一个
10 ; 来自 PF_H = 0x; PF_W =
11 ; PF_X = 0xl的值。
12 dd permissions
13 ; 文件中的偏移量。
14 dq offset
15 ; 运行时偏移量。
16 dq virtual_address
17 ; 未命名；设置为 0。
18 dq physical_address
19 dq disk_size
20 dq mem_size
21 dq alignment
22 ; 以下变量让我们在定义
     ; 程序头时像... 那样
23 PROGRAM_HEADER = CPROGRAM_HEADER + 1
24 }
```

# 深度解析

## `ELF` 格式

意味着“删除字节”，“意味着“清除字（两个）”，以此此类推；`rept { 重复包含的代码 n 次 }`

如你从列表 1 所示，`ELF` 文件头包含了描述程序上下文的通用信息。例如，文件头包含了类（32 位或 64 位）、字节序、操作系统、文件类型（可执行、可重定位、对象、共享库）以及处理器。`ELF` 文件头还为程序头和节头留出了空间，你将在本文中学习这些。

# 表 1: 常见节的名称

| 名称 | 描述 |
| --- | --- |
| `Interp` | （可能的）以空字符结尾的字符串，请求程序解释器（运行时链接器/加载器）。在 `Linux` 上，这将会是 `/lib64/ld-linux.x86-64.so.2`；在 `FreeBSD` 上，它是 `/lib/elf.so.1`。 |
| `gnu.hash` | 当动态链接器合并进程中的对象时，它需要快速发现每个对象中存在哪些特定符号。`GNU` 哈希是一个用于实现此点的哈希表。 |
| `.dynsym` | 需要重定位的符号列表。每个条目应该是一个空符号。对于我们提供的符号，我们包含了符号存储位置的节索引以及符号的虚拟地址。 |
| `dynstr` | 以空字符结尾的字符串，通常是文件中链接的函数和库的。在 `Linux` 中，使用 `.strtab` 并以空字符开始和结束。 |
| `.rela` | 每个重定位包含静态链接器需要填充的地址，以及相应符号的偏移量，以及重定位类型（如使用 `R86_64_JMP_SLTO`）的常量地址。 |
| `.text` | 程序的实际代码。 |
| `got.plt` | 在相同地址空间加载的其他 `ELF` 映像的函数地址。 |
| `.bss, .dynamic` | 这些节包含了有助于动态链接的字对。 |

# `ELF` 文件格式

## 节的内容

此示例并不需要表 1 中描述的所有节，但对 `.text`、`.plt`、`.gdt` 和 `.rel_a` 节的简要描述将让你了解这些节如何构建 32 位有符号值的结构。

> `.text` 节执行程序列举 (4) 中的程序可执行代码。该代码调用 `puts` 将字符串打印到终端，并将控制权交还操作系统。

`x86-64` 指令通常使用相对寻址。这意味着，例如，一个 `CALL` 的编码取决于距离调用处的距离（目标地址被编码）。这使得无法对一个无法适应在 32 位内的地址或函数调用进行编码。解决方案是使用过程链接表 (`plt`) 和全局偏移表 (`got`)，它们在 `.plt` 和 `.gdt` 节中描述。`PLT` 包含该二进制文件本地的本地地址，因此其所有列表都可以通过 32 位相对调用进行访问。它使用 `JMP` 指令跳转到真实函数，该地址由动态链接器放置在 `GOT` 中。`PLT` 和 `GOT` 还允许动态链接器仅在需要时才解析地址，从而加速加载过程。

列表 5 定义了 `.plt` 和 `.gdt` 节的一些特征。我们需要使用 `.rel_a` 节来定义静态重定位的宏，使用之前提到的 24 字节结构（列表 6）。

## 列表 6：重定位

```
01 macro RELOCATION symbol_name plane
02 :
03 ; 链接器必须填充的 qword 地址
04 ; must fill in
05 dq LOAD_BASE + plane + symbol_name@got
06 ; 符号索引和类型，编码在
07 ; 单个字中；
08 dq (symbol_name# shl 32) or R_X86_64_JMP_SL
09 ; 无地址。
10 dq 0
11 )
12 ...
13 ...
14 ...
15
16 ; 实际重定位
17 SECTION_REL_PLT:
18
19 RELOCATION count,index value
20 RELOCATION exit,PLANES
```

## 导出与导入符号

可执行文件通过链接导出符号 `environment` 和 `_start`，并导入 `puts` 和 `exit`。在列表 7 中，我将这些声明封装在一些便利宏中。

## 列表 7：导入与导出符号

```
01 macro EXPORT count,index value 23 db (STR_GLOBAL shl 4) + ((ST_FUNC and Oxf))
02 24 ; 我们不再为该符号提供更多
03 25 信息，因为它本身
04 ; 符号的可见性和类型 26 ; 已在另一个 ELF 对象中定义。
05 ; 编码在字节中：\27 db
06 (STR_GLOBAL shl 4) + ((ST_FUNC and Oxf))
07 ; 使用“其他”字段。\28 db
08 db 29 dq
09 ; 符号所在的节。30 dq
10 index 31 name#index = CSMBOL
11 ; 32 CSMBOL = CSMBOL + 1
12 ; 符号的虚拟地址。\34 dq
13 value 35 ...
14 ; 符号大小。\36 ...
15 dq 8 37 dq
16 name#index = CSMBOL 38 SECTION_DYNSYM
17 ) 39 BEGIN_SYMBOLS
18 40 NULL_SYMBOL
19 macro IMPORT_FUNCTION name 41 IMPORT_FUNCTION puts
20 42 IMPORT_FUNCTION exit
21 ; 43 EXPORT_OBJECT environ, LINK_BSS, LOAD_BASE + PLANES + SLOT_environ
22 dd name 44 EXPORT_OBJECT _program, LINK_DATA, LOAD_BASE + PLANES + SLOT__program
```
