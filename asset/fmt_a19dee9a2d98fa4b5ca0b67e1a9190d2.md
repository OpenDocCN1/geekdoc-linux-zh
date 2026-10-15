
`less` `/etc/syslog.conf`

```
#ident "@)syslog.conf    1.4    96/10/11      * SunOS 5.0 */
# Copyright (c) 1991-1993, by Sun Systems, Inc.
# syslog配置文件。
# 此文件由 m4 处理，因此对匹配保留字的名称要小心。
# 同时，在 ifdefs 中，包含逗号的参数必须加引号。
*.notice                                              @loghost
*err:kern.notice;auth.notice                         /dev/console
*err:kern.debug;daemon.notice;mail.crit;daemon.info    /var/adm/messages
*alert:kern.err;daemon.err                             operator
*alert                                                root
```

## 第7章：Shell、脚本与调度 163

例如，如果当前工作目录是 `/bin`，且你输入命令

```
mkdir oracle
```

那么新目录将是 `/bin/oracle`。然而，如果你输入命令

```
mkdir /oracle
```

新目录将是 `/oracle`。对于交互式使用，通常使用相对目录名；但是，脚本应始终包含绝对目录引用。

## more

`more` 命令打印文件内容，类似于 `less` 命令，但它仅允许对文件进行滚动查看。该命令的格式如下：

```
more filename
```

要滚动查看磁盘设备配置文件 (`/etc/format.dat`) 的内容，你可以使用以下命令：

```
more /etc/format.dat
```
#pragma ident "G(#)format.dat 1.21  98/01/24 SMI"
# Copyright (c) 1991.1998 by Sun Microsystems, Inc.
# All rights reserved.
# Data file为 'format' 程序的数据文件。该文件定义了已知的
# 磁盘、磁盘类型和分区映射。
# 这是 Emux MD21 控制器支持的磁盘列表。
disk_type = "Microlis 1355*"
  : ctrl = 1018 : acyl = 2 : pcyl = 1024 : nhead = 8 : nsect = 34 \
  : rpm = 3600 : bpt = 20832

`more` 命令有许多可以交互式执行子命令。例如，移动一个只需按下空格键，或者移动一行只需按下回车键。`more` 命令还支持通过 `/pattern` 命令进行搜索。

## pwd

`pwd` 命令以绝对路径打印当前工作目录。该命令的格式如下：

```
pwd
```

例如，如果你切换目录到 `/etc` 并执行 `pwd` 命令，你会看到以下结果：

```bash
$ cd /etc
$ pwd
/etc
```

## rmdir

`rmdir` 命令删除目录。然而，相关的目录必须为空，`rmdir` 命令才能执行成功。该命令的格式如下：

```
rmdir directory
```

例如，如果当前工作目录是 `/usr/local`，而你想删除 `oldstuff` 目录，你可以使用此命令：

```
rmdir oldstuff
```

然而，你也可以使用命令

```
rmdir /usr/local/oldstuff
```

来删除该目录。对于交互式使用，通常使用相对目录名；但是，脚本应始终包含绝对目录引用。

## tail

`tail` 命令显示文件的最后一页。该命令的格式如下：

```
tail filename
```

`tail` 命令对于查看非常长文件的最后几行有用。例如，要显示 Web 日志 (`/usr/local/apache/logs/access_log`) 的第一页，你使用以下命令：

```bash
$ tail /usr/local/apache/logs/access_log
192.168.205.238 - [12/Feb/2002:09:35:59 +1000]
"GET /images/picture10.gif HTTP/1.1" 200 53
192.168.205.238 - [12/Feb/2002:09:35:59 +1000]
"GET /images/picture1.gif HTTP/1.1" 200 602
192.168.205.238 - [12/Feb/2002:09:35:59 +1000]
"GET /images/picture5.gif HTTP/1.1" 200 7090
192.168.205.238 - [12/Feb/2002:09:35:59 +1000]
"GET /images/picture66.gif HTTP/1.1" 200 997
192.168.205.238 - [12/Feb/2002:09:35:59 +1000]
"GET /images/picture49.gif HTTP/1.1" 200 2386
192.168.205.238 - [12/Feb/2002:09:36:09 +1000]
"GET /servlet/SimpleServlet HTTP/1.1" 200 10497
```

`tail` 命令还有一个选项，允许你持续监控文件中产生的所有新条目。这对于监控像 Apache 这样的实时服务非常有用，因为你需要实时观察发生的任何错误。该命令的格式如下：

```
tail -f filename
```

### 总结

在本章中，我们检查了如何管理文件和目录，以及如何与 shell 工作。此外，我们还检查了命令。

## 第二部分：系统基础

## 进程管理

进程是操作系统的核心。Solaris 提供了并发运行进程的能力。类 Unix 系统的一个吸引人的特性是，进程可以通过单个 PID 来标识。

### 核心概念

列进程的主要命令是 `ps`，它是高度可配置的具有许多命令行选项。在本节中，你将查看当前运行的进程。

## 发送信号

由于所有进程都可以通过单个 PID 来标识，可以在 C 语言中使用 `signal()` 函数向其他进程发送信号来管理进程，也可以直接在 shell 中发送信号。

## 第8章：进程管理 169

client 3% ls
httpd.conf access.conf srm.conf
client 4% fg

一个非常有用的命令是 `kill` 命令，它用于直接向系统上的任何进程发送信号。它通常带有两个参数调用——类型和 PID（进程 ID）。例如，如果你更改了互联网服务器守护进程的配置文件，你必须向该守护进程发送信号，让它重新读取配置文件。请注意，你不需要重启守护进程本身：这是基于进程的操作系统优势之一，它便于了进程间通信。

```
# kill -167
```

这会强制 `inetd` 重新读取其配置文件并更新其内部设置。`-1` 参数代表 SIGHUP 信号，意思是“挂断（hang up）”。想象一种情况，你需要临时关闭 inetd 以进行安全检查。你可以使用 `-9` 参数（SIGKILL 信号）向进程发送 kill 信号：

```
# kill -9 167
```

虽然 SIGHUP 和 SIGKILL 是 shell 中常用的信号，但程序还会使用其他信号，它们定义在 `signal.h` 头文件中。向进程发送信号的另一个可能后果是，进程不是“挂断”或“被杀死”，而是可能会退出并转储核心文件（core file），该文件是接收消息进程的内存映像。此结果对于调试非常有用，尽管过多的核心文件会迅速填满你的系统！你可以通过传递 `kill -l` 选项随时获取可用信号列表：

```
$ kill -l
HUP INT QUIT KILL ABERT EMP FPE KILL SIG SEGV SYS PIPE
ALRM TERM USR1 USR2 WINCH URG POLL TSTP CONT
TTIN TTOU VTARM PROF XCPU XFSZ WAITING LWP FREE THAW
RTMIN RTMAX+1 RTMIN+2 RTMIN+3 RTMAX-3 RTMAX-2 RTMAX-1
RTMAX
```

### 步骤

以下是常用于管理进程的步骤。

## 列出进程

你可以使用 `ps` 命令列出本地系统上所有当前活动的进程。默认情况下，`ps` 会打印执行 `ps` 命令的用户的进程：

![](img/11bcccd1804574cca0c3018732958dd5_198_0.png)

```
$ ps
PID TTY TIME CMD
```
