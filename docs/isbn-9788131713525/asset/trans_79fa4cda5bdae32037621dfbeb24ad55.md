
## 第 15 章
### 嵌入式 Linux 应用程序调试

**本章内容**

- 目标机调试  第 400 页
- 远程（交叉）调试  第 400 页
- 使用共享库进行调试  第 405 页
- 多任务调试  第 411 页
- 其他远程调试选项  第 417 页
- 本章摘要  第 419 页

在上一章中，我们探讨了 GDB 在调试内核代码以及驻留在 Flash 中的代码（例如引导加载程序代码）时的用法。在本章中，我们将继续介绍 GDB 在用户空间应用程序代码调试中的应用。我们将扩展对远程调试及其在此特殊调试环境中使用的工具和技术的内容。

## 15.1 目标机调试

我们已经在第 13 章“开发工具”中探讨了几个重要的调试工具。`strace` 和 `ltrace` 可用于观察和表征进程的行为，并常常能定位问题。`dmalloc` 有助于隔离内存泄漏并剖析内存使用情况。`ps` 和 `top` 都可用于检查进程状态。这些相对较小的工具旨在直接在目标硬件上运行。

在嵌入式系统上调试 Linux 应用程序代码有其独特的挑战。你的嵌入式目标机上的资源通常有限。RAM 和非易失性存储的限制可能会阻止你运行基于目标机的开发工具。你可能没有以太网端口或其他高速连接。你的目标嵌入式系统可能没有图形显示器、键盘或鼠标。

这正是你的交叉开发工具和 NFS 根挂载环境可以发挥巨大作用的地方。许多工具，尤其是 GDB，其架构设计允许在你的开发主机上执行，同时实际调试远程目标机上的代码。GDB 可用于交互式调试你的目标代码，或执行由应用程序崩溃生成的核心文件的事故后分析。我们在第 13 章中介绍了应用程序核心转储分析的细节。

## 15.2 远程（交叉）调试

交叉开发工具主要是为了克服嵌入式平台的资源限制而开发的。一个使用符号调试信息编译的中尺寸应用程序很容易超过几兆字节。通过交叉调试，繁重的任务可以在你的开发主机上完成。当你在开发主机上调用你的 GDB 交叉版本时，你传入一个带有符号调试信息的 ELF 文件。在目标机上，你可以剥离 ELF 文件中所有不必要的调试信息，以使生成的映像保持最小尺寸，没有任何理由不这样做。

> 请记住使用你的 `strip` 交叉版本，例如 `ppc_82zx-strip`。

我们在第 13 章介绍了 `readelf` 实用工具。在第 14 章“内核调试技术”中，我们使用它检查带有符号调试信息编译的 ELF 文件中的调试信息。列表 15-1 包含了一个针对 ARM 架构编译的相对较小的 Web 服务器应用程序的 `readelf` 输出。

### 列表 15-1
#### 示例程序的 ELF 文件调试信息

```
$ xscale_be-readelf -S webdemo
There are 39 section headers, starting at offset 0x3dfd0:

Section Headers:
 [Nr] Name          Type            Addr     Off    Size   ES Flg Lk Inf Al
 [ 0]               NULL           00000000 000000 000000 00      0   0  0
 [ 1] .interp       PROGBITS       00000154 000154 000013 00      A   0  1
 [ 2] .note.ABI-tag NOTE           00000168 000168 000020 00      A   0  4
 [ 3] .note.numapolicy NOTE         00000188 000188 000074 00      A   0  4
 [ 4] .hash         HASH           000001fc 0001fc 00002c 04      A   5  0  4
 [ 5] .dynsym       DYNSYM         00000828 000428 000460 10      A   6  1  4
 [ 6] .dynstr       STRTAB         00000888 000888 000211 00      A   0  0  1
 [ 7] .gnu.version  VERSYM         00000a9a 000a9a 0000c8 02      A   5  0  2
 [ 8] .gnu.version_r VERNEED       00000b28 000b28 000020 00      A   6  1  4
 [ 9] .rel.plt      REL            00000b48 000b48 000218 08      A   5 11  4
[10] .init         PROGBITS       00000d60 000d60 000018 00      AX  0   0  4
[11] .plt          PROGBITS       0000d7b8 000d78 000038 04      AX  0   0  4
[12] .text         PROGBITS       000090b0 0010b0 019fe4 00      AX  0   0  4
[13] .fini         PROGBITS       00023094 01b094 000010 00      AX  0   0  4
[14] .rodata       PROGBITS       000230a0 01b0a0 002340 00      A   0   0  8
[15] .ARM.exidx    PROGBITS       00025480 01d480 000000 00      A   0   0  1
[16] .ARM.exidx    ARM_EXIDX      00025480 01d480 000000 00      AL  12  0  4
[17] .eh_frame_hdr PROGBITS       00025488 01d488 00001c 00      A   0   0  4
[18] .eh_frame     PROGBITS       000254b4 01d4b4 00007c 00      A   0   0  4
[19] .init_array   INIT_ARRAY     0002d530 01d530 000004 00      WA  0   0  4
[20] .fini_array   FINI_ARRAY     0002d534 01d534 000004 00      WA  0   0  4
[21] .jcr          PROGBITS       0002d538 01d538 000004 00      WA  0   0  4
[22] .dynamic      DYNAMIC        0002d53c 01d53c 0000d0 08      WA  6   0  4
[23] .got          PROGBITS       0002d60c 01d60c 000018 04      WA  0   0  4
[24] .data         PROGBITS       0002d728 01d728 0003c0 00      WA  0   0  8
[25] .bss          NOBITS         0002da88 01da88 0001c8 00      WA  0   0  4
[26] .comment      PROGBITS       00000000 01da88 000940 00      A   0   0  1
[27] .debug_aranges PROGBITS      00000000 01ea28 000040 00      A   0   0  8
[28] .debug_pubnames PROGBITS     00000000 01eb88 001aae 00      A   0   0  1
[29] .debug_info PROGBITS 00000000 020376 013d27 00 0 0 1
[30] .debug_abbrev PROGBITS 00000000 03409d 002e4e 00 0 0 1
[31] .debug_line PROGBITS 00000000 03647b 0043a2 00 0 0 1
[32] .debug_frame PROGBITS 00000000 03a820 003880 00 0 0 4
[33] .debug_str PROGBITS 00000000 03d7b0 000673 00 0 0 1
[34] .note.gnu.arm.ident NOTE 00000000 03de18 00001c 00 0 0 4
[35] .debug_ranges PROGBITS 00000000 03e355 000018 00 0 0 1
[36] .shstrtab STRTAB 00000000 03de4d 000183 00 0 0 1
[37] .symtab SYMTAB 00000000 03e5e8 0048d0 10 38 773 4
[38] .strtab STRTAB 00000000 0431b8 0021fb 00 0 0 1
Key to Flags:
W (write), A (alloc), X (execute), M (merge), S (strings)
i (info), L (link order), G (group), x (unknown)
o (extra OS processing required) os (OS specific), p (processor specific)
```

从列表 15-1 中可以看出，有许多节包含调试信息。还有一个 `.comment` 节，其中包含超过 2KB（0x940）的信息，这些信息对于应用程序的功能并非必需。此示例文件的大小，包括调试信息在内，超过 275KB。

```
$ ls -l webdemo
-rwxrwxr-x 1 chris chris 283511 Nov 8 18:48 webdemo
```

如果使用 `strip` 实用工具剥离此文件，我们可以将其大小最小化，以保留目标系统上的资源。列表 15-2 显示了结果。

### 列表 15-2
#### 剥离目标应用程序

```
$ xscale_bs-strip -s -R .comment -o webdemo-stripped webdemo
$ ls -l webdemo*
-rwxrwxr-x 1 chris chris 283491 Apr 9 09:19 webdemo
-rwxrwxr-x 1 chris chris 123156 Apr 9 09:21 webdemo-stripped
```

在这里，我们从可执行文件中剥离了符号调试信息和 `.comment` 节。我们使用 `-o` 命令行开关指定剥离后的二进制文件的名称。你可以看到，剥离后的二进制文件的大小不到其原始大小的一半。当然，对于较大的应用程序，这种空间节省可能更加显著。最近编译的一个带有调试信息的 Linux 内核大于 18MB。剥离后如列表 15-2 所示，生成的二进制文件略大于 2MB！

为了以这种方式进行调试，你将剥离版本的二进制文件放置在目标系统上，并在你的开发工作站上保留一份包含调试所需符号信息的本地未剥离副本。你在目标板上使用 `gdbserver` 来提供返回开发主机的接口，在那里你对未剥离的二进制文件运行完整版的 GDB。

### 15.2.1 gdbserver

使用 `gdbserver` 允许你从开发工作站而不是在目标嵌入式 Linux 平台上运行 GDB。这种配置显然有很多好处。首先，你的开发工作站通常具有比嵌入式平台远更多的 CPU 算力、内存和硬盘存储空间。此外，被调试应用程序的源代码通常存在于开发工作站上，而不是嵌入式平台上。

`gdbserver` 是一个运行在目标板上的小程序，允许对板上的进程进行远程调试。在目标板上调用它时，需指定要调试的程序，以及它将监听来自 GDB 连接请求的 IP 地址和端口号。列表 15-3 显示了目标板上的启动序列。

#### 列表 15-3
**在目标板上启动 gdbserver**

```
$ gdbserver localhost:2001 webdemo-stripped
Process webdemo-stripped created; pid = 197
Listening on port 2001
```

这个特定示例启动了配置为监听端口 2001 上的以太网 TCP/IP 连接的 `gdbserver`，准备调试名为 `webdemo-stripped` 的剥离二进制程序。

从我们的开发工作站，我们启动 GDB，将包含我们要调试的符号调试信息的二进制可执行文件的名称作为参数传入。GDB 启动后，我们发出命令连接到远程目标板。列表 15-4 显示了这一序列。

