
- `-H server[:port]`

使用替代服务器。

- `-U username`

使用替代用户名。

- `-P destination[/instance]`

将文件打印到指定的打印机。

- `#o copies` 设置打印副本数。

- `-h` 禁用 banner。此选项等同于 `-o job-sheets=none`。

- `-l` 指定打印文件已针对目标格式化，应不经过过滤发送。此选项等同于 `-o raw`。

- `-m` 在作业完成时发送电子邮件。

- `-o option=[value]` 设置作业选项。

- `-p` 指定打印文件应带有阴影页，显示日期、时间、作业名称和页码。此选项等同于 `-o prettyprint`，且仅打印文本文件有用。

- `-q` 保持作业打印。

- `-r` 指定在提交后删除命名的打印文件。

## 注意

`-c`、`-d`、`-f`、`-g`、`-i`、`-n`、`-t`、`-v` 和 `-w` 选项不受 CUPS 支持，使用时会产生警告信息。

## 相关参考

(1), (1), (8), (1), (1), (1), CUPS 在线帮助 (

## 版版权

Copyright © 2007-2014 by Apple Inc.

## lprm

### 名称

`lprm` - 取消打印作业

## 语法

```
lprm [ -E ] [ -U username ] [ -h server[:port] ] [ -P destination[/instance] ] [ job-id(s) ]
```

## 描述

`lprm` 取消已进入队列的打印作业。如果不提供任何参数，将取消默认目标上的当前作业。你可以指定一个或多个作业 ID 数字来取消这些作业，或使用 `-` 选项来取消所有作业。

## 选项

`lprm` 命令支持以下选项：

`-E`

在连接服务器时强制加密。

`-P destination[/instance]`

指定目标打印机或类别。

`-U username`

指定另一个用户名。

`-h server[:port]`

指定另一个服务器。

## 遵循标准

CUPS 版本的 `lpm` 与同名的标准 Berkeley 命令兼容。

## 示例

取消默认打印机上的当前作业：`lprm`

取消作业 1234：`lprm 1234`

取消所有作业：`lprm -`

## 相关参考

(1), (1), (1), (1), (1), CUPS 在线帮助 (

## 版权

Copyright © 2007-2014 by Apple Inc.

## lpstat

### 名称

`lpstat` - 输出 cups 状态信息

## 语法

```
lpstat [-E] [-H] [-U username] [ -h hostname:port] [ -l] [ -W which-jobs ] [ -a destination(s) ] [-c [ class(es) ] ] [-d [ -o destination(s) ] ] [-p [ printer(s) ] ] [-r ] [ -R ] [ -s ] [-t ] [ -u [ user(s) ] ] [-v [ printer(s) ] ]
```

## 描述

`lpstat` 显示关于当前类别、作业和打印机的状态信息。在不带参数运行时，`lpstat` 将列出当前用户提交的活跃作业。

## 选项

`lpstat` 命令支持以下选项：

`-E`

在连接服务器时强制加密。

`-H`

显示服务器主机名和端口。

`-R`

显示打印作业的排序。

`-U username`

指定另一个用户名。

`-W which-jobs`

指定显示哪些作业，“completed”（完成）或“not-completed”（默认）。此选项必须出现在 `-o` 选项和/或任何打印机名称之前，否则向调度程序的请求将使用默认值（"not-completed"）。

`-a [printer(s)]`

显示打印机队列的接收状态。如果未指定打印机，则列出所有打印机。

`-c [class(es)]`

显示打印类别以及属于这些类别的打印机。如果未指定类别，则列出所有类别。

`-d`

显示当前默认目标。

`-h server:port`

指定另一个服务器。

`-l`

显示打印机、类别或作业的详细列表。

`-o [destination(s)]`

显示目标上的队列作业。如果没有指定目标，则显示所有作业。

`-p [printer(s)]`

显示打印机以及它们是否已启用打印。如果未指定打印机，则列出所有打印机。

`-r`

显示 CUPS 服务器是否正在运行。

`-s`

显示状态摘要，包括默认目标、类别列表及其成员打印机，以及打印机及其关联设备。这等同于使用 `-d`、`-c` 和 `-v` 选项。

`-t`

显示所有状态信息。这等同于使用 `-r`、`-d`、`-c`、`-v`、`-a`、`-p` 和 `-n` 选项。

`-u [user(s)]`

显示指定用户提交的作业列表。如果没有指定用户，则列出当前用户提交的作业。

`-v [printer(s)]`

显示打印机及其连接的设备。如果未指定打印机，则列出所有打印机。

## 遵循标准

与 System V 打印系统不同，CUPS 允许打印机名称包含空格、制表符、“和#以外的任何打印字符。此外，打印机类别名称不区分大小写。

`-h`、`-E`、`-U` 和 `-W` 选项是 CUPS 特有的。

Solaris 的 `-f`、`-P` 和 `-S` 选项会被静忽略。

## 相关参考

(1), (1), (1), (1), (1), CUPS 在线帮助 (

## 版权

Copyright © 2007-2014 by Apple Inc.

## ls

### 名称

`ls` - 列出目录内容

## 语法

```
ls [OPTION]... [FILE]...
```

## 描述

列出文件信息（默认是当前目录）。如果指定了 `-sort`，则按字母排序目录。短选项的强制参数是强制的。

`-a, --all`

不忽略以 `.` 开头的项

`-A, --almost-all`

不列出隐含的 `. ..`

`--author`

打印每个文件的作者

`-b, --escape`

对非图形字符打印 C 风格的转义字符

`--block-size=SIZE`

在打印大小前按 SIZE 缩放大小；例如，`block-size=M`

`-B, --block-size`

以 104876 字节为单位打印大小

`-ups`

不列出以 `~` 结尾的项

`-c`

按 `ctime`（文件状态更改时间）排序；`-t`：显示 `ctime` 并按名称排序；否则：按 `ctime` 最新排序

`-C`

按列列出项

`--color=[WHEN]`

彩色输出；WHEN 可以是‘always’‘auto’或‘never’

`-d, --directory`

列出目录本身而非内容

`-D, --dired`

生成用于 Emacs dired 的输出

`-f`

不排序，启用 `-a`

`-F, --classify`

在项后添加指示符（如 `*`）

`--file-type`

同样不添加 `'*'`

`--format=WORD`

跨列，逗号

`-m`

用逗号分隔列表填充宽度

`-n, --numeric-uid-gid`

类似于 `-I`，但列出数字用户 ID

`-N, --literal`

打印原始名称（不特殊处理控制字符）

`-0`

类似于 `-l`，但不列出分组信息

`-p, --indicator-style=slash`

在目录后添加 `/` 指示符

`-q, --hide-control-chars`

用 `?` 打印非图形字符

`--show-control-chars`

原样显示控制字符（默认值，除非程序是 `ls` 且输出到终端）

`-Q, --quote-name`

用双引号括起名称

`--quoting-style=WORD`

对名称使用 WORD 引用样式：literal, locale, shell, shell-always, c, escape

`-r, --reverse`

反向排序

`-R, --recursive`

递归列出子目录

`-s, --size`

打印每个文件的分配大小

`-S`

按文件大小从大到小排序

`--sort=WORD`

按 WORD 排序而不是无 (-U)、大小 (-S)、时间 (-t)、版本 (-v)、扩展 (-X)

`--time=WORD`

在 `-I` 时，用 WORD 显示时间而非默认修改时间：使用 atime 或访问时间 (-u);使用 ctime 或状态 (-c)并在 `--sort=time`（最新）时将指定的时间作为排序键

`--time-style=STYLE`

在 `-I` 时，使用 STYLE 显示时间：full-iso, long-iso, iso, locale, 或 +FORMAT

FORMAT 的解释方式类似于 `'date'`；如果 FORMAT 是

FORMAT1

FORMAT2，则 FORMAT1 应用于非近期文件，FORMAT2 应用于近期文件；如果 STYLE 前缀为 'posix-'，则 STYLE 仅在 POSIX 区域外生效

`-t`

按修改时间排序，最新优先

`-T, --tabs=COLS`

假设制表符位置为 COLS 而非 8

`-u`

在 `-lt` 时，按所有者和访问时间排序；在 `-I` 时：显示访问时间并按名称排序；否则：按访问时间最新优先

`-U`

不排序；按目录顺序列出项

`-v`

对文本中的（版本）数字进行自然排序

`-w, --width=COLS`

假设屏幕宽度而非当前值

打印每个文件的安全上下文

`- -1` 每行列出一个文件。在使用 `-q` 或 `-b` 时避免使用 '\'

`--help` 显示此帮助信息并退出

`--version` 输出版本信息并退出

大小参数（SIZE ARGUMENT）是一个整数和一个可选的单位（例如：`10K` 是 `10*1024`）。单位有 K,M,G,T,P,E,Z,Y（1024 的幂次方）或 KB,MB,\...（1000 的幂次方）。

使用颜色区分文件类型在默认情况下以及使用 `--color=never` 时均会被停用。使用 `--color=auto` 时，`ls` 仅在标准输出连接到终端时才会输出颜色代码。可以使用 `LS_COLORS` 环境变量来更改设置。使用 `diricolors` 命令进行设置。

## 退出状态：

- `0` 如果一切正常（OK），
- `1` 出现轻微问题（例如：无法访问子目录），
- `2` 严重错误（例如：无法访问命令行参数）。

## 作者

由 Richard M. Stallman 和 David MacKenzie 编写。

## 报告 Bug

GNU coreutils 在线帮助：`<>` 向 `<>` 报告 `ls` 翻译 Bug

版权 © 2015 Free Software Foundation, Inc. 许可协议 GPLv3+: GNU GPL 3 版或更高版本 `<>`。这是一份自由软件：你可以自由地更改和分发它。在法律允许的范围内不提供任何保证。

## 另另

完整文档请访问：`<>` 或通过本地查看：info ‘(coreutils) ls invocation’

## LSATTR

- 名称

`lsattr` - 列出 Linux 次级扩展文件系统上的文件属性

## 语法

```
lsattr [ -RVadv ] [ 文件... ]
```

## 描述

`lsattr` 列出次级扩展文件系统上的文件属性。关于属性的描述及其含义，请参阅 (1)。

## 选项

`-R` 递归列出目录及其内容的属性。

`-V` 显示程序版本。

`-a` 列出目录中的所有文件，包括以 `.` 开头的文件。

`-d` 像列出其他文件一样列出目录，而不是列出其内容。

`-v` 列出文件的版本/生成号。

## 作者

Isattr 由 Remy Card `<>` 编写。目前由 Theodore Ts’o `<>` 维护。

## Bug

没有 :-)。

## 可用性

`lsattr` 是 `e2fsprogs` 包的一部分，可以通过以下方式获取

## 另另

(1)

## LSCPU

- 名称

`lscpu` - 显示关于 CPU 架构的信息

## 语法

```
lscpu [-a|-b|-c] [-x] [-s directory] [-e[=list]]|-p[=list]] lscpu -h|-V
```

### 描述 从 `sysfs` 和 `/proc/cpuinfo` 获取的架构信息。命令输出可以针对解析或人类可读性进行优化。这些信息包括（例如）CPU 数量、线程、核心、插槽（sockets）和非统一内存访问（NUMA）节点。此外还有关于 CPU 缓存和缓存共享、系列、型号、bogoMIPS、字节序和步进（stepping）的信息。

导致输出表格的选项具有列表参数。使用该参数可以自定义命令输出。指定一个用逗号分隔的列标签列表，以将表格限制为指定的列，并按指定的顺序排列。查看 COLUMNS 以获取有效列标签列表。列标签不区分大小写。

并非所有架构都支持所有列。如果指定的列不受支持，`lscpu` 会打印该列但不会为其提供任何数据。

## COLUMNS

注意拓扑结构元素（核心、插槽等）使用从零开始的顺序唯一 ID，但 CPU 逻辑编号遵循内核，内核并不保证编号是连续的。

## CPU

Linux 内核使用的 CPU 逻辑编号。

## CORE

逻辑核心数。一个核心可以包含多个 CPU。

## SOCKET

逻辑插槽数。一个插槽可以包含多个核心。

## BOOK

逻辑组数。一个组可以包含多个插槽。

## NODE

逻辑 NUMA 节点数。一个节点可能包含多个组。

## CACHE

关于 CPU 之间如何共享缓存的信息。

## ADDRESS

CPU 的物理地址。

## ONLINE

用于显示 Linux 实例当前是否使用该 CPU 的指示。

## CONFIGURED

显示虚拟机是否已将 CPU 分配给运行 Linux 实例的虚拟硬件的指示。已配置的 CPU 可以由 Linux 实例设置为在线。当您的硬件系统和虚拟机支持动态 CPU 资源分配时，此列才包含数据。

## POLARIZATION

此列包含运行在带有虚拟机的虚拟硬件上的 Linux 实例的数据，该虚拟机可以切换 CPU 分发模式（极化）。极化可以是：

## 水平 (horizontal)

工作负载分布在所有可用 CPU 上。

## 垂直 (vertical)

工作负载集中在少数 CPU 上。

对于垂直极化，该列还显示集中程度：高、中、低。当您的硬件系统和虚拟机支持 CPU 极化时，此列才包含数据。

## MMHZ

CPU 的最大兆赫值。当 `lscpu` 用作硬件清单信息收集工具时非常有用。注意兆赫值是动态的，并根据当前资源需求由 CPU 调度器驱动。

## 选项

`-a, —all`

在输出中包含在线和离线 CPU 的行（`-e` 的默认值）。此选项只能与选项 `-e` 或 `-p` 一起指定。

`-b, —online`

将输出限制为在线 CPU（`-p` 的默认值）。此选项只能与选项 `-e` 或 `-p` 一起指定。

`-c, —offline`

将输出限制为在线 CPU（注：原文此处为 online，应为 offline）。此选项可以与选项 `-e` 一起指定。

`-e, —extended=[list]`

以人类可读的格式显示 CPU 信息。

如果省略列表参数，`lscpu` 将包含所有可用数据的列。

当指定列表参数时，字符串不应包含任何空格。例如：‘`-e=cpu,node or extended=cpu,node`’。

如果未识别到 CPU 缓存，则省略缓存列。当指定列表参数时，列之间用冒号（:）分隔。例如：‘`-p=cpu,node or parse=cpu,node`’。

`-h, —help`

显示帮助文本并退出。

`-p, —parse=[list]`

针对解析优化命令输出。

如果省略列表参数，输出与早期版本的 `lscpu` 兼容。在这种兼容格式下，使用两个逗号分隔缓存列。在未识别到 CPU 缓存时。例如：‘`-p=cpu,node or parse=cpu,node`’。

`-s, —sysroot directory`

获取其他 Linux 实例的 CPU 数据。指定的目录是要检查的实例的根目录。

`-x, —hex`

对集合使用十六进制（例如 `0x3`）。默认是以列表格式打印（例如 `0,1`）。

`-V, —version`

显示版本信息并退出。

## Bug

CPU 系列、型号等基本概览始终基于第一个 CPU。

有时在 Xen Dom0 中内核报告的数据错误。

在虚拟硬件上，每个插槽的核心数等可能是错误的。

## 作者

Cai Qian `<>` Karel Zak `<>` Heiko Carstens `< >`

## 另另

(8)

## 可用性

`lscpu` 命令是 `util-linux` 包的一部分，可以通过以下方式获取

## LSINITRD

名称

`lsinitrd` - 显示 initramfs 镜像内容的工具

## 语法

```
lsinitrd [OPTION...] [<image> [<filename> [<filename> [...] ]]]
```

```
lsinitrd [OPTION...] -k <kernel-version>
```

## 描述

`lsinitrd` 显示 initramfs 镜像的内容。如果没有 `<image>`， `lsinitrd` 使用默认镜像 `/boot/<machine-id>/<kernel-version>/initrd` 或 `/boot/initramfs-<kernel-version>.img`。

## 选项

`-h, --help`

打印帮助信息并退出。

`-s, --size`

按大小对 initramfs 内容进行排序。

`-f, --file<filename>`

打印 `<filename>` 的内容。

`-k, --kver<kernel version>`

检查 `<kernel version>` 的 initramfs。

## 可用性

`lsinitrd` 命令是 `dracut` 包的一部分，可以通过以下方式获取

## 作者

Harald Hoyer

Amerigo Wang

Nikoli

## 相关参考

(8)
