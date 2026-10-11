
- 第三行 `Cpu(s)` 显示系统当前的 CPU 利用率。在本例中，CPU 空闲率为 `98.7%`。

- 第四行 `Mem` 和第五行 `Swap` 提供了内存信息。这与命令中的信息相同。其余行显示系统上所有的活动进程，按 CPU 使用率（`%CPU` 列）排序。即默认显示计算密集型进程。`top` 提供了多个命令行选项和交互选项供使用。

## 如何识别内存占用率最高的进程？

在显示 `top` 输出时，按下 `F`，将显示以下消息并显示所有可排序的字段，按下 `n`（代表内存）并按回车。这将按内存使用率对 `top` 输出中的进程进行排序。当前排序字段：通过字段字母选择排序，按任何其他键返回。

## 如何在 top 输出中添加额外字段（例如 CPU Time）？

在 `top` 命令运行时，按下 `f`，将显示以下消息并显示所有可显示的字段，按下 `l`，这会将 `CPU Time` 添加到显示列中。当前字段：通过字段字母切换字段，按任何其他键返回。

## 如何获取运行中进程的完整路径和参数？

在 `top` 命令运行时，按下 `c`，将显示如下所示的进程完整路径。

```
PID USER PR NI VIRT RES SHR S %CPU %MEM TIME+ COMMAND
11912 apache 15 0 31828 13m S 10.2 0:46.35 httpd
```

## 如何在 top 命令中查看单个 CPU？

当 `top` 命令运行时，按下 `1`（数字一），将显示如下所示的单个 CPU 性能数据。

（注：此处原文似乎缺失了数字“1”的描述，根据逻辑推断为按下 `1`）

（此处根据原文内容翻译，保持结构对应）

# Linux 破解

Ajay Kumar Tiwari

# 破解 91. ps 命令

`ps` 命令（进程状态）将显示所有活动进程的快照信息。

语法：`ps [options]`

## 如何显示系统中运行的所有进程？

使用 `ps aux`，如下所示。

```
# ps aux | more
USER PID %CPU %MEM VSZ RSS TTY STAT START TIME COMMAND
root 0.0 0 2044 588 ?Ss Jun27 0:00 init [5]
apache 0.0 1.6 23736 17556 ?S Jul26 0:40 /usr/local/apache2/bin/httpd
apache 0.0 1.3 20640 14444 ?S Jul26 0:37 /usr/local/apache2/bin/httpd
```

# 打印进程树

## 打印进程树

你可以使用 `ps axuf` 或 `ps -ejH` 以树状格式显示进程。树形结构将有助于直观地查看进程及其父进程。为了清晰起见，下方输出中的某些列被截断了。

# ps axuf

注意：你也可以使用 `ptree` 命令以树形结构显示进程。

# 查看特定用户的进程

以下命令显示由 Linux 用户名 `oracle` 所有的所有进程：

```
$ ps U oracle
PID TTY
5014 ?
7124 ?
8206 ?
8852 ?
8854 ?
8911 ?
STAT
Ss
Ss
Ss
Ss
Ss
TIME COMMAND
0:01 /oracle/bin/tnlsnr
0:00 ora_q002_med
0:00 ora_cqj0_med
0:01 ora_pmon_med
0:00 ora_psp0_med
0:02 oracled (LOCAL=NO)
```

# 查看当前用户的进程

以下命令显示由当前用户的所有进程。

```
$ ps U $USER
PID TTY
10329 ?
10330 pts/1
STAT
S
Ss
# TIME COMMAND

0:00 sshd: ramesh@pts/1,pts/2

0:00 -bash

10354 pts/2
10530 pts/1
Ss+
R+
0:00 -bash
0:00 ps U Umesh
Ajay Kumar Tiwari
```

# 技巧 92. df 命令

`df` 命令（`disk free`）显示已挂载文件系统上可用的总空间和可用空间。
语法：`df [options] [name]`

# 我的系统上有多少 GB 的可用磁盘空间？

使用 `df -h` 以人类可读的格式显示值（例如：`K` 代表 `Kb`，`M` 代表 `Mb`，`G` 代表 `Gb`）。在下面的输出中，`/` 文件系统有 `17GB` 可用磁盘空间，`/home/user` 文件系统有 `70GB` 可用。

```
# df -h

| Filesystem Size Used Avail Use% Mounted |
| --- --- --- --- --- --- |
| /dev/sda1 | 64G | 44G | 17G | 73% | / |
| /dev/sdb1 | 137G | 67G | 0G | 49% | /home/user |
```

# 我的系统上是什么什么类型的文件系统？

选项 `-T` 将显示文件系统类型的信息。在此示例中，`/` 和 `/home/user` 文件系统是 `ext2`。选项 `-a` 将显示所有文件系统，包括系统使用的大小为 `0` 的特殊文件系统。

# df -Tha

```
| Filesystem Type Size Used Avail Use% Mounted on |
| --- --- --- --- --- --- |
| /dev/sda1 | ext2 | 64G | 17G | 73% | / |
| /dev/sdb1 | ext2 | 137G | 67G | 49% | /home/user |
| noneproproc00 | proc | | | | /proc |
| noneysfs00 | sysfs | | | | /sys |
| nonedevpts00 | devpts | | | | /dev/pts |
| nonetmpfs | tmpfs | 2.0G | 2.0G | 0% | /dev/shm |
```

# 技巧 93. kill 命令

`kill` 命令可用于终止运行中的进程。通常，此命令用于杀死挂起且无响应的进程。
语法：`kill [options] [pids][commands]`

# 如何杀死挂起的进程？

首先，使用 `ps` 命令识别你想要杀死的特定进程的进程 ID（`PID`）。一旦知道了 `PID`，将其作为参数传递给 `kill` 命令。下面的示例显示了如何杀死挂起的 `apache httpd` 进程。请注意，通常你应该使用 `"apachectl stop"` 来停止 `apache`。

```
# ps aux | grep httpd

USER %CPU %MEM VSZ RSS TTY START TIME COMMAND

apache 31186 0.016 23736 17556 ?S Jul26 0:40 /usr/local/apache2/bin/httpd

apache 31187 0.013 20640 14444 ?S Jul26 0:37 /usr/local/apache2/bin/httpd

# kill 31186 31187
```

```
# kill -9 31186 31187
```

另一种轻松杀死多个进程的方法是在 `.bash_profile` 中添加以下两个函数：

```bash
function psgrep ()
  ps aux | grep "$1" | grep -v 'grep'
}

function pstern ()
  [ $# -eq 0 ] && echo "usage: $0" && return 0
  local pid
  pid=$(ps ax | grep "$1" | grep -v grep | awk '{ print $1 }')
  echo -e "terminating '$1' (processes):\n$pid"
  kill -SIGTERM $pid
}
```

现在执行以下操作识别并杀死所有 `httpd` 进程。

| USER COMMAND |
| --- --- |
| apache | Jul26 |
| apache | Jul26 |
| PID %CPU %MEM |
| 31186 | 0:40 |
| 31187 | 0:37 |

```
| PID %CPU %MEM VSZ RSS TTY START TIME COMMAND |
| --- --- --- --- --- --- --- |
| 31186 0.016 23736 17556 ?S Jul26 0:40 /usr/local/apache2/bin/httpd |
| 31187 0.013 20640 14444 ?S Jul26 0:37 /usr/local/apache2/bin/httpd |
```
