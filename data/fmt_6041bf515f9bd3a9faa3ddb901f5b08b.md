
## 第 5 章：文件识别与分析

### 动态链接与静态链接

- 区分动态链接与静态链接可以了解程序的功能，并对稍后在其执行期间发出的系统调用进行动态分析时有所预期。动态链接的执行文件依赖于调用驻留在主机系统内存中的共享库或公共库及函数来成功执行。为了实现这一点，动态链接器会在需要时加载并链接这些库。动态链接执行文件执行所需的共享库和代码被称为依赖项。

- 相反，静态链接不需要依赖项，包含了程序成功执行所需的所有代码和库。

### 嵌入字符串分析

- IRC 通道：通常，用于互联网中继聊天（IRC）命令和控制服务器的通道服务器和名称会被编码在影响机器的恶意软件中。事实上，可疑文件可能会为了冗余目的而引用 IRC 通道，以防某个通道丢失或另一个通道上线时使用。

- 程序命令或选项：大多数情况下，攻击者需要与其传播的恶意软件进行交互，通常是为了提高传播方法的有效性。某些较旧版本的变体使用即时消息（IM）程序作为攻击向量，因此，调用 IM 传播的命令可能位于程序的字符串中，命令行选项和/或帮助/用法菜单信息中，这些信息可能会揭示目标标本的能力。

- 错误和确认消息：在恶意软件标本中发现的确认和错误消息，例如 `Exploit FTPD is running on: %i, at thread number: %i; total sends: %i`；往往具有重要意义，并能对恶意软件的能力提供深入的洞察。

#### 分析提示

虚假线索：`植入` 字符串

尽管嵌入字符串在分析可疑标本时可能具有潜在价值，但请注意攻击者和恶意软件作者会在代码中提供`植入`字符串以引导调查人员。虚假昵称、电子邮件地址和域名的实例相当常见。在检查任何给定标本并评估其嵌入字符串的意义时，请记住考虑文件的整个上下文和数字犯罪现场。

### 分析嵌入字符串的工具

- Linux 和 UNIX 发行版通常预装了 `strings` 工具，该工具可以显示文件中可打印字符的字符串。

- 默认情况下，`strings` 将显示从文件中初始化并加载的长度小于四个字符的 ASCII 文本序列，可以通过命令行选项进行修改。

- 要更改字符串的最小长度，请使用 `-n` 选项。同样，要提取 ASCII 以外的编码（如 Unicode），请应用 `-e` 选项并使用所需编码的相应参数。

- 在检查可疑标本的过程中，始终要使用 `all` `-a` 选项，这将导致文件实用扫描并显示可打印字符串，如图 5.21 所示。

- 在搜索字符串时，请注意功能指示器，或作为程序能力指示的文本引用。

#### Linux 系统恶意软件取证现场指南

```bash
lab@MalwareLab:~/home/malwarelab/Malware Repository$ strings -a sysfile | more
/lib/ld-linux.so.2
libc.so.2
strcpy
waitpid
ioctl
sprintf
recv
connect
atol
getpid
fgetats
memcmpy
pclose
fof
malloc
sleep
socket
select
popenen
accept
write
kill
---
```

图 5.21—使用 `strings` 检查可疑执行文件

- 此外，`strings` 可能会揭示用于编译可疑执行文件的编译器版本，如图 5.22 所示。诸如归属标识符或证明识别恶意软件作者的线索。在没有进一步线索或上下文的情况下，它可能并不显著，但与其他线索结合使用，它可以进一步识别攻击者制作该文件时使用的平台。

```bash
GCC: (GNU) 4.4.5 20110324 (Ubuntu/Linaro 4.4.4-14ubuntu5)
GCC: (GNU) 4.4.5 20110324 (Ubuntu/Linaro 4.4.4-14ubuntu5)
GCC: (GNU) 4.4.5 20110324 (Ubuntu/Linaro 4.4.4-14ubuntu5)
GCC: (GNU) 4.4.5 20110324 (Ubuntu/Linaro 4.4.4-14ubuntu5)
GCC: (GNU) 4.4.5 20110324 (Ubuntu/Linaro 4.4.4-14ubuntu5)
GCC: (GNU) 4.4.5 20110324 (Ubuntu/Linaro 4.4.4-14ubuntu5)
```

图 5.22—识别用于编译可疑执行文件的 GCC 编译器版本

### 调查考虑量

- 建议使用 `less` 或 `more` 文件分页选项，因为查询输出可能会在终端窗口中滚动几页。或者，考虑将输出重定向到文件；这通常使用 `>` 符号（如图 5.23 所示）或 `>>` 向文件追加内容来实现。

```bash
lab@MalwareLab:~/home/malwarelab/Malware Repository$ strings -a sysfile > strings-sysfile.txt
```

图 5.23—将输出重定向到文件

### 检查文件依赖：动态链接或静态链接

- 在对可疑程序的初步分析期间，只需识别文件是静态还是动态链接执行文件，就能为程序的功能提供早期指导，并对稍后在其执行期间发出的系统调用进行动态分析时有所预期。

- 正如本书引言所述，动态链接的执行文件依赖于调用驻留在主机系统内存中的共享库或公共库及函数来成功执行。为了实现这一点，动态链接器会在需要时加载并链接这些库。动态链接执行文件执行所需的共享库和代码被称为依赖项。

- 相反，静态链接不需要依赖项，包含了程序成功执行所需的所有代码和库。

- 区分这些者可以了解程序的功能，并对稍后在其执行期间发出的系统调用进行动态分析时有所预期。

### 在线资源

**参考页面**

通常在检查字符串、共享库和系统调用引用等嵌入实体时，拥有参考网站进行快速查阅是非常方便的。考虑下载一份 GNU C Library 副本以便快速方便地参考（http://www.gnu.org/software/libc/#Overview 或 http://ftp.gnu.org/gnu/libc/），或访问 GNU.org 上的 GNU C 参考文档（http://www.gnu.org/software/libc/manual/html_node/index.html）。同样，Open Group 的函数索引也是一个实用的参考工具（http://www.opengroup.org/onlineinepubs/009695399/idx/index.html）。

- 在响应证据支持可能发生过上述情况的事件期间，在可行的情况下，最佳行动方案是：

  - 获取受害者硬盘的取证镜像，如第 3 节所述；
  - 利用第 3 节涵盖的制品发现，识别可能受影响的共享对象/ELF 动态链接器/加载器；
  - 使用本章之前介绍的工具和技术，获取共享对象/ELF 动态链接器/加载器的哈希值，以便后续与未修改的未知版本进行对比。

### GUI 文件依赖分析工具

- 如果你倾向于使用 GUI 工具检查文件依赖关系，Filippos Papadopoulos 和 David Sandbox 开发了 Visual Dependency Walker（也称为 Vis-ld），它能够让调查人员获取目标文件共享库的细粒视角，如图 5.26 所示。

- 与 `lld` 不同，Visual Dependency Walker 为二进制可执行文件中所有的模块构建图形化分级树，允许调查人员深入识别依赖项需要并调用的文件，如图 5.26 所示。

- 许多好奇的分析师都会使用像 Visual Dependency Walker 这样的分级分析工具，因为工具输出提供了视角。因此，开发并发布了三个与 Visual Dependency Walker 相似且感觉类似的工具：ELF Library Viewer、ELF Dependency Walker 以及 DepSpec Dependency Viewer，它们在本章末尾的工具箱中进行了更详细的解释。

有关 Visual Dependency Walker（也称为 Vis-ld）的更多信息，请访问 http://freshmeat.net/projects/visual-lld/。

有关 ELF Library Viewer 的更多信息，请访问 http://www.purinchu.net/wp/2007/10/24/elf-library-dependency-viewer/。

**图 5.26**——使用 Visual Dependency Walker 检查怀疑文件

- DepSpec Dependency Viewer 具有双界面，允许探索文件依赖关系以及相关的符号信息，如图 5.27 所示。

**图 5.27**——使用 DepSpec 检查怀疑文件

在获取怀疑文件依赖关系的总体概览后，通过查找文件中可能存在的任何符号和调试信息来继续检查该程序。

有关 ELF Dependency Walker 的更多信息，请访问 http://code.google.com/p/elf-dependency-walker/。

有关 DepSpec 的更多信息，请访问 http://wiki.gpio.ca/wiki/DepSpec。

### 分析技巧

Solaris 系统上的 ELF 二进制分析

我们从一些网络和安全管理员那里听到：`是的，但 Solaris 与 Linux 不同。`操作系统确实不同，但在用于分析 ELF 二进制可执行文件的工具和技术上存在一些共同点。尽管如此，某些工具可以在 Solaris UNIX 中实现，而这些工具在 Linux 系统上并不原生可用。以下是 Solaris 平台中可用于进行分析的某些工具。

- `PVS` 显示动态对象的内部版本信息。
- `Elldump` 导出 ELF 文件的部分。
- `Ldd` 列出执行文件或共享对象的依赖。
- `File` 识别文件类型。
- `Dump` 导出对象部分（类似于 Linux 的 `objdump`）。
- `Strings` 查找对象或二进制文件中的可打印字符串。
- `Nm` 输出对象文件。
- `pdb` 通用调试器（类似于 Linux 的 `gdb`）。

### 符号与调试信息

执行文件被编译和链接的方式留下了关于怀疑程序性质和能力的重大线索。

正如本章讨论的，执行文件被攻击者编译和链接的许多方式可能会留下关于怀疑程序性质和能力的重大线索。例如，攻击者不会剥离 ELF 执行文件的变量和函数名（作为符号，位于执行文件的符号表中），数字调查人员可能借此了解程序的程序。同样，如果程序在开发阶段以调试模式编译以协助故障排除，它将提供额外信息，如源代码和调试行。

- 大多数 Linux 操作系统发行版都带有 `nm` 工具。

- 要显示怀疑二进制文件的符号，对其执行 `nm -al` 命令，它将显示所有符号，包括调试器（通常不列出）以及任何相关的调试数字（图 5.28）。

```
lab@Malware:~/home/malware$ nm -al sysfile
0804d30b b .bss
00000000 n .comment
0804d41 d .ctors
0804a000 d .data
00000000 N .debug_abbrev
00000000 N .debug_arr
00000000 N .debug_frame
00000000 N .debug_info
00000000 N .debug_line
00000000 N .debug_ptr
00000000 N .debug_str
0804dfd0 d .dtors
0804a120 d .dynamic
0804a863 r .dynsym
0804a828 r .dynym
0804c3f4 m .eh_sym
0804c3f9 r .fin
0804a7f5 r .gnu.version
0804a866 r .gnu_version_
0804d12c d .got
0804a128 d .hash
0804a418 n .init
0804e0f6 e .interp
0804a11 d .ljr
08048108 N .note.ABI-tag
0804a6e4 t .plt
0804b89e r .rel.dyn
0804b89c r .rel.plt
0804e6b0 r .rodata
00000000 a .shrtab
00000000 a .strtab
00000000 .symtab
0804a66d t .text
0804d860 B execute
U exit@@GLIBC_2.0
U fclose@@GLIBC_2.1
U feof@@GLIBC_2.0
U fgets@@GLIBC_2.0
08049141 T filters
U fopen@@GLIBC_2.0
U forctl@@GLIBC_2.0
U fputc@@GLIBC_2.0
0804ae58 t frame_dummy
U free@@GLIBC_2.0
080495f4 d data
U gethostname@@GLIBC_2.0
U getpid@@GLIBC_2.0
U getppid@@GLIBC_2.0
080490de T getspspof
U getspspof@@GLIBC_2.0
0804a9e7 T help
0804aeae4 T host2ip
08049e7b U htons@@GLIBC_2.0
```

图 5-28-`nm -al` 命令解析怀疑的 ELF 文件。

`-a` 选项的替代方案是 `--debug-syms`，它可以实现相同的结果。

如图 5.28 所示，输出揭示了大量的符号信息，其中某些信息可能有助于了解程序的性质和目的。

- 输出的左侧列识别相应符号的十六进制值，随后是符号类型，然后是符号名称。

- 记住，小写符号类型是局部变量，而大写符号是全局变量。

#### 分析技巧

```
Break,enter...compile
```

- 在检查 `nm` 输出时，注意引用以下内容：

- ELF 段
- 函数调用
- 攻击命令
- 用于创建程序的编译器类型和版本

对于解析怀疑文件中符号信息的替代查看方法，请考虑使用 `nm` 工具（`elfutils` 工具套的一部分），它为分析提供了更具结构化的输出，包括符号名、值、类、类型、大小、行号和 ELF 段的指定和列出。

可以通过 `nm` 和 `eu-nm` 工具中提供的额外命令，从恶意二进制文件中收集更多的符号信息。通过这种方式，数字调查人员可以在特定的上下文中查看符号内容。要显示特殊符号（或具有目标特定含义且在包含正常符号列表中通常没有帮助的符号），请应用 `--special-sym` 选项（图 5.29）。

### Linux系统恶意软件取证指南

```
lab@MalwareLab:~/home/malwarelab/Malware Repository$ nm --special-syms ysfile
08048af T send
0804b367 T _352
0804b2f3 T _376
08040659 T _433
0804d420 D DYNAMIC
0804fc D GLOBAL_OFFSET_TABLE
0804be84 R _std_used
      J_RegisterClasses
0804b58c T _NICK
08040399 T _PRIMMSG
0804a6b3 T _
0804dlec D CTSTOR_END
0804d1e8 D CTSTOR_LIST
0804d1fd D DTOR_HDR
0804d1f0 D DTOR_LIST
0804c34 R EH_FRAME_BEGIN
0804c7f9 R _FRAME_END
0804d1f8 D JCR_END
0804d1f9 D JCR_LIST
080408e6 A _beg_start
0804d000 D data_start
      do_global_dtors_aux
0804e440 t to_global_dtors_aux
0804d004 D dso_handle
      u _errno_location@GLIBC_2.0
0804d000 A _fini_array_end
w      _fini_array_end
0804d000 A _init_array_end
0804be0c T libc_csu_fini
0804bdcc T libc_csu_init
      u _libc_main@GLIBC_2.0
0804d2e6 A _edata
0804a379 T _send
0804be64 T _fini
0804be80 R _init
0804b8d4 T _start
      u accept@GLIBC_2.0
      u atoi@GLIBC_2.0
      u atol@GLIBC_2.0
      u bcopy@GLIBC_2.0
      u bind@GLIBC_2.0
0804d8f8 t call_gmon_start
0804d968 B chan
0804d030 D changeserver
      u close@GLIBC_2.0
<edited for brevity>
```

图 5.29—使用 `nm --special-syms` 命令
