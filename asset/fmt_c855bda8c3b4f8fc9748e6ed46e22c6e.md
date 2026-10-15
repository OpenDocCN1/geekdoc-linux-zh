
```text
Breakpoint 1 at 0x80483d5: file ctest.c, line 4.

(gdb) run

Starting program: /home/rich/ctest

Breakpoint 1, main () at ctest.c:4

4 printf("My first C program!\n");

(gdb) next

My first C program!

5 return(0);

(gdb) next

6 }

(gdb) next

0xb7e2268b in __libc_start_main () from /lib/tls/i686/cmov/libc.so.6

(gdb) next

Single stepping until exit from function __libc_start_main, which has no line number information.

Program exited normally.

(gdb) quit

$
```

首先，使用 `list` 命令显示源代码行号。接下来，使用 `break` 命令在 `main` 标签处创建断点，并使用 `run` 命令启动程序。

由于断点设置为 `main`，程序在 `main` 后的第一个源代码语句之前立即停止运行。`next` 命令用于步进到源代码的下一行，这会执行 C 代码中的 `printf` 语句。另一个 `next` 命令用于执行 C 代码中的 `return` 语句，这会终止应用程序。尽管应用程序已终止，但您仍在调试器中，可以再次运行程序。

# GNU `objdump` 程序

GNU `objdump` 程序是 `binutils` 包中另一个对程序员非常有用的实用程序。通常有必要查看编译器在目标代码文件中生成的指令代码。`objdump` 程序不仅会显示汇编语言代码，还会显示生成的原始指令代码。

本节描述 `objdump` 程序以及如何使用它来查看高级语言程序中的底层指令代码。

## 使用 `objdump`

`objdump` 命令行参数指定程序将对目标代码文件执行的功能以及它将如何显示检索到的信息。`objdump` 的命令行格式为

```text
objdump [ -a ] [--archive-headers] [ -b bfdname ] [--target=bfdname]

[ -C|--demangle[=style] ] [ -d|--disassemble ]

[ -D|--disassemble-all ] [ -z|--disassemble-zeroes ]

[ -EB|--endian=big ] [ -EL|--endian=little ] [ -f|--file-headers ]

[ --file-start-context ] [ -g|--debugging ]

[ -e|--debugging-tags ] [ -h|--section-headers ]|--headers ]

[ -i|--info ] [ -j section ] [--section=section ]

[ -l|--line-numbers ] [ -S|--source ]

[ -m machine ] [--architecture=machine ]

[ -M options ] [--disassembler-options=options ]

[ -p|--private-headers ] [ -r|--reloc ]

[ -R|--dynamic-reloc ] [ -s|--full-contents ]

[ -G|--stabs ] [ -t|--syms ] [ -T|--dynamic-syms ]

[ -x|--all-headers ] [ -w|--wide ]

[ --start-address=address ] [ --stop-address=address ]

[ --prefix-addresses ] [ --no-show-raw-insn ]

[ --adjust-vma=offset ] [ -V|--version ] [ -H|--help ]

objfile...
```

命令行参数在表 27-5 中描述。

表 27-5：`objdump` 参数

| 参数 | 描述 |
|---|---|
| `-a` | 如果有任何文件是归档文件，则显示归档头信息 |
| `-b` | 指定目标代码文件的目标代码格式 |
| `-C` | 将低级符号解混淆为用户级名称 |
| `-d` | 将目标代码反汇编为指令代码 |
| `-D` | 将所有节反汇编为指令代码，包括数据 |
| `-EB` | 指定大端目标文件 |
| `-EL` | 指定小端目标文件 |
| `-f` | 显示每个文件的头中的摘要信息 |
| `-G` | 显示调试节的内容 |
| `-h` | 显示每个文件的节头中的摘要信息 |
| `-i` | 显示所有架构和目标格式的列表 |
| `-j` | 仅显示指定节的信息 |
| `-l` | 用源代码行号标记输出 |
| `-m` | 指定反汇编时使用的架构 |
| `-p` | 显示特定于目标文件格式的信息 |
| `-r` | 显示文件中的重定位条目 |
| `-R` | 显示文件中的动态重定位条目 |
| `-s` | 显示指定节的完整内容 |
| `-$` | 显示与反汇编代码混合的源代码 |
| `-t` | 显示文件的符号表条目 |
| `-T` | 显示文件的动态符号表条目 |
| `-x` | 显示文件的全部可用头信息 |
| `--start-address` | 从指定地址开始显示数据 |
| `--stop-address` | 在指定地址停止显示数据 |

`objdump` 程序是一个非常通用的工具。它可以解码除目标代码文件之外的许多不同类型的二进制文件。对于 C 程序员来说，`-d` 参数是最有用的，因为它显示反汇编的目标代码文件。

## 一个 `objdump` 示例

使用示例 C 程序，你可以通过使用 `-c` 选项编译程序来创建一个要转储的目标文件：

```text
$ gcc -c ctest.c
```

这会创建一个 *object file*。目标文件包含程序生成的原始汇编语言代码，在链接成系统应用程序文件之前。此时你可以使用 `objdump` 程序来查看 C 程序生成的原始汇编语言代码：

```text
$ objdump -d ctest.o

ctest.o: file format elf32-i386

Disassembly of section .text:

00000000 <main>:
0: 8d 4c 24 04 lea 0x4(%esp),%ecx
4: 83 e4 f0 and $0xfffffff0,%esp
7: ff 71 fc pushl -0x4(%ecx)
a: 55 push %ebp
b: 89 e5 mov %esp,%ebp
d: 51 push %ecx
e: 83 ec 04 sub $0x4,%esp
11: c7 04 24 00 00 00 00 movl $0x0,(%esp)
18: e8 fc ff ff ff call 19 <main+0x19>
1d: b8 00 00 00 00 mov $0x0,%eax
22: 83 c4 04 add $0x4,%esp
25: 59 pop %ecx
26: 5d pop %ebp
27: 8d 61 fc lea -0x4(%ecx),%esp
2a: c3 ret
$ 
```

反汇编的目标代码文件显示了编译器创建的汇编语言助记符以及对应的指令代码。你可能会注意到，程序中引用的内存地址被清零了。这些值要等到链接器链接应用程序并准备好在系统上执行时才会确定。在此步骤中，你可以轻松看到执行这些功能的指令。

# GNU 分析器程序

GNU 分析器 (`gprof`) 是包含在 `binutils` 包中的另一个程序。该程序用于分析程序执行并确定应用程序中的“热点”。

应用程序热点是程序运行时需要最多处理时间的函数。它们通常是最数学密集的函数，但并非总是如此。I/O 密集型函数也会增加处理时间。

本节描述 GNU 分析器并演示如何在 C 程序中使用它来查看不同函数在应用程序中消耗了多少时间。

## 使用分析器

与其他工具一样，`gprof` 是一个命令行程序，使用多个参数来控制其行为。`gprof` 的命令行格式为

```text
gprof [ -[abcDhilIsTvwxyz] ] [ -[ACEeFfJjnNdpQqZ][name] ]

[ -i dirs ] [ -d [num] ] [ -k from/to ]

[ -m min-count ] [ -t table-length ]

[ --[no-]annotated-source[name] ]

[ --[no-]exec-counts[name] ]

[ --[no-]flat-profile[name] ] [ --[no-]graph[name] ]

[ --[no-]time-name ] [ --all-lines ] [ --brief ]

[ --debug[level] ] [ --function-ordering ]
```
