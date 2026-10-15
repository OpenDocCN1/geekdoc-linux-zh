
`0,0, 1)`

`0,0, 2)`

在所示的两个示例中，`CD/DVD`驱动器仅读取而不能刻录`CD`（`DVD-ROM`和`CD-ROM`）。第二个示例显示了一个可以刻录`CD`或`DVD`的驱动器（`DVDWR`）。插入您想要刻录的介质。由于您的驱动器与介质匹配，这里是一些刻录`CD`或`DVD`介质的`cdrecord`命令：

```
# cdrecord --blank-fast ...
# cdrecord -v home.iso ...
# cdrecord -v e speed-d2 home.iso ...
# cdrecord -pad home.iso ...
# cdrecord -eject/dev/cdrom.iso...
# cdrecord dev0,2,home.iso
```

`cdrecord`命令可以刻录多会话`CD/DVD`。以下是一个示例：

```
# cdrecord --multi home.iso
# cdrecord -mininfo
  /dev/cdrom of unknown partitions \
  0/93041
# mkisofs -J -R o new.iso \
  -C 0,93041 /home/chris/more
# cdrecord new.iso
```

您可以使用多次`-multi`刻录直到`CD`填满。对于最后一次刻录，不要使用`-multi`，这样`CD`将

## 使用 `growisofs` 制作并刻录 `DVD`

使用`growisofs`命令，您可以将收集文件到`ISO`镜像（`mkisofs`）以及将该镜像刻录到`DVD`（`cdrecord`）这两个阶段结合起来。通过简化步骤，`growisofs`命令还具有默认保持会话开启直到您将其关闭的优势，因此您不需要对多次刻录会话进行任何特殊操作。

以下是多会话的`growisofs`命令示例：

```
# growisofs -Z /dev/cd0 -R -J /home/chris    制作并刻录到 DVD
# growisofs -Z /dev/cd0 -R -J /home/francois  添加并刻录
# growisofs -M /dev/cd0/zero               关闭刻录
```

如果您想在创建`ISO`镜像时添加选项，只需将`mkisofs`添加到命令中。（例如，参见上述示例中如何添加`-R`和`-J`选项。）

如果您想使用`growisofs`刻录`DVD`镜像，可以使用`-dvd-compat`选项。这里是一个示例：

```
# growisofs -dvd-compat -Z /dev/cd0-image.iso 将 ISO 镜像刻录到 DVD
```

在某些多会话`DVD`刻录过程中，`-dvd-compat`选项可以提高与不同`DVD`驱动器的兼容性。

## 总结

`BSD`及其之前的`UNIX`系统通过组合处理离散功能的命令来处理数据备份。您的关键数据备份仍然可以通过这种方式进行。事实上，您使用的许多工具将比以前任何时候都更安全、高效。

磁带归档实用（`tar`命令）已经远远超出了其制作数据文件磁带备份的原始工作。由于几乎每个`BSD`、`Linux`和`UNIX`系统都使用`tar`，它已成为软件包打包和数据压缩归档的标准工具。这些归档随后可以通过多种方式传输和存储。

要通过网络将数据传回其他机器，您可以使用`OpenSSH`工具的执行功能（如`ssh`）。您还可以使用一个名为`rsync`的优秀工具。通过`rsync`，您可以通过只备份已更改的文件（或文件的部分）来节省资源。

廉价的`CD`和`DVD`让这些介质在个人和小办公室备份中流行起来。`mkisofs`命令可以创建`ISO9660`格式的备份数据文件，可以在多种系统（`BSD`、`Linux`、`Windows`或`Mac`）上恢复。在`mkisofs`命令创建`ISO`镜像后，可以使用`cdrecord`和`growisofs`命令将镜像刻录到`CD`或`DVD`。

## 查看和管理运行进程

当一个可执行程序启动时，它作为一个受您的`BSD`系统进程表管理的进程在运行。每个`BSD`系统都提供了查看和更改系统上运行进程所需的所有工具。

`ps`和`top`命令是查看运行中进程信息的绝佳工具。`ps`和`top`实际上有几十个选项可以帮助您按照想要的方式处理信息。`pgrep`命令可以进一步帮助找到您所需的进程。

有诸如`nice`和`renice`等命令用于提高或降低进程的处理器优先级。您可以将进程移动到后台运行（`bg`命令）或返回前台（`fg`命令）。

向进程发送信号是改变其行为或彻底杀死它的方法。通过使用`kill`和`killall`命令，您可以分别通过`PID`或名称发送信号。您还可以向进程发送其他信号来执行操作，如重新读取配置文件或继续已停止的进程。要在调度时间运行命令，可以使用`cron`。要重复运行命令，可以使用`batch`。

### 使用 `ps` 和 `top` 查看活动进程

要查看系统当前运行哪些进程，大多数人使用`ps`和`top`。`ps`命令提供了当前运行进程的快照。`top`命令提供了按`CPU`、`I/O`等排序的持续更新列表。要看到所有输出，您需要在`/etc/fstab`中添加以下行：

```
proc
```

然后输入以下命令（如`Linux`）：

```
mount /proc
```

每个系统（如`UNIX`）都包含了`ps`命令。多年来出现了不同的版本，提供了不同的选项（例如，允许在某些情况下删除）。`ps`在`FreeBSD`、`OpenBSD`和大多数其他系统中工作。这里是当前用户的进程示例：

| PID | STAT | TIME | COMMAND |
| --- | --- | --- | --- |
| 1132 | ? | 00:06 | `sshd@tty0` |
| 810 | I+ | 00:09 | `-sh (sh)` |
| 1117 | I+ | 00:05 | `-sh (sh)` |
| 1133 | Ss | 00:03 | `-sh (sh)` |
| 1211 | R+ | 00:00 | |

| USER | PID | %CPU | %MEM | VZ | STAT | TIME | COMMAND |
| --- | --- | --- | --- | --- | --- | --- | --- |
| `chris` | 1132 | 0.0 | 0.0 | 6352 | 3312 | S | 4:52PM | 00:03 |
| `chris` | 810 | 0.0 | 0.6 | 1752 | 1400 | I+ | 3:00PM | 00:09 |
| `chris` | 1117 | 0.0 | 0.6 | 1752 | 1396 | I+ | 4:45PM | 00:05 |
| `chris` | 1133 | 0.0 | 0.6 | 1756 | 1396 | S | 4:52PM | 00:03 |
| `chris` | 1204 | 0.0 | 0.4 | 1460 | 1036 | R+ | 5:07PM | 00:00 |

`$ ps -fu chris`显示`chris`的运行进程（带有`PID`）

| PID | STAT | TIME | COMMAND |
| --- | --- | --- | --- |
| 1132 | ? | 00:06 | `sshd: chris:ttyp0 (sshd)` |
| 810 | I+ | 00:09 | `-sh (sh)` |
| 1117 | I+ | 00:05 | `-sh (sh)` |
| 1133 | Ss | 00:03 | `-sh (sh)` |
| 1211 | R+ | 00:00 | |

`$ ps -ps vu`显示所有运行进程（带有`SL`和`RE`）

| PID | STAT | TIME | RE | PAGE | VZ | RSS | MEM | LIMSI | %CPU | %MEM | COMMAND |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1132 | S | 00:00:16 | 0 | 127 | 6252 | 3312 | 168 | 0.0 | 1.3 | `sshd: chris` |
| 810 | I+ | 00:00:29 | 0 | 127 | 1756 | 1400 | 100 | 0.0 | 0.6 | `-sh (sh)` |
| 1133 | Ss | 00:00:08 | 0 | 127 | 1756 | 1400 | 100 | 0.0 | 0.6 | `-sh (sh)` |
| 1244 | I+ | 00:00:47 | 0 | 70 | 1752 | 1392 | 100 | 0.0 | 0.6 | `-sh (sh)` |
| 1264 | R+ | 00:00:01 | 0 | 0 | 1460 | 1044 | 24 | 0.4 | `ps -vu` |

`$ ps -aux`显示所有运行进程，长`BSD`样式，显示每个运行进程，长`BSD`样式，无限制

`$ ps -auwx`显示所有运行进程，长`BSD`样式，宽格式，显示每个运行进程，长`BSD`样式，无限制

# 第 9 章：检查和管理运行进程

如果你想查看`ps`条目的完整输出，之前的两个命令将非常有用。如果输出超过了你的列宽，它将换行而不是截断。

某些进程会启动其他进程。例如，`Web`服务器（`http`守护进程）会产生多个`httpd`守护进程来等待来自服务器的请求。你可以使用`pstree`命令查看进程层次结构（树状视图）（以`root`身份运行，输入`pkg_add -r pstree`进行安装）：

```
$ pstree 以树状格式按字母顺序显示进程
+= 00000 root [swapper]
|-- 00001 root /sbin/init
|   |-- 01121 root adjkertnz -i
||-- 00739 root /usr/bin/sshd
| \+ 01129 root sshd: chris [priv] (sshd)
| |\- 01132 chris sshd: chris@ttyp0 (sshd)
|   |\- 01133 chris -sh (sh)
|     \+ 01999 chris pstree
|       \-+ 02000 chris ps -c -awxo user.pid,ppid,pgid,command
|       \-+ 02001 chris ps -awxo user.pid,ppid,pgid,command
```

“树”示例仅说明了显示进程层次结构的另一种方式。`ssh`进程显示了一个正在运行的、通过网络登录的用户安全守护进程（Secure Daemon），导致了一个`bash` shell（以及最终的`ps`命令）。

如果你更倾向于`ps`输出的个性化视图，可以使用`-o`选项精确地选择要显示哪些数据列。表 9-1 显示了可用的列输出以及添加到`-o`的选项，以便用`ps`打印每一列。

### 表 9-1：选择和查看 `ps` 列输出

| 选项 | 列标题 | 描述 |
|---|---|---|
| `%cpu` | `%CPU` | `CPU` 使用百分比 |
| `%mem` | `%MEM` | 内存使用百分比 |
| `acflag` | `ACFLAG` | 计费标志 |
| `args` | `COMMAND` | 命令和参数 |
| `comm` | `COMMAND` | 仅命令 |
| `command` | `COMMAND` | 命令和参数（与 `args` 相同） |
| `cpu` | `CPU` | 短期 `CPU` 使用因子（用于调度） |
| `etime` | `ELAPSED` | 运行已时间 |
| `flags` | `F` | 进程标志，十六进制（与 `f` 相同） |
| `inblk` | `INBLK` | 总读取块数（与 `inblock` 相同） |
| `jid` | `JID` | Jail ID |
| `jobc` | `JOBC` | 作业控制计数 |
| `ktrace` | `KTRACE` | 跟踪标志 |
| `label` | `LABEL` | MAC 标签 |
| `lim` | `LIM` | 内存使用限制 |
| `lockname` | `LOCK` | 当前阻塞的锁（作为符号名称） |
| `logname` | `LOGIN` | 启动会话的用户登录 |
| `Istart` | `STARTED` | 开始时间 |
| `majflt` | `MAJFLT` | 总页异常 |
| `minflt` | `MINFLT` | 总页请求 |
| `msgrcv` | `MSGRCV` | 总接收消息数（管道/socket 读取） |
| `msgsnd` | `MSGSND` | 总发送消息数（管道/socket 写入） |
| `mwchan` | `MWCHAN` | 当前阻塞的等待通道或锁 |
| `nice` | `NI` | Nice 值（与 `ni` 相同） |
| `nivscw` | `NIVCSW` | 总非自愿上下文切换 |
| `nsigs` | `NSIGS` | 总处理信号（与 `nssignals` 相同） |
| `nswap` | `NSWAP` | 总交换换出次数 |
| `nvcsw` | `NVCSW` | 总自愿上下文切换 |
| `nwchan` | `NWCHAN` | 等待通道（作为地址） |
| `oublk` | `OUBLK` | 总写入块数（与 `oublock` 相同） |
| `paddr` | `PADDR` | 交换地址 |
| `pagein` | `PAGEIN` | 页（与 `majflt` 相同） |
| `pgid` | `PGID` | 进程组号 |
| `pid` | `PID` | 进程 ID |
| `ppid` | `PPID` | 父进程 ID |
| `pri` | `PRI` | 调度优先级 |
| `re` | `RE` | 核心驻留时间（秒）（127 表示无穷） |
| `rgid` | `RGID` | 真实组 ID |
| `rgroup` | `RGROUP` | 组名（与真实组 ID 关联） |
| `rss` | `RSS` | 驻留集大小 |
| `rtprio` | `RTPRIO` | 实时优先级（101 表示不是实时进程） |
| `ruid` | `RUID` | 用户 ID |
| `ruser` | `RUSER` | 用户（与真实用户 ID 关联） |
| `sid` | `SID` | 会话 ID |
| `sig` | `PENDING` | 等待信号（与 `pending` 相同） |
| `sigcatch` | `CAUGHT` | 已捕获的信号（与 `caught` 相同） |
| `signignore` | `IGNORED` | 忽略的信号（与 `ignored` 相同） |
| `sigmask` | `BLOCKED` | 阻塞的信号（与 `blocked` 相同） |
| `sl` | `SL` | 睡眠时间（秒）（127 表示无穷） |
| `start` | `STARTED` | 开始时间 |
| `state` | `STAT` | 符号进程状态（与 `stat` 相同） |
| `svgid` | `SVGID` | 从集合中保存的 gid |
| `svuid` | `SVUID` | 从集合中保存的 UID |
| `tdev` | `TDEV` | 控制终端设备 |
| `time` | `TIME` | 累计 `CPU` 时间，系统（与 `cputime` 相同） |
| `tsid` | `TSID` | 控制会话 ID |
| `tsize` | `TSIZ` | 文本大小（字节） |
| `tt` | `TT` | 控制终端名称，缩写 |
| `tty` | `TTY` | 控制终端全名 |
| `uprocp` | `UPROCP` | 进程指针 |
| `ucomm` | `UCOMM` | 用于计数的名称 |
| `uid` | `UID` | 有效用户 ID |
| `upr` | `UPR` | 调度优先级（与 `uspr` 相同） |
| `user` | `USER` | 用户名（来自用户） |
| `vsz` | `VSZ` | 虚拟大小（字节） |
| `wchan` | `WCHAN` | 等待通道（符号名称） |
| `xstat` | `XSTAT` | 退出或停止状态（僵尸进程） |

注意某些值如果名称太长将以数字形式打印。要查看数值，请使用`ps -L`选项。

使用逗号分隔的列表，例如`pid,mem,comm`，可以产生自定义输出。以下是运行进程的一些自定义视图示例：

```
$ ps -ko pid,user,comm 显示进程 ID，内存，等。
PID USER %MEM TSIZ VSZ
1129 chris 1.38 6252

$ ps -ko pid,user,start,time,%cpu 显示 PID，启动时间，时间，等。
PID USER STARTED %CPU
1129 chris 4:52 0.08 chris@ttyp0
```

```
$ ps -xo puser,nice,cutime,args 显示用户，nice，时间，参数。
PPID NI TIME
1129 chris 0 00:00:84 chris:ttyp0

$ ps -xo puser,stat,tty,sid,etime 显示 PID，用户，终端，等。
PPID USER STAT ELAPSED
1129 chris S ?06:39:23 chris:ttyp0
```

以下是`ps`命令的几个示例：

```
$ ps -aux -r | less 按 CPU 使用率排序
USER %CPU %MEM VSS RS TT TIME
root 10.7 4.0 8 ? RL 3:30PM 503:12.85 [idle]
root 2551 7.8 1384 916 V3 R 11:55PM 02:02.50 find
root 4 1.0 8 ? DL 3:30PM 00:08.73 [g_down]

$ ps -l tty 按内存使用率排序
USER %CPU %MEM VSS RS TT STAT
root 1307 0.0 1.2 4928 3004 I 5:31PM 00:05.58 -csh (csh)
```
