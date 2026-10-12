
## ollydbg

**描述** `OllyDbg` 是一个强调二进制代码分析的 x86 调试器，在没有源代码可用时非常有用。它可以跟踪寄存器、识别过程、API 调用、切换、表、常量和字符串，并从对象文件和库中定位例程。它具有友好的界面，其功能可以通过第三方插件扩展。`OllyDbg` 常用于程序的逆向工程。它经常被破解者用于破解其他开发者开发的软件。由于其易用性和易得性，它通常是破解和逆向工程的首选工具。对于程序员来说，它也有助于确保程序按预期运行。此外，它还可以用于恶意软件分析。

**用法** n/a；GUI 工具

**示例** n/a；GUI 工具

## [54] 反汇编

- `jad`
- `rabin2`
- `radiff2`
- `rasm2`
- `recstudio`
- `recstudio-cli`

## jad

**描述** `Jad` (Java Decompiler) 是一个目前不再维护的 Java 语言反汇编器。`Jad` 提供了一个命令行界面用于从类文件中提取源代码。`Jad` 的图形用户界面是 `JadEclipse`，它是 `Eclipse` IDE 的一个插件。

**用法** n/a

**示例** n/a

**描述** `rabin2` — 二进制程序信息提取器。该程序允许你简单地获取 ELF/PE/MZ 和 CLASS 文件的信息。

**用法** `rabin2 [-eoicsSlrvz] [-h] [-L library] [file]`

**选项**
- `-e` 显示磁盘和内存中的入口
- `-l` 显示导入（从库导入的符号）
- `-c` 显示头部校验和（如果存在）
- `-s` 显示导出符号
- `-o` 显示其他符号（非导入/导出）
- `-S` 显示节（sections）
- `-l` 列出链接到二进制文件的库
- `-L library` 显示内存中加载的库的基地址
- `-r` 以 radare 格式显示输出
- `-z` 显示数据段中的字符串（类似于 gnu strings）
- `-v` 显示虚拟地址偏移
- `-h` 显示用法帮助信息。

**示例** `rabin2 -s a.out` (列出程序的符号)

**示例** `rabin2 -e a.out` (获取入口)

**示例** `rabin2 -vrsi a.out` (从 radare 加载符号和导入)

## radiff2

**描述** `radiff2` - 统一二进制差异工具。`radiff2` 为数据和代码实现了许多二进制差分算法。

**用法** `radiff2 [-cCOdrspvh] [-t 0-100] [-g sym] file1 file2`

**选项** http://manpages.ubuntu.com/manpages/precise/man1/radiff2.1.1.html

**示例** `radiff2 -g 0x8034804 a > b.dot`

**示例** `radiff2 /bin/true /bin/false`

## rasm2

**描述** `rasm2` — radare2 补丁汇编器和反汇编器。该工具使用 `r_asm` 汇编和反汇编文件或十六对字符串。它支持大量的架构，可以使用 `-L` 标志列出。

**用法** `rasm2 [-dDfBCLev] [-F in:out] [-o offset] [-a arch] [-b bits] [-s syntax] [-I int] [ARG]`

**选项** http://manpages.ubuntu.com/manpages/precise/man1/rasm2.1.html

**示例** `rasm2 -a x86 -b 32 'mov eax, eax, 33'` (汇编操作码)

**示例** `rasm2 \d 90` (反汇编操作码)

## recstudio

**描述** 无信息

**用法** 无信息

**选项** 无信息

**示例** 无信息

![](img/5d79c1ec)

## recstudio-cli

**描述** 无信息

**用法** 无信息

**选项** 无信息

**示例** 无信息

![](img/5d79c1ec)

## javasnoop

**描述** `JavaSnoop` 是一个用于测试（即：黑客）Java 桌面应用程序或 applet 的工具。更多信息：http://javasnoop.googlecode.com/svn-history/r32/trunk/resources/README.txt

**用法** 无适用； GUI 工具

**示例** 无适用； GUI 工具

## radare2

**描述** `radare-` 逆向工程框架。`Radare2` 是一个用于反汇编、调试、分析和操作二进制文件的开源工具。`Radare` 项目最初作为一个法证工具，一个可编写脚本的命令行十六进制编辑器，但后来支持了分析二进制文件、反汇编代码、调试程序、附加到远程 gdb 服务器等……

**用法** `radare2 [-s addr] [-b bsize] [-e k=v] [-dwnLV] file`

**选项** http://www.makelinux.net/man/1/R/radare2

**选项** 输入 `?` 获取帮助。

**选项** 使用 `V` 命令进入视觉化模式。然后按 `?` 获取帮助。

```
EXAMPLE r2 -c=H /bin/ls
```

# rafind2

**描述** `afind2` — 高级命令行十六进制编辑器

**用法** `rafind2 [-zXnrhv] [-b size] [-f from] [-t to] [-[m|s|e] str] [-x hex] file`

**选项** http://manned.org/rafind2.1

**示例** 无适用

# ragg2

**描述** `ragg2` — 在奇异环境下运行程序的 radare2 工具。

`ragg2` 是 `r_egg` 的前端，将程序编译为适用于 x86-32/64 和 ARM 的极小二进制文件。

该工具是实验性的，它是对旧 rarc2 和 rarc2-tool 程序的库重写，并与 `r_asm` 和 `r_bin` 集成。

由 `r_egg` 生成的程序是可定位的，可以注入到运行中的进程或磁盘二进制文件中。

`ragg2-cc` 是随 r2 提供的另一个工具，用于从 C 代码生成 shellcode。最终代码可以使用 `rabin2` 进行链接，并且是可定位的，可以用于注入到任何远程进程。

`ragg2-cc` 在概念上基于 `shellforge4`，但仅支持 linux/osx x86-32/64 平台。

```
USAGE ragg2 [-a arch] [-b bits] [-k kernel] [-f format] [-o file] [-i shellcode] [-l path] [-e encoder] [-B hexpairs] [-c k=v] [-C file] [-d off:dword] [-D off:dword] [-w off:hexpair] [-p padding] [-FOLSRxvh]
```
