
如有必要，`adduser`会为新用户创建主目录，从`/etc/skel`复制“骨架”文件，并允许系统管理员为用户设置初始密码。通常，系统上有两种用户和组：登录系统的用户以及为了各种任务而存在的“非用户”账户。从此以后，每个用户将指的是登录名称和 ID，默认情况下，Debian/Linux 中的每个用户都会赋予一个同名的对应组，允许人们轻松地访问其主目录。在 Debian GNU/Linux 下，小于或等于 1000 的 ID 由基础维护者分配用于各种目的。大于 1000 的 ID 留给用户和组。当用单个名称调用时，`adduser`创建一个该名称的用户。当用两个名称时，`adduser`假设第一个名称代表一个已存在的用户，第二个名称代表一个已存在的组。在这种情况下，用户被添加到该组。

## 选项

- `-system` 创建一个系统用户。该用户将被分配 shell `/bin/false` 并在密码字段中有一个星号。除非另有指定，否则不会将配置文件复制到用户的主目录中。
- `-home` 与 `-system` 调用时，使用该目录而不是配置文件中指定的默认。如果目录不存在，则创建它。
- `-group` 与 `-system` 结合使用时，创建一个与系统用户同名同 ID 的组。如果不与 `-system` 结合，则创建一个给定名称的组。
- `-quiet` 抑制消息。
- `-force-badname` 默认情况下，用户名组组必须由小写字母开头，后跟一个或多个小写字母或数字。此选项允许 `adduser` 或 `addgroup` 更加宽松。
- `-help` 显示说明。
- `-version` 显示版本和版权信息。
- `-debug` 显示大量的调试信息。

## 另请

`adduser.conf(5)`

## 版权

Copyright(c) 1995, Ted Haj, 大量引用原始 `adduser` 的版权(c) 1994, Ian Murdock.`adduser` 是自由软件；GNU 公共许可证二版或更高版本。不提供担保。Debian GNU/Linux 版本 1.9

# agetty

`agetty`—替代性的 Linux `getty`。

## 语法

```
agetty [-l login_program] [-m] [-t timeout] port baud_rate,... [term]
agetty [-l login_program] [-m] [-t timeout] baud_rate,..., port [term]
```

## 描述

`agetty` 打开一个 tty 端口并读取登录名称。它具有若干非标准功能，适用于硬线和拨号线路：它调整 tty 设置以适应校验位、删除、行结束以及输出字符。程序可以处理 7 位字符（奇校验、偶校验或空格校验）和 8 位字符（无校验）。识别以下特殊字符：`@` 和 Control+U（删除）；`#` 和退格键（删除）；回车和换行符（行结束）。

可选从兼容 Hayes 调制解调器的连接 信息中推断波特率。

当给定已打开的线路时不挂断（适用于回调应用程序）。

可选不显示 `/etc/issue` 文件的内容（仅限 System V）。

## 第八部分：特权命令

可选调用非标准的登录提示符而不是 `/bin/login`。

可选开启硬件流控。

强制线路为本地，无需载检测器。

此程序不使用 `/etc/gettydefs` (System V) 或 `/etc/gettyab` (SunOS 4) 文件。

## 参数

- `port`。如果指定了路径，tty 假设标准输入已连接到 tty 端口且已与远程用户建立连接。在 System V 下，`port` 参数前必须有一个 `-`。
- `baud rate`,一个或多个波特率的逗号分隔列表。每当 `atty` 接收到中断字符时，它就会循环遍历该列表。波特率应按降序排列，以便空字符（Ctrl@）也可以用于波特率切换。
- `term` 用于 `TERM` 环境变量的字符串。这会覆盖 `init(1)` 可能设置的值，并被 `login` 和 `shell` 继承。

## 选项

- 硬件（RTS/CTS）流控。由应用程序禁用软件（XON/XOFF）流控。

在写入登录提示符之前不显示 `/etc/issue` 的内容。在错误的波特率下接收文本可能会导致通信混乱；如果登录提示符之前文本太多，拨号脚本将失败。

列出所有波特率。

## 示例

本节显示了 `/etc/ittab` 文件的示例条目。

对于线路：

`tty1:con0x60:/sbin/agetty 9600 tty1`

对于带有 9600/2400/1200 波特率调制解调器的线路：

`tty1:dump:/agetty -mtty tty1 9600,2400,1200`

这些示例假设你使用的是 Linux 下的 `simpleinit(8)` init 程序。如果你使用的是类似 SysV 的 init（检查 `/etc/inittab` 是否提到了 "respawn"），请参考相应的手册页。

## ISSUE 转义字符

`/etc/issue` 文件可能包含用于显示系统名称、日期等内容的转义代码。所有转义代码均由一个反斜杠 (`\`) 后紧跟以下字母之一组成：

- `b` 插入当前行的条形码。
- `t` 插入当前日期。
- `s` 插入系统名称，操作系统名称。
- `l` 插入当前 tty 行的名称。
- `m` 插入机器的架构标识符，例如 i486。
- `n` 插入机器的代号，也称为主机名。
- `o` 插入机器的域名。
- `r` 插入操作系统的发布版本，例如 1.1.9。
- `u` 插入当前登录的用户数。
- `v` 插入字符串 "u users" 或 "n users"，其中 n 是当前登录的用户数。
- `V` 插入操作系统版本，例如构建日期等。

例如，在我的系统中，以下 `/etc/issue` 文件

`This is \n\o (\s|m\r) \t` 显示为

`This is thingol.orcan.dk (Linux i386 1.1.9) 18:29:30`

## 文件

- `/var/run/utmp`，在登录提示前打印（仅限 System V）
- `/etc/console` 报告（不使用 syslog3）
- `/etc/inittab`（Simpleinit(8) 配置文件）

## 缺陷

波特率功能（`-m` 选项）要求 `getty` 在拨号完成后尽快调度（对于以 2400 波特通信的调制调器为 30ms）。为了健壮性，请将 `-m` 选项与多个波特率命令行参数结合，以便启用处理。

`/etc/issue` 文件中的文本和登录提示使用 7 位字符和空格输出。

波特率功能（`-m` 选项）要求调制调器在置高 DCD 线后发送状态消息。

## 诊断

取决于程序的配置方式，所有诊断信息将写入控制台设备或通过 `syslog(3)` 报告。如果端口参数未指定终端设备、进程没有 utmp 条目（System V）等，则会产生错误消息。

## 作者

- W.Z. Venema (wietse@zw.win.tu.nl) 埃因霍夫科技大学数学与计算机科学系，Den Dolech, P.O. Box 513, 5600 MB Eindhoven, Netherlands。
- Orbaek (poe@daimi.au.dk), Linux 移植。

## 创建日期

1989年11月25日 周六 22:51:05 MET

## 最后修改

91/09/01 23:22:00

## 版本/发布

1.29

# archive

`archive`—Usenet 文章归档工具。

## 概要

```
archive [-a archive] [-f [-i index]] [-m] [-r] [input]
```

## 描述

`archive` 为标准输入中指定的文件创建副本。它通常作为 `under(8)` 的通道流运行，或者在 `archive(8)` 运行之前由脚本调用。

`archive` 读取命名的输入文件，如果没有提供文件则读取标准输入。输入被视为一组行。空行和以井号 (`#`) 开头的行会被忽略。所有其他行应指定要归档的文件名。如果文件名不是绝对路径，则被视为相对于 `/news/spool` 的路径。

文件被复制到归档内部的目录 `/news/spool/news.archive`。默认会创建一个模拟输入文件的层级结构；例如，输入文件 `comp/sources/unix/2211`（comp.sources.unix 新闻组中的文章 2211）被复制到 `/news/spool/news.archive/comp/sources/unix/2211`。如果使用了 `-f` 标志，则所有目录将被扁平化，并将斜杠替换为点。在这种情况下，文件被复制到 `/news/spool/news.archive/comp.sources.unix/2211`。

如果使用了 `-i` 标志，`archive` 会为其复制的每篇文章附加一个唯一的索引文件。此处包含目标名称以及 Message-ID 和 Subject 头信息。

例如，一个用于归档大多数源码新闻组的 `newsfeeds(5)` 条目如下：
