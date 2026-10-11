
fuser 显示使用指定文件或文件系统的进程 PID。

killall 向运行任何指定命令的所有进程发送信号。

pstree 以树形显示运行中的进程。

# Sed

## 目录

Sed 软件包包含 `sed` 程序。

## 描述

`sed` 是一个流编辑器。流编辑器用于对输入流（文件或来自管道输入）进行基本的文本转换。

# Syslogd

## 目录

Syslogd 软件包包含 `klogd` 和 `syslogd` 程序。

## 描述

### klogd

`klogd` 是一个系统守护进程，用于拦截并记录 Linux 内内核消息。

### syslogd

Syslogd 提供了许多现代程序使用的日志类型。每条日志消息至少包含一个时间和主机名字段，通常还包含程序名称字段，但这取决于日志记录程序的可靠性。

# Sysvinit

## 目录

Sysvinit 软件包包含 `pidof`, `last`, `lastb`, `mesg`, `utmpdump`, `wall`, `halt`, `init`, `killall5`, `poweroff`, `reboot`, `runlevel`, `shutdown`, `sulogin` 和 `telinit` 程序。

## 描述

### pidof

`pidof` 查找指定命名程序的进程 ID (pids)，并将这些 ID 打印到标准输出。

### last

`last` 反向搜索 `/var/log/wtmp` 文件（或由 `-f` 标志指定的文件），显示自该文件创建以来所有登录（注销）的用户列表。

### lastb

`lastb` 与 `last` 相同，不同之处在于默认显示 `/var/log/btmp` 文件的日志，该文件包含了所有错误的登录尝试。

### mesg

`mesg` 控制其他对你终端的访问。它通常用于允许或禁止其他用户写入你的终端。

### utmpdump

`utmpdump` 以用户友好的格式将文件（通常为 `/var/run/utmp`）的内容打印到标准输出。

### wall

`wall` 向所有 `mesg` 权限设置为 yes 的登录用户发送消息。

### halt

`halt` 在 `/var/log/wtmp` 文件中记录系统已关闭，然后告诉内核停止、重启或关机系统。如果在系统不在运行级别 0 或 6 的情况下调用 `halt` 或 `reboot`，则将调用 `shutdown`（带有 `-h` 或 `-r` 标志）。

### init

`init` 是所有进程的父进程。它的主要作用是从存储在 `/etc/inittab` 文件中的脚本创建进程。该文件通常包含一些条目，导致 `init` 在用户可以登录的每一行生成 `getty`。它还控制任何特定系统所需的自主进程。

### killall5

`killall5` 是 SystemV 的 `kill` 命令。它向除自身会话进程外的所有进程发送信号，因此它不会杀死运行该脚本的 shell。

### poweroff

`poweroff` 等同于 `shutdown -h -p now`。它停止计算机并关闭电源（当使用兼容 APM 的 BIOS 且内核中启用 APM 时）。

### reboot

`reboot` 等同于 `shutdown -r now`。它重启计算机。

### runlevel

`runlevel` 读取系统 `utmp` 文件（通常为 `/var/run/utmp`）以定位运行级别记录，然后将之前的和当前的系统运行级别打印到标准输出，中间用单个空格分隔。

### shutdown

`shutdown` 以安全的方式关闭系统。所有登录用户都会收到系统即将关闭的通知，并阻塞登录。

### login

`init` 在系统进入单用户模式时调用 `slogin`（这是通过 `/etc/inittab` 中的条目实现的）。当 `init` 从启动监视器（例如 LILO）接收到 `-b` 标志时，它也会尝试执行登录。

### telinit

`telinit` 向 `init` 发送相应的信号，告诉它更改到哪个运行级别。

# Tar

## 目录

`tar` 软件包包含 `tar` 和 `rmt` 程序。

## 描述

### tar

`tar` 是一种归档程序，用于从名为 `tarfile` 的归档文件中存储和提取文件。

### rmt

`rmt` 是远程转储和恢复程序使用的程序，通过进程间通信连接操作磁带驱动器。

# Textutils

## 目录

Textutils 软件包包含 `cat`, `cksum`, `comm`, `split`, `cut`, `expand`, `fmt`, `fold`, `head`, `md5sum`, `nl`, `od`, `paste`, `pr`, `ptx`, `sort`, `split`, `tac`, `tail`, `tr`, `tsort`, `expand`, `uniq` 和 `wc` 程序。

## 描述

### cat

`cat` 将文件或标准输入连接到标准输出。

### cksum

`cksum` 打印每个指定文件的 CRC 校验和和字节数。

### comm

`comm` 按行比较两个排序后的文件。

### csplit

`cplit` 将按 (a) 模式分隔的文件部分输出到文件 `xx01`, `xx02`, ... 中，并将每个部分的字节数输出到标准输出。

### cut

`cut` 将指定文件中选定的行部分打印到标准输出。

### expand

`expand` 将文件中的制表符转换为空格，写入标准输出。

### fmt

`fmt` 重新格式化指定文件中的每个段落，写入标准输出。

### fold

`fold` 对每个指定文件（默认认为标准输入）中的输入行进行折叠，写入标准输出。

### head

将每个指定文件的前 `xx`（默认 10）行打印到标准输出。

### join

`join` 根据公共字段连接两个文件中的行。

### md5sum

`md5sum` 打印或检查 MD5 校验和。

### nl

`nl` 将每个指定文件写入标准输出，并添加行号。

### od

`od` 将指定文件的无歧义表示（默认为八进制字节）写入标准输出。

### paste

`paste` 写入由顺序对应的行组成的行。

### pr

`pr` 以格式化页面打印文件。

### ptx

`ptx` 处理文件以便打印机输出。

### sort

`sort` 对文本行进行排序。

### split

`split` 将文件分成若干部分。

### tac

`tac` 反转每个文件的行。

### tail

`tail` 打印每个文件的最后部分。

### tr

`tr` 翻译或删除字符。

### tsort

`tsort` 对文本进行排序。

### uniq

`uniq` 过滤重复行。

### wc

`wc` 统计字节、单词和行数。

# Linux From Scratch

### sort

`sort` 对文本进行排序。

### ptx

`ptx` 处理文件用于打印机输出。

### split

`split` 将文件分成若干部分。

### tac

`tac` 反转每个文件的行。

### tail

`tail` 打印每个文件的最后部分。

### tr

`tr` 翻译或删除字符。

### tsort

`tsort` 对文本进行排序。

### uniq

`uniq` 过滤重复行。

### wc

`wc` 统计字节、单词和行数。

# Linux From Scratch

### wc

`wc` 统计字节、单词和行数。

# Util Linux

## 目录

Util–linux 软件包包含 `arch`, `dmesg`, `kill`, `more`, `umount`, `agetty`, `blockdev`, `cfdisk`, `ctrlaltdel`, `elvtune`, `fdisk`, `fsck.minix`, `hwclock`, `kbdrate`, `losetup`, `mkfs`, `mkfs.bfs`, `mkfs.minix`, `mkswap`, `swapoff`, `swapon`。

## 描述

### arch

`arch` 打印机器架构。

### dmesg

`dmesg` 用于检查或控制内核缓冲区（启动消息）。

### kill

`kill` 向进程发送指定信号。

### more

`more` 是一个分页查看文本的过滤器。

### mount

`mount` 将文件系统从设备挂载到目录（挂点）。

### umount

`umount` 卸载文件系统。

### agetty

`agetty` 打开 tty 端口，提示登录名称并调用 `/bin/login` 命令。

### blockdev

无可用描述。

### cfdisk

`cfdisk` 是一个基于 `libncurses` 的分区表管理器。

### ctrlaltdel

`ctrlaltdel` 设置 CTRL+ALT+DEL 键组合的功能（硬重启或软重启）。

### elvtune

`elvtune` 允许按块设备队列调整 I/O 调度。

### fdisk

`fdisk` 是一个分区表管理器。

### fsck.minix

`fsck.minix` 对 Linux MINIX 文件系统进行一致性检查。

### hwclock

`hwclock` 查询并设置硬件钟（也称为 RTC 或 BIOS 时钟）。

### kbdrate

`kbdrate` 重置键盘重复速率和延迟。

### losetup

`losetop` 设置并控制循环设备。

### mkfs
