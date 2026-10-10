
### 语法

```text
printf FORMAT [ARGUMENT]...
printf OPTION
```

### 描述

根据 `FORMAT` 打印 `ARGUMENT`(s)，或根据 `OPTION` 执行：

- `--help`

  显示此帮助并退出

- `--version`

  输出版本信息并退出

`FORMAT` 控制输出，类似于 C 语言中的 `printf`。解释序列如下：

- `\"`

  双引号

- `\\`

  反斜杠

- `\a`

  警报 (BEL)

- `\b`

  退格

- `\c`

  不再产生输出

- `\e`

  转义

- `\f`

  换页

- `\n`

  换行

- `\r`

  回车

- `\t`

  水平制表符

- `\v`

  垂直制表符

- `\NNN`

  具有八进制值 `NNN` 的字节（1 到 3 位数字）

- `\xHH`

  具有十六进制值 `HH` 的字节（1 到 2 位数字）

- `\uHHHH`

  具有十六进制值 `HHHH` 的 Unicode (ISO/IEC 10646) 字符（4 位数字）

- `\UHHHHHHHH`

  具有十六进制值 `HHHHHHHH` 的 Unicode 字符（8 位数字）

- `%%`

  单个 `%`

- `%b`

  将 `ARGUMENT` 视为字符串并解释`` 转义，但八进制转义形式为 `\0` 或 `\ONNN`

以及所有以 `dioXxXfeEgGcs` 之一结尾的 C 格式规范，`ARGUMENT`s 首先转换为适当的类型。处理可变宽度。

注意：你的 shell 可能有自己的 `printf` 版本，通常此处描述的版本会被其取代。请查阅你 shell 的文档以了解它支持的选项详情。

### 作者

由 David MacKenzie 编写。

### 报告缺陷

GNU coreutils 在线帮助: <http://www.gnu.org/software/coreutils/> 将 `printf` 翻译缺陷报告至 <http://translationproject.org/report.html>

### 版权

版权所有 2015 Free Software Foundation, Inc. 许可证 GPLv3+: GNU GPL 版本 3 或更高版本 <http://gnu.org/licenses/gpl.html>。这是自由软件：你可以自由修改和重新分发它。在法律允许的范围内，无保修。

### 参见

(3)

完整文档请访问: <https://www.gnu.org/software/libc/manual/html_node/printf-Invocation.html> 或在本地通过 `info '(coreutils) printf invocation'` 查看

### PRLIMIT

### 名称

`prlimit` - 获取和设置进程资源限制

### 语法

```text
prlimit [options] [--resource[=limits] [--pid PID]
prlimit [options] [--resource[=limits] command [argument...]
```

### 描述

给定一个进程 ID 和一个或多个资源，`prlimit` 尝试获取和/或修改限制。

当给定 *command* 时，`prlimit` 将使用给定参数运行此命令。

`limits` 参数由软值和硬值组成，用冒号 (`:`) 分隔，以修改现有值。如果未给出 `limits`，`prlimit` 将显示当前值。如果未给出其中一个值，则使用现有值。要指定无限或无穷大限制 (`RLIM_INFINITY`)，可以传递 `-1` 或 `'unlimited'` 字符串。由于限制的性质，软限制必须小于或等于硬限制（也称为上限）。要查看所有可用的资源限制，请参见 RESOURCE OPTIONS 部分。

- `soft:hard` 指定两个限制。

- `soft:` 仅指定软限制。

- `:hard` 仅指定硬限制。

- `value` 将两个限制指定为相同值。

### 通用选项

- `-h`, `--help`

  显示帮助文本并退出。

- `--noheadings`

  不打印标题行。

- `-o`, `--output list`

  定义要使用的输出列。如果未指定输出排列，则使用默认集。使用 `--help` 获取所有支持列的列表。

- `-p`, `--pid`

  指定进程 ID；如果未给出，则使用正在运行的进程。

- `--raw`

  使用原始输出格式。

- `--verbose`

  详细模式。

- `-V`, `--version`

  显示版本信息并退出。

### 资源选项

- `-c`, `--core[=limits]`

  核心文件的最大尺寸。

- `-d`, `--data[=limits]`

  数据段的最大尺寸。

- `-e`, `--nice[=limits]`

  允许提升的最大 nice 优先级。

- `-f`, `--fsize[=limits]`

  文件的最大尺寸。

- `-i`, `--sigpending[=limits]`

  待处理信号的最大数量。

- `-l`, `--lock[=limits]`

  锁定在内存中的地址空间的最大值。

- `-m`, `--rss[=limits]`

  常驻集大小 (RSS) 的最大值。

- `-n`, `--nofile[=limits]`

  打开文件的最大数量。

- `-q`, `--msgqueue[=limits]`

  POSIX 消息队列中字节数的最大值。

- `-r`, `--rtprio[=limits]`

  实时优先级的最大值。

- `-s`, `--stack[=limits]`

  堆栈的最大尺寸。

- `-t`, `--cpu[=limits]`

  CPU 时间，以秒为单位。

- `-u`, `--nproc[=limits]`

  进程的最大数量。

- `-v`, `--as[=limits]`

  地址空间限制。

- `-x`, `--locks[=limits]`

  持有文件锁的最大数量。

- `-y`, `--rt[=limits]`

  实时任务的时间。

### 示例

`prlimit --pid 13134`

显示所有当前资源的限制值。

`prlimit --pid 13134 --rss --nofile=1024:4095`

显示 RSS 的限制，并将打开文件数的软限制和硬限制分别设置为 1024 和 4095。

`prlimit --pid 13134 --nproc=512:`

仅修改进程数的软限制。

`prlimit --pid $$ --nproc=unlimited`

将当前进程的进程数软限制和上限值均设置为无限制。

`prlimit --cpu=10 sort -u hugefile`

将软限制和硬限制 CPU 时间均设置为 10 秒，并运行 'sort'。

### 参见

`prlimit(2)`, `prlimit(1)`

### 备注

`prlimit` 系统调用自 Linux 2.6.36 起得到支持，旧内核会导致此程序出错。

### 作者

Davídlohr Bueso <> - 纪念 Dennis M. Ritchie。

### 可用性

`prlimit` 命令是 util-linux 包的一部分，可从以下地址获取

### PS

### 名称

`ps` - 报告当前进程的快照。

### 概要

`ps` [*选项*]

### 描述

`ps` 显示关于选定活动进程的信息。如果您希望重复更新选定的进程和显示的信息，请使用 `top(1)`。

此版本的 `ps` 接受几种不同类型的选项：

1.  UNIX 选项，可以组合，但必须以前导破折号开始。

2.  BSD 选项，可以组合，但不应与破折号一起使用。

3.  GNU 长选项，以前导两个破折号开始。

不同类型的选项可以自由混合使用，但可能会出现冲突。由于此 `ps` 兼容的众多标准和实现，存在许多同义选项，它们在功能上是相同的。

请注意，`ps -aux` 与 `psaux` 是不同的。POSIX 和 UNIX 标准要求 `ps -aux` 打印由名为 "x" 的用户拥有的所有进程，以及由 `-a` 选项选择的所有进程。如果名为 "x" 的用户不存在，此 `ps` 可能会将该命令解释为 `psaux` 并打印警告。这种行为旨在帮助旧脚本和习惯的过渡。它是脆弱的，可能会发生变化，因此不应依赖它。

默认情况下，`ps` 选择与当前用户具有相同的有效用户 ID (`euid=EUID`) 并且与调用者位于同一终端的所有进程。它显示进程 ID (`pid=PID`)、与进程关联的终端 (`tty=TTY`)、以 [DD-]hh:mm:ss 格式计算得出的 CPU 时间 (`time=TIME`) 以及可执行文件名称 (`ucmd=CMD`)。默认情况下，输出是未排序的。
