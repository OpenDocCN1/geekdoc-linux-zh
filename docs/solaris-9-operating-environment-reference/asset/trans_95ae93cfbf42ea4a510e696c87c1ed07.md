

# 410 ftptp

verbose 切换详细模式。在详细模式下，FTP 服务器的所有响应都将显示出来。此外，如果开启了详细模式，当文件传输完成时，将报告有关传输效率的统计数据。默认情况下，如果 ftp 命令来自终端，则开启详细模式，否则关闭。

```
? [command]
```

help（帮助）命令的同义词。
你可以使用引号（""）引用包含空格的命令参数。如果你没有指定任何未标记为可选的命令参数，ftp 将会提示你输入该参数。

# 中止文件传输

要中止文件传输，请使用终端中断键。发送传输将立即停止。接收传输将通过向远程服务器发送 FTP 协议 ABOR 命令并丢弃任何后续数据来停止。完成此操作的速度取决于远程服务器对 ABOR 处理的支持。如果远程服务器不支持 ABOR 命令，则在远程服务器完成请求的文件之前，不会显示 ftp> 提示符。
当 ftp 完成任何本地处理并正在等待远程服务器的回复时，终端中断键序列将被忽略。在此模式下，长时间延迟可能是由于上述 ABOR 处理，或者由于远程服务器的意外行为（包括违反 ftp 协议）导致的。如果延迟由于远程服务器的意外行为，你必须手动杀死本地 ftp 程序。

# 文件命名规范

作为 ftp 命令参数的本地文件将根据以下规则处理。
如果你指定了文件名 -

# 文件传输参数

FTP 规范中的以下参数可能会影响文件传输。

## 表示类型

ASCII、EBCDIC、image 或具有指定字节大小的本地字节大小（主要用于 PDP-10s 和 PDP-20s）。网络 ASCII 和 EBCDIC 类型具有额外的子类型，指定垂直格式控制（如换行符和分页符）是直接透传（非打印）、以 TELNET 格式提供（TELNET 格式控制），或以 ASA (FORTRAN) 格式提供（回车控制 (ASA)）。ftp 支持网络 ASCII（仅限非打印子类型）和 image 类型，以及与 TENEX 机器通信时字节大小为 8 的本地字节大小。

## 文件结构

file（无记录结构）、record（记录）或 page（页）。ftp 仅支持默认值 file，即 file。

## 传输模式

stream（流）、block（块）或 compressed（压缩）。ftp 仅支持默认值 stream，即 stream。

# 使用

largefile(5) 用于描述 ftp 遇到大于或等于 2 Gbytes (**31 字节**) 的文件时的行为。

ftp 命令已启用 IPv6。请参见 ip6 (7P)。

# 文件

~/.netrc

# 属性

参见 attributes(5) 获取以下属性的描述：

| 属性类型 | 属性值 |
|---|---|
| Availability CSI | SUNmbip |
| CSI | Enabled |

# 参见

ls(1), rcp(1), sh(1), tar(1), in.ftpd(1M), open(3C), ftpusers(4), netrc(4), attributes(5), largefile(5), ip6(7P)

# ftpcount — 显示每个 FTP 服务器类的当前用户数

# 概要

/usr/sbin/ftpcount [-V]

# 描述

使用 Solaris 9 操作系统环境中新增的 ftpcount 命令，显示在 ftpaccess(4) 文件定义的每个 FTP 服务器类的当前登录用户数和登录限制。

# 选项

+   -V 显示程序的版权和版本信息，然后退出。

# 示例

以下示例显示了系统 mopoke 目前没有配置任何 FTP 用户。

```
mopoke% ftpcount
Service class realusers - 1 users (no maximum)
Service class guestusers - 0 users (no maximum)
Service class anonymouss - 0 users (no maximum)
mopoke%
```

# 退出状态

0 成功完成。
>0 发生错误。

# 文件

/etc/ftpd/ftpaccess
用于配置 FTP 服务器运行的文件。
/var/run/ftp.pids-classnames
FTP 服务器运行文件。

# 属性

参见 attributes(5) 获取以下属性的描述。

| 属性类型 | 属性值 |
|---|---|
| Availability | SUNWftpu |

# 参见

+   * ftpwho(1), in. ftpd(1M), ftpaccess(4), attributes(5)

# ftpwho 413

# ftpwho — 显示每个 FTP 服务器用户的当前进程信息

# 概要
/usr/sbin/ftpwho [-V]

# 描述
使用 Solaris 9 操作系统环境中新增的 ftpwho 命令，显示每个到到 服务器登录的用户的当前进程信息。这些信息是 ftpcount(1) 命令显示之外的信息。

# 选项
-V 显示程序的版权和版本信息，然后退出。

# 示例
以下示例显示了 ftpwho 命令的输出。
mopoke@ ftpwho
Service class realusers:
winsor 596 0.0 1.9 2648 2176 ? S 19:54:45 0:00 ftppd:
  castle: winner: IDLE
  - 1 users (no maximum)
Service class guestusers:
  - 0 users (no maximum)
Service class anusers:
  - 0 users (no maximum)
mopoke@

# 退出状态
0 服务完成。
>0 发生错误。

# 文件
/etc/ftpd/ftpaccess
用于配置 FTP 服务器运行的文件。
/var/run/ftp.pids-classnames
FTP 服务器运行文件。

# function

# 属性

参见 attributes(5) 获取以下属性的描述。

| 属性类型 | 属性值 |
| --- | --- |
| Availability | SUNWftpu |

# 参见

ftpcount(1), ps(1), in.ftpd(1M), ftpaccess(4), attributes(5)

# function — 定义 Shell 函数的 Shell 内置命令

# 概要

```
ksh
function identifier { list; }
identifier() { list; }
```

# 描述

# Korn Shell

function 定义了一个通过 identifier 引用的函数。函数体是花括号 {} 内的命令列表。

或者，你也可以通过省略 function 关键字并在 identifier 后面加上一组括起来括号来定义函数。

# 示例

以下示例创建了一个名为 status() 的函数，它会返回当前工作目录的名称并列出它。

```
$ status() { cd $*; pwd;ls; }
$
$ functions
function status
{
cd $*; pwd;ls; }
$
$ status /home
/home
TT_DB bill last+found
$ 
```

以下示例创建了一个名为 scp() 的函数用于安全复制。它防止覆盖现有文件。当你连续执行两次相同的命令时，第二个命令将不会执行，且 scp() 函数将显示错误消息。

```
$ scp()
>
> if test ! -s "$2"
```

> then cp "$1" "$2"
> else echo "scp: cannot copy $1: $2 exists"
> fi
> )
$ scp junk junk1
$ scp junk junk1
scp: cannot copy junk: junk1 exists
$ 
```

# 属性

参见 attributes(5) 获取以下属性的描述：

| 属性类型 | 属性值 |
| --- | |
| Availability | SUNWcsu |

# 参见

ksh(1), attributes(5)

```
castle@ gcore 450
gcore: core.450 dumped
castle@ ls -1 core*
-rw-rw-rw- 1 winner 66216 Jan 16 14:16 core.450
```

# 418

# gencat

```
core.450: ELF 32-bit MSB core file SPARC Version 1, from 'cat'
castle%%
```

以下示例尝试为不存在的进程 ID 461 创建核心映像。注意 gcore 创建了一个名为 core.o 的输出文件，但它是空文件。

```
castle%% gcore 461
castle%% ls -l *
-rw-rw-rw- 1 winner 0 Jan 14 15:50 core.o
castle%%
```

# 退出状态

0 成功。
非零 失败（例如不存在的进程）。

# 文件

```
core.process-id
```

核心映像。

# 属性

参见 attributes(5) 获取以下属性的描述：

| 属性类型 | 属性值 |
| --- | --- |
| Availability | SUNwtoo (32-bit)
SUNwtoox (64-bit) |

# 参见

```
kill(1), core(4), proc(4), attributes(5)
```

# gencat — 生成格式化消息目录

# 概要

/usr/bin/gencat catfile msgfile...

# 描述

使用 gencat 命令将消息文本源文件（或）msgfile 合并到格式化消息数据库 catfile。如果 catfile 不存在，则创建它。如果 catfile 存在，则将其消息包含在新的 catfile 中。如果集合和消息号冲突，msgfile 中定义的新消息文本将替换 catfile 中当前的旧消息文本。你输入 gencat 的消息文本源文件（或文件集）可以包含集合和消息号，也可以仅包含消息号，此时假设集合为 NL_SETD（参见 nl_types(5)）。

