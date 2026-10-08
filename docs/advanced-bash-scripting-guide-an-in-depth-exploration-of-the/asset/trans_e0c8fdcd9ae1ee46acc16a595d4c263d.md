

# 高级 Bash 脚本指南

wall

这是 "write"写入）的缩写，即向登录到网络的每个终端的所有用户发送消息。它主要是一个系统管理员的工具，非常有用，例如在需要警告所有人系统将因问题即将关机时（参见示例 19-1）。

```bash
$ wall "System going down for maintenance in 5 minutes!"
Broadcast message from bozo (pts/1) Sun Jul 8 13:53:27 2001...
System going down for maintenance in 5 minutes!
```

如果我禁用了对特定终端的访问，那么 `wall` 无法向该终端发送消息。

## 信息与统计

uname

向标准输出输出系统规格（操作系统、内核版本等）。使用 `-a` 选项调用时，会提供详细的系统信息（参见示例 16-5）。`-s` 选项仅显示操作系统类型。

```bash
$ uname
Linux

$ uname -s
Linux

$ uname -a
Linux iron.iron 2.6.15-2054_FC5 #1 Tue Mar 14 15:48:33 EST 2006 1686 1686 1386 GNU/Linux
```

arch

显示系统架构。等同于 `uname -m`。参见示例 11-27。

```bash
$ arch
1686

$ uname -m
1686
```

lastcomm

提供以前命令的信息，存储在 `/var/account/pacct` 文件中。可以通过选项指定命令和用户名。这是 GNU 统计工具之一。

lastlog

列出所有用户的最后登录时间。引用引用 `/var/log/lastlog` 文件。

```bash
$ lastlog
root              tty       Fri Dec 7 18:43:21 -0700 2001
bin               **Never logged in**
daemon            **Never logged in**
...
bozo              tty       Sat Dec 8 21:14:29 -0700 2001
```

lsof

列出打开的文件。此命令输出所有打开文件的详细表格，并提供关于其所有者、大小等的信息。`lsof` 可以通过管道传递 `grep` 或 `awk` 以分析结果。`lsof` 命令是一个很有用且复杂的管理工具。如果你无法确定文件系统上哪些文件仍处于打开状态，`lsof` 可以追踪入侵或攻击。`-i` 选项列出网络套接文件。

| COMMAND | USER | FD | TYPE | SIZE | NAME |
| :--- | :--- | :--- | :--- | :--- | :--- |
| init | root | 1,5 | REG | 30748 | /sbin/init |
| init | root | 1,5 | REG | 73120 | /lib/libc.so.3.so |
| init | root | 1,5 | REG | 93168 | /lib/ld-linux.so.so |
| cdmgr | root | 1,5 | REG | 36956 | /sbin/cdmgr |
| firefox | bozo | 32u | ipv4 | 9956 | 66.0.118.137:5796 |
| firefox | bozo | 38u | ipv4 | 10535 | 66.0.118.137:5770 |

strace

用于追踪系统调用和信号的系统调试。`strace` 有助于诊断程序为何无法运行（可能是由于缺少库或相关情况）。

```bash
$ strace df
execve("/bin/df", ["df"], /* args */) = 0
uname(sys="Linux", node="bozo.localdomain", ...) = 0
brk(0) = 0
```

ltrace

库追踪和调试工具，用于追踪给定命令调用的库。这是 Solaris `truss` 的 Linux 等版本。

```bash
$ ltrace df
__libc_start_main(0x804a910, 1, 0xbf5894a, 0x80fb70, 0x<unfinished>) = 0
setlocale(6, "*") = "en_US.UTF-8"
bindtextdomain("coreutils", "/usr/share/locale") = "/usr/share/locale"
textdomain("coreutils") = "coreutils"
__cxa_atexit(0x804b650, 0, 0, 0xbf58bf90) = 0
getenv("DF_BLOCK_SIZE") = NULL
```

`nc` (netcat) 工具是一个用于连接和监听 TCP 和 UDP 端口的完整工具包。它可以作为诊断和测试工具，以及简单的脚本型 HTTP 客户端。

```bash
$ nc localhost.localdomain 25
220 localhost.localdomain ESMTP Sendmail 8.13.1/8.13.1;
Thu, 31 Mar 2005 15:41:35 -0700
```

### 示例 17-5. 连接远程服务器进行 ident

```bash
#!/bin/sh
## 使用 netcat 复制 Dave 的 ident-scan 东西。噢，他会很生气的。
## 参数: 目标端口 [port ...]
## 同时使用标准输出和标准错误。

## 优点: 比 ident-scan 慢慢，让 inetd 触发警报的机会更少，并且只命中你指定的几个守护进程端口。
## 缺点: 需要数字参数，输出简洁，且当从高源端口来时对 r-services 不起。
## 脚本作者: Hobbit ~hobbit@avian.org~
## 经许可在 ABS Guide 使用。

E_BADARGS=6      # 需要至少两个参数。
TWO_WINKS=3       # 睡眠多久。
THREE_WINKS=3
# 认证 "tap ident" 端口。
IDPORT=113
RAND1=999
RAND2=31337
TIMEOUT0=0
TIMEOUT1=8
TIMEOUT2=4

case "${2}" in
  "") echo Need HOST and at least one PORT."; exit E_BADARGS ;;
esac

# 探测一次看它们是否正在运行 ident。
if nc -z -w $TIMEOUT0 "$1" "$IDPORT" >/dev/null 2>&1; then
  echo "$1 is running ident."
else
  echo "oops, $1 isnt running ident."
  exit 0
fi

# 生成一个随机的端口。
PORT=$(expr $RAND1 + $RAND2)

# 连接多长时间。
while true; do
  nc -v -w $TIMEOUT1 "$1" "$PORT" >/dev/null 2>&1; then
    break
  fi
  sleep $THREE_WINKS
done
```

du

递归显示（磁盘）文件使用情况。除非另有指定，默认为当前工作目录。

```bash
$ du -ach
1.0k /wi.sh
1.0k /tst.sh
1.0k /random.file
6.0k
6.0k total
```

free

以表格形式显示内存和缓存使用。输出显示空闲等。

```bash
$ free
Mem: 30504 28624 15820 1608 16376
buffers/cache: 10640 19864 5412
Swap: 68540 3128 65412
```

df

以表格形式显示文件使用情况。

| Filesystem | 1-blocks | Used | Available | % | Mounted on |
| :--- | :--- | :--- | :--- | :--- | :--- |
| /dev/h5 | 273262 | 92607 | 166547 | 36% | / |
| /dev/h8 | 222525 | 123951 | 87085 | 59% | /home |
| /dev/h7 | 140896 | 107574 | 26148 | 80% | /usr |

dmesag

所有系统启动消息到标准输出。对于调试和确定安装了哪些设备驱动及其中断非常有用。dmesag 的输出当然可以在脚本中使用 `grep`、`sed` 或 `awk` 进行解析。

```bash
$ dmesag | grep /dev/h2
Kernel command line: root=/dev/h2
hda: IBM-DLGA-23080, ATA DISK drive
hda: 601574 sectors (308 MB) W/96KB Cache, Csh=746/128/63
hda h2 h3 < h5 h7 > h4
```

lsdev

列出设备，即安装的硬件。

| Device | I/O Ports | IRQ |
| :--- | :--- | :--- |
| cascade | 4 | 080 |
| dma | 0000 | 01f |
| dml1 | 00c | 0df |
| dma2 | 000f | ff |
| ide0 | 14 | 1f7 |

procinfo

从 /proc 伪文件提取列表和信息。提供了非常大量的列表。

```bash
$ procinfo | grep Bootup
Bootup: Wed Mar 21 15:15:50 2001 Load average: 0.04 0.21 0.34 1/47 .829
```

stat

对给定文件（或目录文件）或一组文件提供详细且冗余的统计信息。如果目标文件不存在，stat 将返回错误消息。

```bash
$ stat nonexistent-file
nonexistent-file: No such file or directory
```

在脚本中，你可以使用 stat 提取文件（以及文件系统）的信息并相应赋值变量。

```bash
#!/bin/bash
# fileinfo2.sh

# 根据 Joël Bourquard 的建议和 . . .
# http://www.linuxquestions.org/questions/showthread.php?t=410766
```

FILENAME=testfile.txt

