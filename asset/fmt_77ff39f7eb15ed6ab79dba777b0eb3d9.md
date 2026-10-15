
有 39 个节头，起始偏移为 `0xdf0`。

| Nr | Name | Type | Addr | Off | Size | Flags |
|---|---|---|---|---|---|---|
| 0 | NULL | | 000000 | 000000 | | 0 |
| 1 | .interp | PROGBITS | 0008154 | 000150 | A | 1 |
| 2 | .note.ABI | NOTE | 0008168 | 000168 | A | 4 |
| 3 | .note.num | NOTE | 0008188 | 000188 | A | 4 |
| 4 | .hash | HASH | 000818c | 0001fc | A | 5 |
| 5 | .dynym | DYNM | 0008428 | 000428 | A | 6 |
| 6 | .dynstr | | 0008888 | 000828 | A | 1 |
| 7 | .gnu.version | VERSYM | 0008a9a | 0000a9 | A | 5 |
| 8 | .gnu.version_r | VERNEED | 0008b2b | 00002b | A | 6 |
| 9 | .rel.pt | REL | 0008b48 | 00004b | A | 5 |
| 10 | .init | PROGBITS | 0008d60 | 0000d0 | A | 0 |
| 11 | .plt | PROGBITS | 0008d78 | 000d78 | A | 4 |
| 12 | .text | PROGBITS | 00099b0 | 0001b0 | A | 4 |
| 13 | .fini | PROGBITS | 000239a | 0001b9 | A | 4 |
| 14 | .rodata | | 00023b0 | 0001b0 | A | 8 |
| 15 | ARM.extab | PROGBITS | 0025480 | 0148d0 | A | 1 |
| 16 | ARM.exidix | ARM_EXIDX | 0025488 | 0148d8 | AL | 12 | | 4 |
| 17 | eh_frame_hdr | | 0025488 | 0148d8 | 00002c | A | 4 |
| 18 | eh_frame | PROGBITS | 00254b4 | 01d4b4 | 00007c | A | 4 |
| 19 | init_array | INIT_ARRAY | 0002d50 | 01d530 | WA | 4 |
| 20 | fini_array | FINI_ARRAY | 0002d54 | 01d534 | WA | 4 |
| 21 | jcr | PROGBITS | 0002d58 | 01d538 | 4 | WA | | 4 |

> 记得使用你交叉版本的 `strip`，例如 `pp_82xx-strip`。

# 列表 15-1 继续

| 节 | 类型 | 起始 | 虚拟 | 大小 | 标记 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| [22] .dynamic | DYNAMIC | 0002d53c | 01d53c | 0000d | 08 WA 6 0 4 |
| [23] .got | PROGBITS | 0002d60c | 01d60c | 00018 | 04 WA 0 0 4 |
| [24] .data | PROGBITS | 0002f728 | 01d728 | 003c0 | 00 WA 0 8 |
| [25] .bss | NOBITS | 0002ae8 | 01dae8 | 00018 | 08 WA 0 0 4 |
| [26] .comment | PROGBITS | 00000000 | 01dae | 000940 | 00 O 0 1 |
| [27] .debug_ranges | PROGBITS | 00000000 | 01e428 | 0004a0 | 00 O 0 8 |
| [28] .debug_pubnames | PROGBITS | 00000000 | 01e8c | 001laee | 00 O 0 1 |
| [29] .debug_info | PROGBITS | 00000000 | 020376 | 01d327 | 00 O 0 1 |
| [30] .debug_abbrev | PROGBITS | 00000000 | 034099 | 0022de | 00 O 0 1 |
| [31] .debug_line | PROGBITS | 00000000 | 03e6f7 | 0037a4 | 00 O 0 1 |
| [32] .debug_frame | PROGBITS | 00000000 | 03a420 | 003380 | 00 O 0 4 |
| [33] .debug_str | PROGBITS | 00000000 | 03d7a0 | 000679 | 00 O 0 1 |
| [34] .note.gu.arm.id | NOTE | 00000000 | 03de19 | 00001c | 00 O 0 1 |
| [35] .debug_ranges | PROGBITS | 00000000 | 03de35 | 000018 | 00 O 0 1 |
| [36] .shstrtab | STRTAB | 00000000 | 03de43 | 000183 | 00 O 0 1 |
| [37] .symtab | SYMTAB | 00000000 | 03e5e4 | 0004b0 | 18 38 77 4 |
| [38] .strtab | STRTAB | 00000000 | 0431b8 | 0021bf | 00 O 0 1 |

标记含义：
W (写), A (分配), x (执行), M (合并), S (字符串)
I (信息), L (链接顺序), G (组), o (未知)
O (需要额外的操作系统处理) o (操作系统特定), p (处理器特定)
$

从列表 15-1 中你可以看到，许多节都包含调试信息。名为 `.comment` 的节包含了超过 2KB (`0x940`) 的信息，这些信息对于应用程序的运行是并不是必需的。该示例文件的大小（包含调试信息）超过 275KB，如下所示：

```
$ ls -l websdom

-rwxrxr-x 1 chris chris 283511 Nov 8 18:48 websdom
```

如果我们使用 `cross-strip` 工具对该文件进行剥离，我们可以将其缩小以保留目标机上的资源。列表 15-2 显示了结果。

# 列表 15-2 剥离目标应用程序

```
$ xscale-be_strip -s -R .comment -o websdom-stripped websdom

$ ls -l websdom*

-rwxrxr-x 1 chris chris 283491 Apr 9 09:19 websdom

-rwxrxr-x 1 chris chris 123156 Apr 9 09:22 websdom-stripped

$
```

# 15.2 远程（交叉）调试

在这里，我们从执行文件中剥离符号调试信息和 `.comment` 节。我们使用 `-o` 命令行开关来指定剥离后二进制文件的名称。你可以看到，剥离后的二进制文件小于原始大小的一半。当然，对于较大的应用程序，这种空间节省可能会更加显著。一个带有调试信息的最新编译 Linux 内核大于 18MB。在剥离后，生成的二进制文件略大于 2MB！

要以这种方式进行调试，你将剥离版本的二进制文件放在目标系统上，而在工作站上保留一个包含调试信息的未剥离副本。你使用目标板上的 `gdbserver` 为开发工作站提供接口，你在工作站上运行完整版本的 GDB（当然，是交叉版本的 `gdb`）。

## 15.2.1 gdbserver

使用 `gdbserver` 允许你在工作站而不是目标平台上运行 GDB。这种配置具有显而易见的优势。首先，开发工作的 CPU 性能、内存和存储通常远大于嵌入式平台。此外，应用程序的源代码通常位于开发工作站而不是嵌入式平台。`gdbserver` 是一个运行在目标板上的小型程序，允许对板上的进程进行调试。它在目标板上被调用，需要指定要调试的程序以及 GDB 监听连接的 IP 地址和端口。列表 15-3 显示了在目标板上启动 `gdbserver` 的序列。

# 列表 15-3 在目标板上启动 gdbserver

```
$ gdbserver localhost:2001 websdom-stripped

Process websdom-stripped created; pid = 197

Listening on port 2001
```
