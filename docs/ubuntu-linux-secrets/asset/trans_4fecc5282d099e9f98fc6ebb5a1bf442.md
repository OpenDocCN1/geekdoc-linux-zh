

```
[-defsym symbol=expression] [--demangle]
[--no-demangle] [-e emed] [--embedded-relocs] [-E]
[--export-dynamic] [-f name] [--auxiliary name]
[-F name] [--filter name] [--format input-format]
[-g] [--g-size] [-h name] [--soname name] [--help]
[-i] [--l] [--searchdir] [-M] [--Map mapfile]
[-m emulation] [-n] [-N] [--noinhibit-exec]
[--no-keep-memory] [--no-warn-mismatch] [--olevel]
[--format output-format] [-R file name] [--relax]
[-r] [--Ur] [--rpath directory] [--rpath-link directory]
[-S] [-s] [--shared] [--sort-common]
[--split-by-reloc count] [--split-by-file]
[-T commandfile]
[--section-start sectionname=sectionorg]
[--text textorg] [--Tdata dataorg] [--Tbss bssorg]
[-t] [--trace] [-v] [--verbose] [--version]
[--warn-common] [--warn-constructors]
[--warn-multiple-gp] [--warn-once]
[--warn-section-align] [--whole-archive]
[--no-whole-archive] [--wrap symbol] [-X] [-x]
```

虽然看起来命令行参数很多，但实际上你一次不必使用其中很多。示例只是表明 GNU 链接器是一个极其通用的程序，具有多种不同的功能。表 27-3 描述了用于 Intel 平台的命令行参数。

| **参数** | **描述** |
|---|---|
| `-b` | 指定目标代码输入文件的格式 |
| `-Bstatic` | 仅使用静态库 |
| `-Bdynamic` | 仅使用动态库 |
| `-Bsymbolic` | 在共享库中绑定对全局符号的引用 |
| `-c` | 从指定的命令文件读取命令 |
| `--cref` | 创建交叉引用表 |
| `-d` | 即使指定了可重定位输出，也为公共符号分配空间 |
| `-defsym` | 在输出文件中创建指定的全局符号 |
| `--demangle` | 在错误消息中对符号名称进行去修饰 |
| `-e` | 使用指定的符号作为程序的开始执行点 |
| `-E` | 对于 ELF 格式文件，将所有符号添加到动态符号表中 |
| `-f` | 对于 ELF 格式的共享对象，设置 DT_AUXILIARY 名称 |

## 表 27-3：(续)

| 参数 | 描述 |
|---|---|
| -F | 对于 ELF 格式的共享对象，设置 DT_FILTER 名称 |
| -format | 指定目标代码输入文件的格式（与 -b 相同） |
| -g | 已忽略。为与其他工具兼容而使用 |
| -h | 对于 ELF 格式的共享对象，设置 DT_SONAME 名称 |
| -i | 执行增量链接 |
| -l | 将指定的归档文件添加到链接文件列表中 |
| -L | 将指定的路径添加到搜索库的目录列表中 |
| -M | 为诊断目的显示链接映射 |
| -Map | 创建指定的文件以包含链接映射 |
| -m | 模拟指定的链接器 |
| -N | 指定可读写文本和数据段 |
| -n | 设置文本段为只读 |
| -noinhibit-exec | 即使出现非致命链接错误也生成输出文件 |
| -no-keep-memory | 优化链接以使用内存 |
| -no-warn-mismatch | 允许链接不匹配的目标文件 |
| -O | 生成优化的输出文件 |
| -o | 指定输出文件的名称 |
| -oformat | 指定输出文件的二进制格式 |
| -R | 从指定的文件名读取符号名称和地址 |
| -r | 生成可重定位输出（称为部分链接） |
| -rpath | 将指定的目录添加到运行时库搜索路径 |
| -rpath-link | 指定一个目录以搜索运行时共享库 |
| -S | 从输出文件中省略调试器符号信息 |
| -s | 从输出文件中省略所有符号信息 |
| -shared | 创建共享库 |
| -sort-common | 不按大小对输出文件中的符号进行排序 |
| -split-by-reloc | 根据指定的大小在输出文件中创建额外段 |
| -split-by-file | 为每个目标文件在输出文件中创建额外段 |
| --section-start | 将指定的段定位在输出文件中的指定地址 |

## 表 27-3：(续)

| 参数 | 描述 |
|---|---|
| `-T` | 指定命令文件（与 `-c` 相同） |
| `-Ttext` | 使用指定的地址作为文本段的起点 |
| `-Tdata` | 使用指定的地址作为数据段的起点 |
| `-Tbss` | 使用指定的地址作为 bss 段的起点 |
| `-t` | 在处理时显示输入文件的名称 |
| `-u` | 强制指定的符号作为未定义符号出现在输出文件中 |
| `-warn-common` | 当公共符号与另一个公共符号合并时发出警告 |
| `-warn-constructors` | 如果使用任何全局构造函数则发出警告 |
| `-warn-once` | 对每个未定义符号仅警告一次 |
| `-warn-section-align` | 如果由于对齐导致输出段地址发生变化则发出警告 |
| `--whole-archive` | 对于指定的归档文件，将归档中的所有文件都包含在内 |
| `-X` | 删除所有本地临时符号 |
| `-x` | 删除所有本地符号 |

对于最简单的情况，从汇编器生成的目标文件创建可执行文件，你可以使用以下命令：

```
ld -o cpuid cpuid.o
```

该命令从目标代码文件 cpuid.o 创建可执行文件 cpuid。可执行文件会创建适当的权限，以便可以从命令行提示符中运行。以下是该过程的示例：

```
 $ld -o cpuid cpuid.o
 $ ls -al cpuid
-rwxr-xr-x 1 rich rich 663 2008-11-13 19:53 cpuid
 $ ./cpuid
The processor Vendor ID is 'GenuineIntel'
 $
```

链接器自动创建了可执行文件，允许系统上的任何人执行它，但只有所有者可以修改它。

## GNU 调试器程序

许多专业程序员使用 GNU 调试器程序（gdb）来调试和排查 C 和 C++ 应用程序。你可能不知道的是，它也可以用于调试汇编语言程序。本节描述了 gdb 包以及如何使用它来排查你自己的 C、C++ 和汇编语言程序。
