
`put localfile remotefile`

`put filename1 filename2... filenameN remote-directory`

```
将文件或一组文件传输到指定的远程文件或目录。目标可以是两种形式之一：如果已经指定了主机，则为远程主机上的文件名；或者使用如下格式的字符串来同时指定主机和文件名。
```

```
host:filename
```

如果你使用后一种格式，指定的主机将成为后续传输的默认主机。如果你使用 `remote-directory` 形式，则假设远程主机运行着 UNIX 系统。只有当文件已存在且公开写时才能写入文件（参见 `.tftpd(1)`）。

```
get filename
```

```
get remotename localname
```

```
get filename1 filename2... filenameN
```

从指定的远程源获取文件或一组文件。源可以是两种形式之一：如果已经指定了主机，则为远程主机上的文件名；或者使用如下格式的字符串来同时指定主机和文件名。

`host:filename`

如果你使用后一种格式，最后指定的主机将成为后续传输的默认主机。使用 `get` 命令从远程主机传输多个文件时，必须指定三个或更多文件。如果你指定两个文件，则第二个文件将用作本地文件。

- `quit` 退出 ftftp。文件结束也会退出。
- `verbose` 切换详细模式。
- `trace` 切换数据包跟踪。
- `status` 显示当前状态。
- `remxt retransmission-timeout` 设置每个包重传超时时间（秒）。
- `timeout total-transmission-timeout` 设置总传输超时时间。
- `ascii` mode 的缩写。
- `binary` mode 的缩写。
- `?` 打印帮助。

## 1362

## Attributes

参见 `attributes(5)` 以获取以下属性的描述：

| 属性类型 | 属性值 |
| :--- | :--- |
| 可性 | SUNWcsu |

## 1337

## Description

`use time` 用于计算所需的时间。以下两个示例显示了 csh 版本的 `time` 与 `/usr/bin/time` 版本之间的区别。这些示例使用了 C shell。

```
castle# time find -name -print

export/home/winsor/core

1.0u 13.0s 1:11 99%0k 0+0io 0pf+0w

castle# /usr/bin/time find -name -print

export/home/winsor/core

```

```
real      1:10.2

user      1.0

sys       13.5

castle#
```

参见 `csh(1)` 以解释 `time` 输出的格式。

# Environment Variables

参见 `environ(5)` 以获取对影响 `time` 执行的环境变量的描述：`LC_CTYPE`, `LC_MESSAGES`, `LC_NUMERIC`, `NLSPATH`, 和 `PATH`。

# Exit Status

如果调用了命令，`time` 的退出状态为命令的退出状态；否则，`time` 命令以以下值之一退出。

```
1-125      time 命令中发生错误。

126        找到了命令但无法调用。

127        未找到命令。
```

# times 1339

## 属性

参见 `attributes(5)` 获取以下属性的描述：

| 属性类型 | 属性值 |
| --- | --- |
| 可用性 | SUNWcsu |

## 参见
`csh(1)`, `shell_builtins(1)`, `timex(1)`, `times(2)`, `attributes(5)`, `environ(5)`

# Bug

执行时间精确到秒，而 CPU 时间的测量精度为十分100秒。因此，CPU 时间之和可能比执行时间多出一秒。

# times — 报告当前 Shell 使用时间的 Shell 内置函数

### 概要

+ - sh
`times`
ksh
*
`times`

## 描述

**Bourne Shell**
打印从 shell 运行的进程的累计用户时间和系统时间。

**Korn Shell**
打印 shell 以及从 shell 运行的进程的累计用户时间和系统时间。

前面带有一个或两个星号 (`*`) 的 `ksh(1)` 命令将按以下方式进行特殊处理：

1. 命令前的变量赋值列表在命令完成后仍然有效。
2. 变量赋值后的 I/O 重定向。
3. 错误会影响包含它们的脚本。
4. 跟在带有 `**` 命令之后的且格式为变量赋值的单词将按照与变量赋值相同的规则进行扩展。这意味着在等号后执行波浪号替换，且不进行单词拆和文件名生成。

## 属性

参见 `attributes(5)` 获取以下属性的描述：

| 属性类型 | 属性值 |
| --- | --- |
| 可用性 | SUNWcu |

## 参见

+ - `ksh(1)`, `sh(1)`, `time(1)`, `attributes(5)`

# timex — 运行命令；报告进程数据和系统活动

### 概要

```
/usr/bin/timex [-o][-p [-fhkmert]][-s] command
```

## 描述

`timex` 命令作为 `sar` 包的一部分提供，提供了比普通的 `timex` 命令更好的诊断信息，特别是对于会产生子进程的 shell 脚本。默认情况下，`timex` 提供与普通 `timex` 命令相同的实际时间、用户时间和系统时间。此外，如果安装了进程记录软件，它还提供了额外的选项来显示进程记录数据 (`-p`)、磁盘块使用情况 (`-o`) 和总系统活动数据 (`-s`)。`timex` 命令将结果以秒为单位输出到标准错误。

> 注意 — 命令相关的进程记录是从记录文件 `/var/adm/pacct` 通过推断选择的，因为无法获取进程谱系关系。具有相同用户 ID、终端 ID 和执行时间窗口的后台进程会被错误地包含。

## 选项

+ -o 报告命令及其所有子进程读取或写入的块总数以及传输的字符总数。此选项仅在安装了进程记录软件时有效。

+ -p 列出命令及其所有子进程的进程记录。此选项仅在安装了进程记录软件时有效。子选项 `f`, `h`, `k`, `m`, `r`, 和 `t` 修改报告的数据项。

+ -f 在输出中打印 `fork(2)` 或 `exec(2)` 标志和系统退出状态列。

+ -h 不显示平均内存大小，而是显示进程在执行期间消耗总 CPU 的比例。这个“占用因子”（hog factor）的计算方法为 (总 CPU 时间/执行时间)。

+ -k 不显示内存大小，显示总 kcore 分钟。

+ -m 显示平均核心大小（默认值）。

+ -r 显示 CPU 因子（用户时间/系统时间 + 用户时间）。

+ -t 显示独立的系统和用户 CPU 时间。始终报告读取或写入的块数和传输的字符数。

+ -s 报告命令执行间隔期间发生的总系统活动（而不只是由于命令引起的）。报告 `sar(1)` 中列出的所有数据项。

## 示例

以下是使用 `timex` 的简单示例。

```
castle% timex -ops sleep 60
```

以下示例通过对子 shell 计时，测量任意复杂性的终端会话。

```
castle% timex -opskmt sh

session commands

EOT
```

## 属性

参见 `attributes(5)` 获取以下属性的描述：

| 属性类型 | 属性值 |
| --- | --- |
| 可用性 | SUNWaccu |

## 参见

`sar(1)`, `time(1)`, `times(2)`, `attributes(5)`

# tip — 连接到远程系统

### 概要

```
/usr/bin/tip [-v] [-speed-entry] {hostname | phone-number | device}
```

## 描述

使用 `tip` 命令建立到远程主机的全双工终端连接。一旦建立连接，使用 `tip` 的远程会话就像在本地终端上的交互会话一样。

`/etc/remote` 文件包含描述 `tip` 使用的远程系统和速度的条目。

每个主机都有一个默认波特率，或者你可以通过 `-speed-entry` 命令行参数指定速度。

当你指定电话号码时，`tip` 在远程文件中查找以下格式的条目：

```
tip -speed-entry
```
