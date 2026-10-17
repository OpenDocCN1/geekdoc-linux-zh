
```
root@boota ltrace# strace ./a.out
execve("/a.out", ["/a.out"], /*44 vars */]) = 0
uname({sys="Linux", node="boota.boota.net", ...}) = 0
brk(0) = 0x04095f8
old_map(NULL, 4096, PROT_READ|PROT_WRITE,
MAP_PRIVATE|MAP_ANONYMOUS, -1, 0) = 0x04017000
open("/etc/ld.so.preload", O_RDONLY) = -1 ENOENT (No such
file or directory)
open("/etc/ld.so.cache", O_RDONLY) = 3
stat64(3, {st_mode=S_IFREG|0644, st_size=77871, ...}) = 0
old_map(NULL, 77871, PROT_READ, MAP_PRIVATE, 3, 0) = 0x04018000
close(3) = 0
open("/lib/libc.so", O_RDONLY) = 3
read(3,
#\177ELF/1\1\1\0\0\0\0\0\3\0\3\1\0\0\2\302...\n1024) = 1024
stat64(3, {st_mode=S_IFREG|0755, st_size=5634864, ...}) = 0
old_map(NULL, 1244290, PROT_READ|PROT_EXEC, MAP_PRIVATE, 3,
0) = 0x0402c002
mprotect(0x04152000, 38696, PROT_NONE) = 0
old_map(0x04152000, 24576, PROT_READ|PROT_WRITE,
MAP_PRIVATE|MAP_FIXED, 3, 0x1250000) = 0x04152000
old_map(0x04158000, 14120, PROT_READ|PROT_WRITE,
MAP_PRIVATE|MAP_FIXED|MAP_ANONYMOUS, -1, 0) = 0x04158000
close(3) = 0
munmap(0x04018000, 77871) = 0
getpid() = 32610
stat64(3, {st_mode=S_IFCHR|0620, st_rdev=makedev(136, 3,
..}) = 0
munmap2(NULL, 4096, PROT_READ|PROT_WRITE,
MAP_PRIVATE|MAP_ANONYMOUS, -1, 0) = 0x04018000
ioctl(1, TCGETS, 33840 output is ican echo ...) = 0
write(1, "Hello world\n", 12Hello) = 12
munmap(0x04018000, 4096) = 0
_exit(12) = ?
root@boota ltrace# 
```

如你所见，它为你展示了程序从执行到结束期间发生的情况。请查看 `strace` 的手册页以获取完整的命令行列表。`strace` 工具也可以用于性能收集活动，并可以记录程序中每个函数消耗的时间。更多信息请参阅 man页。

## 7.7 使用 GNU 二进制工具 (GNU Binary Utilities)

GNU binutils 是一个与处理库文件或获取不同类型二进制文件信息相关的工具包。这些工具的范围从在二进制文件中查找字符串、创建库文件、显示二进制文件信息到汇装二进制文件等。本节介绍了最常用的二进制工具。

### 7.7.1 使用 ar 工具

可以使用 `ar` 工具将文件存储到单个文件中。存储多个文件的文件称为归档（archive）。`ar` 程序保留了原始文件的权限、所有权和其他属性。如果需要，以后可以从归档中提取这些文件。该程序还在归档文件中创建一个索引，用于加速定位归档的组件（或成员）。

从开发的角度来看，`ar` 程序被用于创建函数库。这些库与其他对象文件一起使用以链接成一个可执行文件。这些库文件的约定命名格式为 `lib(name)`，其中 `name` 是用作库名的任何字符串。例如，名为 `common` 的库将存储在文件 `libcommon.a` 中。

当在命令行上使用选项时，`ar` 程序会执行以下任务之一：

- 从归档中删除文件（选项 d）
- 移动归档中的文件（选项 m）
- 打印归档中的文件列表（选项 p）
- 向归档中追加文件（选项 q）
- 如果归档中已存在文件，则通过替换来插入新文件（选项 r）
- 显示归档内容（选项 t）
- 从归档中提取文件（选项 x）

更多选项可以与常用选项结合使用以执行额外任务。在本节中，我们使用一些常用选项来展示 `ar` 程序在软件开发环境中的用法。

书中版本为 2.10.91。你可以使用 `-V` 选项显示系统上的当前程序版本。使用 `ar` 工具通常是因为它与动态加载器 `ld` 兼容。

```
[root@boota ar]# -V
Gnu 2.10.91
Copyright 1997, 98, 99, 2000, 2001 Free Software Foundation,
c.
此程序是免费软件，你可以根据 GNU 通用许可证的条款重新分发它。此程序不提供任何保证。
[root@boota ar]#
```

## 使用 GNU 二进制工具 (Binary Utilities)

```
common.o:
00000000 T msg
U printf
```

```
ftp.o:
00000000 T main
U msg
U printf
[root@boota make]#
```

对于每个符号，nm 显示符号的三个属性。

- 1. 值 (Value)
- 2. 类型 (Type)
- 3. 名字 (Name)

符号的值默认以十六进制字符显示。类型是一个字符，大写或小写均可。大写字母表示符号是全局的，小写字母表示符号是局部的如下行显示符号值为 00000000，类型为 T（表示符号位于代码段），其名称为 msg。

```
00000000 T msg
```

在 nm 命令的上述输出中，类型 U 表示符号是未定义的，不显示值。注意，函数 msg 在 `common.o` 中定义，但在归档的 `ftp.o` 成员中未定义。这是因为该函数定义在 `common.c` 文件中，并在 `ftp.c` 文件中引用。

通常，可执行文件的符号列表非常长。考虑以下显示 "Hello world" 字符串的文件：

```
#include <stdio.h>
main()
{
    printf("Hello world\n");
}
```

让我们编译此文件创建一个可执行文件 `a.out`。`a.out` 可执行文件中的符号列表所示：

```
[root@boota]# nm -s a.out
08049540 ? _DYNAMIC
0804951c ? _GLOBAL_OFFSET_TABLE_
080484e4 R _IO_stdin_used
08049510 ? _DTOR_END_
0804950c ? _DTOR_LIST_
08049518 ? _DTOR_END_
08049514 ? _DTOR_LIST__
```

## 第 7 章 • 杂项工具

```
08049508 ? __EH_FRAME_BEGIN_
08049508 ? __FRAME_END_
0804950e A _bss_start
    w _cxa_finalize@GLIBC_2.1.3
080494f8 D _data_start
    w _deregister_frame_info@GLIBC_2.0
08048480 t _do_global_ctors_aux
080483b0 t _do_global_dtors_aux
    w _gmon_start_
    U _lib_start_main@GLIBC_2.0
    w _register_frame_info@GLIBC_2.0
0804950e A _edata
080495f8 A _end
080484c0 ? _fp_hw
080484e0 R ? _init
080482e4 ? T _start
08048384 t call_gmon_start
08049504 d completed.1
080494f8 W data_start
08048410 t fini_dummy
08049508 d force_to_data
0804950d d force_to_data
08048420 t frame_dummy
08048384 t gcc2_compiled.
080483b0 t gcc2_compiled.
08048480 t gcc2_compiled.
080484c0 t gcc2_compiled.
08048460 t gcc2_compiled.
08048450 t init_dummy
080484b0 t init_dummy
08048460 T main
0804950e b object.2
08049500 d p.o
    U printf@GLIBC_2.0
[root@boota]# make]#
```

## 7.7.3 列出源文件中的行号

此命令配合 `-l` 选项非常有用。该选项还会显示使用这些符号的路径和行号。以下命令详细列出了 `lib-common.a` 文件中的符号。注意，它显示了源文件的路径和行号。这些信息用于调试过程。

```
[root@boota]# nm -s libcommon.a -l
```

归档索引：

msg in common.o

main in ftp.o

## GNU 二进制工具

common.o:

00000000 T msg /root/make/common.c:6

U printf /root/make/common.c:7

ftp.o:

00000000 T main /root/make/ftp.c:7

U msg /root/make/ftp.c:12

U printf /root/make/ftp.c:11

### 7.7.3.2 列出调试符号

当你使用调试选项编译程序时，文件中会插入许多用于调试的符号。在 nm 命令中使用 `-a` 选项也会显示调试符号。

请参阅 nm 的帮助页以获取所有内容的描述。

### 7.7.4 使用 strip 工具

`strip` 命令用于从对象文件中移除符号。由于可执行代码中不需要符号，这有助于减小体积。使用该命令也可以部分移除本地符号或所有符号。注意 `strip` 会修改对象文件；它不会创建文件。为了了解 `strip` 命令前后的对象文件大小，参考打印 "Hello world" 的 C 文件示例。可执行文件 `a.out` 的大小为 13640 字节。使用命令后减小到 3208 字节。

```
strip a.out
```

然而，在时间敏感的系统中，移除符号可能会导致问题。

### 7.7.5 使用 objcopy 工具

`objcopy` 工具的基本功能是将一个对象文件拷贝到另一个。该功能可以更改对象文件的格式。用于创建 S-record 或二进制文件。S-record 或二进制文件可用于嵌入系统的 ROM。以下命令将 ftp 文件（静态链接）转换为 S-record 的 ftp.S，可以使用 EPROM 下载到 ROM。

```
objcopy -O srec ftp.S
```

可以使用 `file` 命令查看输入和输出文件的类型。

## 第 7 章 • 杂项工具

```
[root@boota]# file ftp
ftp: ELF 32-bit LSB executable, Intel 8036, version 1, statically linked, stripped
[root@boota]# file ftp.S
ftp.S: Motorola S-Record; binary data in text
```

S-record 文件是 ASCII 格式，可以使用 `head` 命令显示前几行：

```
[root@boota]# head ftp.S
S080000667402E53C
S315088040904000010000047E5500CB
S3150880409000000200020020000050000B1
S315088045589E53EC0EE4500009EDB0F0
S030D08004C0E836610400C993
S3150880031ED5E89E1183AFE40542680208071
S3150880F06B884008516E0810104E80B010056
S315088010000F49F6558E53558000005B1C
S3150880113C282C05008B3C00000085C07402FF3
S3150880120DD08B5DEC59C38FE6909090909FE
[root@boota]#
```

以下命令创建 文件的二进制映像。二进制输出是可执行文件的内存映像，且移除了所有符号。

```
objcopy -O binary ftp
```

以下是显示新二进制文件类型的方法。

```
[root@boota]# file ftp
ftp: X11 binary font data, LSB first
```

在将对象文件转换为 S-record 或二进制文件之前，对它们进行 strip 是个主意。可以使用命令行选项 `--start-set` 和 `--adjust-start` 设置起始地址。

## 7.7.6 使用 objdump 工具

`objdump` 命令显示对象文件的信息。它也可以用于反汇编对象文件。可以使用不同的命令行选项显示对象文件的特定信息。

### 7.7.6.1 显示头部信息

以下命令显示二进制文件 `a.out` 的头部。

```
[root@boota]# objdump -f a.out
```

```
a.out:      file format elf32-i386
architecture: i386, flags 0x00000112:
EXEC_P,    HAS_SYMS, D_PAGED
start address 0x08048360
```

```
[root@boota]#
```

### 7.7.6.2 显示节 (Section)

以下命令显示 `a.out` 文件中所有节的信息。

```
[root@boota]# objdump -h a.out
```

```
a.out:      file format elf32-i386

Sections:
| Index | Name | Size | Off | LMA | VMA | Flags |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 0 | .interp | 0x13 | 0x0000000 | 0x08040000 | 0x08040000 | ALLOC, LOAD |
| 1 | .note.ABI | 0x20 | 0x0000010 | 0x08040010 | 0x08040010 | ALLOC, LOAD |
| 2 | .gnu.version | 0x24 | 0x0000030 | 0x08040030 | 0x08040030 | ALLOC, LOAD |
| 3 | .gnu.version_r | 0x30 | 0x0000050 | 0x08040050 | 0x08040050 | ALLOC, LOAD |
| 4 | .rel.got | 0x14 | 0x0000080 | 0x0804080 | 0x0804080 | ALLOC, LOAD |
| 5 | .rel.plt | 0x1c | 0x000009c | 0x080409c | 0x080409c | ALLOC, LOAD |
| 6 | .data | 0x1e0 | 0x00001c0 | 0x080401c0 | 0x080401c0 | ALLOC, LOAD |
| 7 | .bss | 0x200 | 0x00002d0 | 0x080402d0 | 0x080402d0 | BSS, alloc |
| 8 | .text | 0x29a4 | 0x0000360 | 0x08040360 | 0x08040360 | ALLOC, LOAD |
| 9 | .eh_frame | 0x1a0 | 0x00026a4 | 0x080426a4 | 0x080426a4 | ALLOC, LOAD |
| 10 | .rodata | 0x1f4 | 0x00027e8 | 0x080427e8 | 0x080427e8 | ALLOC, LOAD |
```

234

第 7 章 • 杂项数据

| CONTENTS | ALLOC | LOAD | DATA |

| :--- | :--- | :--- | :--- | :--- |

| CONTENTS, ALLOC, LOAD, DATA | .ctors | 0000008 | 080495c | 080495c | 0000050c 2** |

| CONTENTS, ALLOC, LOAD, DATA | .dtors | 0000008 | 08049514 | 08049514 | 00000514 2** |

| CONTENTS, ALLOC, LOAD, DATA | .got | 0000024 | 0804951c | 0804951c | 0000051c 2** |

| CONTENTS, ALLOC, LOAD, DATA | .dynamic | 00000a0 | 08049540 | 08049540 | 00000540 2** |

| CONTENTS, ALLOC, LOAD, DATA | .sbss | 0000000 | 080495e | 080495e | 000005e 2** |
