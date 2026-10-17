
| 22 | .dynamic | DYNAMIC | 0000000000000628 | 00000628 | 00000000000001d0 | WA | 6 | 8 |
| 23 | .got | PROGBITS | 00000000000006ff8 | 000006ff8 | 0000000000000000 | WA | 0 | 8 |
| 24 | .got.plt | PROGBITS | 0000000000000200 | 00000200 | 0000000000000098 | WA | 0 | 8 |
| 25 | .data | PROGBITS | 0000000000000298 | 00000298 | 0000000000000010 | WA | 0 | 8 |
| 26 | .bss | NOBITS | 00000000000002c0 | 000002c0 | 0000000000000010 | WA | 0 | 32 |
| 27 | .comment | PROGBITS | 00000000000002a8 | 000002a8 | | | 0000000000000034000000000000001 MS 0 |
| 28 | .debug_ar | PROGBITS | 0000000000000000 | 000002dc | 0000000000000030 | |
| 29 | .debug_info | PROGBITS | 0000000000000000 | 0000210c | 000000000000005e | |
| 30 | .debug_abbrev | PROGBITS | 0000000000000000 | 00002ec | 0000000000000127 | |
| 31 | .debug_line | PROGBITS | 0000000000000000 | 00002813 | 0000000000000192 | |
| 32 | .debug_str | PROGBITS | 0000000000000001 | 000029a5 | 0000000000000593 | |
| 33 | .shstrtab | STRTAB | 0000000000000000 | 00003ae8 | 000000000000014c | |
| 34 | .symtab | SYMTAB | 0000000000000000 | 00002f38 | 0000000000000858 | |
| 35 | .strtab | STRTAB | 0000000000000000 | 00003790 | 0000000000000358 | |

标志含义：

`W` (写), `A` (分配), `X` (执行), `M` (合并), `S` (字符串), `l` (大)

`I` (信息), `L` (链接顺序), `G` (组), `T` (排除), `x` (未知)

`O` (操作系统处理) `o` (操作系统特定), `p` (处理器特定)

你看到上面输出中从索引 28 开始、以 `.debug_` 开头的五个节了吗？这些节包含了你通过 `-g` 选项请求的调试信息。调试信息以 DWARF 格式提供。

### DWARF

DWARF 代表“Debugging with Attributed Formats”（带属性格式的调试），是 GCC 用于存储调试信息的默认格式。

对于这本书来说，最有趣的 `.debug` 节是 `.debug_info`。你可以使用命令行工具 `objdump` 查看 `.debug_info` 的内容。

> http://dwarfstd.org/

### objdump

“`objdump` 显示关于一个或多个目标文件的信息。选项控制显示哪些特定信息。这些信息对于编写编译工具的程序员特别有用，而不是对于那些只想让程序编译并运行的程序员。”

要在 `_debug_info` 中显示 DWARF 信息，请在 `objdump` 中使用 "`dwarf-info`" 标志。运行此命令会产生大量的输出，这是我少数几次裁剪输出以关注特定信息的情况。

使用 `objdump` 查看 `_debug_info`

```bash
albino-lobster@ubuntu:~/antire_book/chap_2_compiler/trouble/build$ objdump --dwarf-info ./trouble

./trouble: file format elf64-x86-64

Contents of .debug_info section:

Compilation Unit @ offset 0:
Length: 0x5dc (32-bit)
Version: 4
Abbrev Offset: 0
Pointer Size: 8
<0>: Abbrev Number: 1 (DW_TAG_compile_unit)
<1> DW_AT_producer : (indirect string, offset: 0xafaf) GNU cc 5.4.0 20160909-mtune=generic -march=x86-64 -g -gnull -fstack-protector-strong
<10> DW_AT_language : 12 (ANSI C99)
<11> DW_AT_name : (indirect string, offset: 0x21d): /home/albino-lobster/antire_book/chap_2_compiler/trouble/src/trouble.c
<15> DW_AT_comp_dir : (indirect string, offset: 0x366): /home/albino-lobster/antire_book/chap_2_compiler/trouble/build
<19> DW_AT_low_pc : 0x400c06
<21> DW_AT_high_pc : 0x257
<29> DW_AT_stmt_list : 0x0
<1><5ba>: Abbrev Number: 21 (DW_TAG_variable)
<5bb> DW_AT_name : (indirect string, offset: 0x1aa): s_password
<5bf> DW_AT_decl_file : 1
```

## 第 2 章：编译器选项

```
DW_AT_decl_line : 11
DW_AT_type : <0x5cf5>
DW_AT_location : 9 byte block: (DW_OP_addr: 400f00)
```

`.debug_info` 段包含调试调试器所需的有用信息，但对于任何尝试将二进制文件归因于特定操作的人来说也有用。例如，在输出中，你可以看到源文件的完整路径（`/home/albino-lobster/antire_book/chap_2_compiler/trouble/src/trace.c`）、目录的完整路径（`/home/albino-lobster/antire_book/chap_2_compiler/trouble/build`）、声明的 C 版本（`GNU C 5.4.0 20160609`），甚至还有变量 `s_password` 定义的精确行号（`DW_AT_decl_line: 1`）。

这看起来信息量大得惊人，但在调试时确实非常有用。例如，考虑这个由 GDB 生成的回溯轨迹（back trace）。

## 在 GDB 中生成回溯轨迹

```bash
albino-lobster@ubuntu:~/antire_book/chap_2_compiler/trouble/build$ gdb .trouble
GNU gdb (Ubuntu 7.11.1-0ubuntu16.04) 7.11.1
输入 "show configuration" 查看配置详情。
有关报告报告，请参阅：
<http://www.gnu.org/software/gdb/bugs/.。
在网上查找 GDB 手册和其他文档资源：
<http://www.gnu.org/software/gdb/documentation/>。
需帮助请输入 "help"。
输入 "apropos" 搜索与 "word" 相关的命令
正在从 ..trouble... 读取符号
(gdb)
run
Starting program: /home/albino-lobster/antire_book/chap_2_compiler/trouble/trace.c
收到信号 SIGINT, Interrupt。
0x00007ffff7f1b54b0 in __accept_nocancel () at ../sysdeps/unix/syscall-template.S:84
    ../sysdeps/unix/syscall-template.S: 无此类文件或目录。
(gdb) bt
#0 0x00007ffff7b154b0 in __accept_nocancel () at ../sysdeps/unix/syscall-template.S:84
#1 0x0000000000040036 in main (p_argc=1, p_argv=0x7ffffffffdeb8) at /home/albino-lobster/antire_book/chap_2_compiler/src/trouble.c:59
```

注意回溯中包含了 `main()` 函数中的参数名 `p_argc` 和 `p_argv` 吗？这些是 Trouble 源代码中使用的精确名称。此外，在 `trouble.c` 中调用 `accept()` 的行号在回溯中也是可见（第 59 行）。得益于 Trouble 中存在 `.debug_info` 段，GDB 可以显示这些信息。

因为这些信息使得调试变得简单得多，每个程序员在编写程序时都会使用 `-g` 选项。然而，正如你所看到的，它对于逆向工程师来说很有用。

## 使用 Hexxdump 恢复 Bind Shell 密码

在上一节中，由于 `.debug_info` 中的 DWARF 信息，你看到了 `s_password` 变量声明的行号。如果你再次查看该输出，还可以看到 `s_password` 存储的地址。

`objdump` 中的 `s_password`

```
DW_AT_name      : (indirect string, offset: 0xaa): s_password
DW_AT_decl_file  : 1
DW_AT_decl_line : 11
DW_AT_type       : <0x5cf>
DW_AT_location   : 9 byte block: (DW_OP_addr: 400f00)
```

`s_password` 存储在虚拟地址 `0x400f00`。将虚拟地址转换为文件偏移量，你就可以使用 `hexdump` 提取 `s_password` 的内容。要将 `0x400f00` 转换为文件偏移，请找到它所在的程序头地址。

## 查看 Trouble 的程序头

```bash
albino-lobster@ubuntu:~/antire_book/chap_2_compiler/trouble/build$ readelf -l ./trouble
```

Elf 文件类型为 EXEC (可执行文件)

入口点 `0x400b10`

有 9 个程序头，从偏移量 64 开始

| Type | Offset | VirtAddr | PhysAddr | FileSize | MemSize | Flags | Align |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| PHDR | 0x0000000000000040 | 0x0000000000000040 | 0x0000000000000040 | 0x0000000000000000 | 0x0000000000000000 | | 0 |
| LOAD | 0x0000000000000018 | 0x0000000000000018 | 0x0000000000000018 | 0x0000000000000018 | 0x0000000000000018 | R | 8 |
| INTERP | 0x0000000000000028 | 0x0000000000000028 | 0x0000000000000028 | 0x0000000000000028 | R | 1 |
| LOAD | 0x000000000000000c | 0x000000000000000c | 0x000000000000000c | 0x0000000000000000 | | interpreter: /lib64/ld-linux-x86-64 | |
| LOAD | 0x00000000000000d4 | 0x00000000000000d4 | 0x00000000000000d4 | 0x0000000000000000 | E | 200000 |
| LOAD | 0x00000000000001e0 | 0x00000000000001e0 | 0x00000000000001e0 | 0x0000000000000000 | E | 200010 |
| DYNAMIC | 0x0000000000000298 | 0x00000000000002c0 | 0x00000000000002c0 | 0x0000000000000000 | RW | 200000 |
| DYNAMIC | 0x0000000000000128 | 0x0000000000000128 | 0x0000000000000128 | 0x0000000000000000 | RW | 8 |
| NOTE | 0x0000000000000254 | 0x0000000000000254 | 0x0000000000000254 | 0x0000000000000000 | R | 4 |
| GNU_EH_FRAME | 0x00000000000000f0 | 0x00000000000000f0 | 0x00000000000000f0 | 0x0000000000000000 | R | 4 |
| GNU_STACK | 0x0000000000000000 | 0x0000000000000000 | 0x0000000000000000 | 0x0000000000000000 | RW | 10 |
| GNU_RELRO | 0x00000000000001e0 | 0x00000000000001e0 | 0x00000000000001e0 | 0x0000000000000000 | R | 1 |

`s_password` 的虚拟地址落在第一个 `LOAD` 段的范围内，该范围涵盖 `0x400000` 到 `0x4010d4`。第一个 `LOAD` 段从偏移量 0 开始。因此，要计算 `s_password` 在文件中的偏移，你需要从 `0x4000f0` 减去 `0x400000`。这意味着你应该能在 `0xf0` 找到 shell 的密码。尝试使用 `hexdump` 显示它。

## 使用 hexdump 打印 s_password

```bash
albino-lobster@ubuntu:~/antire_book/chap_2_compiler/trouble/build$ hexdump -C -s 0xf0 -n 64 ./trouble
00000f00 54 47 4f 45 75 32 36 54 57 30 6b 31 62 39 49 65 |TGOu26TW0k1b9I
00000f10 58
```

## C语言中的 check_password() 调用

```c
if (check_password(password_input)) {
    close(client_sock);
    return EXIT_FAILURE;
}
```

注意 `password_input` 和 `client_sock` 出现在反汇编和 C 代码中了吗？另外，`p_password`（`check_password()` 唯一参数使用的名称）也出现在反汇编中。IDA 解析了 `.debug_info` 中的 DWARF 信息，并用这些更容易理解的变量名丰富了反汇编。对于逆向工程师来说，这非常有用，因为许多程序员会使用上下文变量名（例如，`password_input` 是存储用户提交密码的地方）。

## 移除调试信息

我希望我已经说服了你我们无法让逆向工程师访问调试信息。遗憾的是，移除调试信息非常简单。你只需要不在编译标志中提供 `-g` 选项即可。这将防止各种 `.debug` 段的生成。这意味着 GDB 和 IDA 也不会获得额外的变量信息来丰富它们的分析。

例如，如果没有 `-g`，GDB 用户将无法像本节之前那样使用 "`print`" 命令打印 `s_password`。遗憾的是，这并不意味着逆向工程师不能通过其他手段让 GDB 打印它，但我们稍后会讨论。

# 第二章：编译器选项

## 使用 GDB 在没有调试信息的情况下打印 s_password
