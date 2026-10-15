
| `--whole-archive` | 对于 `--whole-archive` 之后提到的每个归档，整个归档都被包含在链接中，而不是所需的模块。这通常用于将归档转换为共享库。 |

# 98 编程：1d

| 选项 | 说明 |
| --- | --- |
| `--wrap SYMBOL` | 为 `SYMBOL` 使用包装函数。任何对 `SYMBOL` 的未定义引用将解析为 `__wrap_SYMBOL`。任何对 `__real_SYMBOL` 的未定义引用将解析为 `SYMBOL`。 |

## nm

```
nm [ OPTION ... ] [ OBJFILE ... ]
```

`nm` 列出来自对象文件(s) `OBJFILE ...` 的符号。如果没有列出对象文件作为参数，`nm` 假设为 `a.out`。

对于每个符号，`nm` 显示符号的值、类型和名称。符号的值默认以十六进制显示，但也可以通过 `-t` 或 `--radix=` 选项选择另一种基数。符号类型包括但不限于以下列表（取决于对象文件格式，还可能存在其他类型）：

| 符号 | 说明 |
| --- | --- |
| A | 符号的值是绝对的，不会被进一步的链接改变。 |
| B | 符号位于未初始化数据段（称为 bss）。 |
| C | 符号是公共符号。公共符号是未初始化数据。当链接 |

以下表描述了 `nm` 行命令选项：

| 选项 | 说明 |
| --- | --- |
| `-A` or `-o` or `--print-file-name` | 在每个符号前加上发现它的输入文件名称或归档元素名称。否则，`nm` 仅在列出符号之前识别文件名。 |
| `-a` or `--debug-syms` | 显示所有符号，即使是通常不列出的调试器专用符号。 |
| `-B` | 等同于 `--format=bsd`。 |
| `-C` or `--demangle` | 将低级符号名解码（反混淆）为用户级名称。除了移除系统预置的任何初始下划线外，此 C++ 函数使名称具有可读性。 |
| `--no-demangle` | 不对低符号符号进行反混淆。这是默认设置。 |
| `-D` or `--dynamic` | 显示动态符号而非普通符号。这对于动态对象（例如某些类型的共享库）才有意义。 |
| `-f FORMAT` or `--format=FORMAT` | 使用输出 `FORMAT`，可以是 bsd、sys 或 posix。默认是 bsd。`FORMAT` 的第一个字符是重要的；可以是大写也可以是小写。 |
| `-g` or `--extern-only` | 仅显示外部符号。 |
| `-l` or `--extern-only` | 在符号符号前显示文件名。否则，`nm` 仅在列出符号之前识别文件名。对于每个符号，显示其重定位信息。 |
| `-n` or `--numeric-sort` | 按数字排序。 |
| `-p` or `--no-sort` | 不排序。按出现顺序列出符号。 |
| `-P` or `--portability` | 使用 POSIX 标准输出其成员。 |
| `-r` or `--reverse-sort` | 反向排序。 |
| `--size-sort` | 按大小排序。 |
| 选项 | 说明 |
| `-t RADIX` or `--radix=RADIX` | 使用 radix：十进制、八进制或十六进制。 |
| `--target=BFDNF` | 指定目标格式。 |
| `-u` or `--undefined-only` | 仅显示未定义的符号。 |
| `--defined-only` | 仅显示定义的符号。 |
| `-v` or `--version` | 显示版本。 |
| `--help` | 显示帮助。 |

# ranlib

```
ranlib ARCHIVE [ OPTION ]
```

`ranlib` 为归档生成索引。

| 选项 | 说明 |
| --- | --- |
| `-o FILE` | 将输出保存到 `FILE` 而不是替换它。 |
| `-p` or `--preserve-dates` | 保留访问和修改日期。 |
| `-X` or `--discard-all` | 移除所有全局符号。 |
| `-X` or `--discard-locals` | 移除生成的本地符号。这些通常以 L 开头。 |
| `-V` or `--version` | 显示版本。 |
| `-v` or `--verbose` | 详细输出。列出所有修改过的成员。 |

# strip

```
strip [ OPTION ... ] OBJFILE ...
```

`strip` 从对象文件(s) `OBJFILE` 中删除所有符号。必须提供一个文件。

| 选项 | 说明 |
| --- | --- |
| `-O BFDNAME` or `--output-target=BFDNF` | 使用输出格式 替换 `OBJFILE`。 |
| `-R SECTIONNAME` or `--remove-section=SECTIONNAME` | 从文件中删除命名的段。此选项可以给出多次。不当使用此选项可能会导致输出文件不可用。 |
| `-s` or `--strip-all` | 删除所有符号。 |
| `-g` or `-S` | 删除调试符号。 |
| `--strip-unneeded` | 删除重定位不需要的符号。 |
| `-K SYMBOLNAME` or `--keep-symbol=SYMBOLNAME` | 从文件中仅保留 `SYMBOLNAME`。此选项可以给出多次。 |
| `-N SYMBOLNAME` or `--strip-symbol=SYMBOLNAME` | 从文件中删除符号 `SYMBOLNAME`。此选项可以给出多次，并可以与 `-K` 以外的 strip 选项组合。 |
| `-o FILE` | 将输出保存到 `FILE`。使用此参数时，只能指定 `OBJFILE` 参数。 |

# 编程: gdb

`gdb` 是一个符号级调试器，用于为 C 和 C++ 程序提供源码级的问题隔离。它对 Modula-2、Chill、Pascal 和 Fortran 提供部分支持。对于使用不支持语言编写的程序或没有源代码的程序，`gdb` 可以提供汇编语言级别的支持。

`gdb` 可以有四种使用方式：

- 启动并调试新进程。
- 对已失败并留下核心转储文件（core dump）的进程进行“事后”调试。
- 调试正在运行的进程。
- 作为调试设施的后端，例如 emacs 调试器 xxgdb。

`PROGRAM` 是一个链接了包含符号数据的可执行二进制文件。当遇到段错误等错误时，某些程序会在后台使用一个 `CORE` 文件（通常命名为 core）。该文件的目的是对失败的进程进行调试。`CORE` 文件包含了描述故障时进程状态的数据。

提供 `PID` 可以对已经正在运行的进程进行调试。

## gdb 命令行选项

可以使用以下命令行选项：

| 选项 | 描述 |
| --- | --- |
| `-b BPS` | 设置 `gdb` 用于远程调试的任何串口接口的波特率（每秒比特数）。 |
| `-batch` | 以批模式运行。执行完所有通过 `-x` 指定的命令后带状态退出。 |
| `-cd DIRECTORY` | 使用 `DIRECTORY` 作为工作目录运行 `gdb`，而不是当前目录。 |
| `-command FILE` | 执行来自文件 `FILE` 的命令。 |
| `-core FILE` 或 `-c FILE` | 使用该文件作为核心转储。 |
| `-c NUMBER` | 连接到进程 ID `NUMBER`。如果存在核心转储格式的文件名，则将 `NUMBER` 作为核心文件。 |
| `-directory DIRECTORY` 或 `-d DIRECTORY` | 将 `DIRECTORY` 添加到搜索源文件的路径中。 |
| `-exec FILE` 或 `-e FILE` | 使用该文件作为适时执行的可执行文件，并结合核心转储文件检查数据。 |
| `-fullname` 或 `-f` | 每次显示帧（包括程序停止的每次）时，以标准、可识别的方式输出完整文件名和行号。 |
| `-nx` 或 `-n` | 不执行任何初始化文件（通常称为 `.gdbinit`）中的命令。 |
| `-quiet` 或 `-q` | 不打印介绍信息和版权消息。 |
| `-r` 或 `-readnow` | 立即读取每个符号文件的整个符号表。 |

# 编程: ltrace 103

| 选项 | 描述 |
| --- | --- |
| `-se FILE` | 从 `FILE` 读取符号表并将其作为可执行文件。 |
| `-symbols FILE` `-s FILE` | 从 `FILE` 读取符号表。 |
| `-tty DEVICE` | 使用 `DEVICE` 作为程序的标准输入和输出。 |
| `-x FILE` | 与 `-command FILE` 相同。 |

## 交互式 gdb 命令

`gdb` 命令仅占一行，但行的长度可以是任意的。每个命令以命令名开始，并带有取决于所用命令的参数。可以通过按下 Return 或 Enter 键重复许多命令。从 `#` 到行尾的任何文本都会被忽略并视为注释数据。这对于使用命令文件批处理运行 `gdb` 特别有用。

`gdb` 命令太多，无法在此处列出所有。在线帮助设施提供了可用命令的完整信息：

| 命令 | 描述 |
| --- | --- |
