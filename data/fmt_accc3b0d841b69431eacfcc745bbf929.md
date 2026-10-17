
`id3:initdefault:`

将数字 `(3)` 替换为你想要系统启动的运行级别对应的值。

大多数发行版会自动将其设置为多用户文本模式，尽管最近的发行版在安装时让你选择运行级别。

你可能希望进入多用户模式或 X。其他级别不提供完整的功能。在某些情况下，它们可能不提供功能或损坏设备。例如，将重启设置为默认运行级别会导致机器无限重启。

## 进入单用户模式

可能需要进入单用户模式来修复系统损坏或在程序启动之前修改某些参数。这可以通过启动时将 `single` 关键字传递给 `LILO` 来实现。例如，如果你想进入内核镜像 `linux`，你输入以下内容：

```
LILO: linux single
```

### 管理任务

这将在运行级别 `1` 下停止 `init` 进程。根据你的系统，在访问系统之前可能需要输入超级用户（Superuser）密码。

你可以通过注销单用户会话（Single User session），选择在默认运行级别下继续。

## 动态更改运行级别

你可以随时通过发布 `init` 命令后跟你想要的任何运行级别来更改运行级别。例如，如果你想重启系统，可以输入以下内容：

```
init 6
```

## `/etc/rc.d/` 目录结构 (Red Hat)

如果你查看 `init-scripts` 目录，列表内容应该类似于所示：

```
# ls -Fa /etc/rc.d/

./  *  rc.sysinit  rc2.d/  rc5.d/

../  rc.firewall  rc0.d/  rc3.d/  rc6.d/

init.d/  rc.local*  rc1.d/  rc4.d/
```

如你所见，每个运行级别都有一个对应的名为 `rc<number>` 的脚本目录。查看其中一个目录：

```
# ls -Fa /etc/rc.d/rc3.d/

../  K65portmap  S30syslog  S65dhcpd  S91smb

K65nfsfsd  S44atd  S75keytable  S95httppd

K20usersd  K96ncmial  S40crond  S80qmail  S99local

K30mculeserv  S01kernel  S89init  S85ppgm

K40snmpd  S10network  S55named  S90squid

K5routed  S20random  S68local  S98hostname
```

在启动过程中，随着 `init` 经过各个运行级别，它将访问每个对应的目录并运行所有以 `S` 开头的脚本。由于它是按字母顺序读取文件名，数字越小的脚本优先级越高。例如，`S01kernel` 将先运行，而 `S95httppd` 几乎最后运行。

当系统关机时，`init` 会反向执行该过程并调用以 `K` 开头的文件，赋予它们停止命令。

你可能已经注意到，所有这些脚本实际上都是符号链接——`rc<number>.` 目录通常不包含实际文件。真实文件都位于 `/etc/rc.d/init.d`：

```
# ls -Fa /etc/rc.d/init.d/

../  mcserv*  random*  syslog*

../  halt*  named*  routed*  vmware*

../  atd*  httpd*  network*  rusersd*

crond*  inet*  nfsfs*  single*

debug  keytable*  pcmcia*  smb*

dhcp*  killall*  portmap*  snmpd*

functions*  lpd*  qmail*  squid*
```

`init` 进程通过从一个或多个 `rc <number>.d` 目录符号链接到这些文件中的任何一个来控制，并带有相应的 `<priority>` 进程或 `<number>` 进程。由于这些是 shell 脚本，`init` 可以为它们提供命令行参数，这样同一个脚本就可以用于启动、停止或重启一个进程。

## 手动控制进程

你可能想手动启动、停止或重启这些进程中的任何一个。你要做的只是使用相应的命令行参数运行相应的 init 脚本。例如，要停止你的 `httpd` 进程，请输入以下内容：

```
# /etc/rc.d/init.d/httpd stop
```

再次启动你的 `httpd` 进程，请输入以下内容：

```
# /etc/rc.d/init.d/httpd start
```

其他有效的命令选项可能包括 `restart`、`status` 或 `reload`，取决于你的发行版以及你试图控制的特定进程。

## 修改 init 进程

修改 `init` 进程最直接（也最复杂）的方法手动设置或删除 `/etc/rc.d/` 内的符号链接。

常见的做法是将不想运行的脚本重命名为带有点（`.~`）的名字——这不仅可以防止 `init` 找到它们，还会导致它们在普通命令中隐藏。另一种常见的做法是将文件重命名为小写。然而，这些方法对维护并不友好。

## 使用 chconfig 工具 (Red Hat)

`chconfig` 工具可用于显示、激活或停用 `init` 进程。它实际上会操作 `/etc/rc.d/` 目录树中的符号链接。

你可以通过发布以下命令获取系统所有 `init` 进程列表（实际上是位于 `/etc/rc.d/init` 且包含关于它们认为应该处于哪些运行级别的信息的脚本）：

```
# chconfig --list
```

这将产生一个很长的服务列表，以及关于它们激活的运行时间的信息。要检查特定脚本，请在命令行中使用其名称：

```
# chconfig --list httpd

httpd 0:off 1:off 2:off 3:on 4:on 5:on 6:off
```

如你所见，`httpd` 在运行级别 `3`、`4` 和 `5` 中是激活的。

如果你想禁用脚本，输入以下内容：

```
# chconfig off httpd

# chconfig --list httpd

httpd 0:off 1:off 2:off 3:off 4:off 5:off 6:off
```

该脚本现在在每个运行级别上都处于活动状态。

要重新开启脚本，输入以下内容：

```
# chconfig httpd
```

## 关机

`shutdown` 命令将等待直到你指定的关机时间。它将通知系统上的所有人（你也可以指定）。你可以告诉它在之后留出一定的时间，以便人们注销系统。然后它将调用 `init` 来执行脏工作。

`shutdown` 命令的语法如下：

```
# shutdown [-t delay] [-r][-h][-k][-c] time message
```

`-t` 选项的参数是警告与实际关机之间的延迟（秒）。

你可以使用 `-r` 重启或 `-h` 停止。`-k` 选项将使 `shutdown` 发送消息。`-c` 选项将取消挂起的关机。

`time` 参数指定关机发生的时间。可以使用 24 小时格式（`hh:mm`）或从现在起的几分钟数。如果你使用 `now`，关机将立即发生。

`message` 参数将在关机前显示给所有登录用户。它可以用于解释系统为什么要关机。

你应该能看到 `fdisk` 交互模式提示符。在此模式下，你通常输入单个字母命令来创建、删除和列出分区。你应该尝试的第一个命令是 `p` 命令，如下所示，它将打印当前分区表：

```
Command (m for help): p
```

```
Disk /dev/hdd: 15 heads, 63 sectors, 8912 cylinders
Units = cylinders of 945 * 512 bytes

| Device Boot | Start | End | Blocks | Id | System |
|---|---|---|---|---|---|
| /dev/hdd1 | * | 1 | 8912 | 4210888+ | b | FAT32 |
```

```
Command (m for help):
```

如你所见，此驱动器只有一个分区 (`/dev/hdd1`)。它跨越整个硬盘，大小约为 4.3GB，格式为 FAT32 分区。

由于你想将此驱动器用于 Linux，请继续使用 `d` 命令删除此分区，如下所示：

```
Command (m for help): d
Partition number (1-4): 1
```

```
Command (m for help): p
```

```
Disk /dev/hdd: 15 heads, 63 sectors, 8912 cylinders
Units = cylinders of 945 * 512 bytes

| Device Boot | Start | End | Blocks | Id | System |
|---|---|---|---|---|---|
```

```
Command (m for help):
```

现在分区表已经空了，你可以继续添加 Linux 分区。

## 主分区与扩展分区

在添加分区之前，你必须决定想要什么种类型的分区。

Linux 支持多多四个主（实际）分区。如果你不需要比这更多数量的分区，你可以将所有分区都创建为该类型。

如果你需要更多的分区，可以将其中一个分区创建为扩展分区。这种分区类型可以包含许多逻辑卷。这些逻辑卷的作用类似于普通分区，但不能用于启动。

注意，主分区的编号为 1 到 4。逻辑卷分区的编号从 5 开始。

## 添加分区

现在你将向驱动器添加三个分区。你将添加一个 128MB 的 Linux Swap（交换）分区和一个 3GB 的 Linux 数据（或 Linux 原生）分区。剩余的 911MB 将分配为扩展分区，并在其中你创建两个逻辑卷。它们将是大小约为 455MB 的 FAT32 分区。

整个过程你使用了两个 `fdisk` 命令。首先，`n` 命令创建新分区。它会提示你分区类型和编号。它还会提示你起始磁道和结束磁道。不用担心缺少正确的磁道或计算每个磁道的字节数；系统会提供默认起始值，且结束参数可以用千字节为单位给出。

第二个使用的命令是 `t` 命令，用于修改分区。它会提示你分区编号，并询问你想更改为哪种类型。它还可以显示已知分区类型的列表。

另一个实用的命令是 `l` 命令，它将向你显示已知分区类型的列表。你可以提前咨询它以节省时间。例如，如果你将使用分区类型 `b2` (Linux Swap) 和 `b` (FAT32)。在后续过程之前，这里显示了使用 `l` 命令：

```
Command (m for help): l
```

```
| Empty | a OS/2 Boot Manag | 65 Novell Novare | a6 OpenBSD |
| 1 DOS 12-bit FAT | b FAT32 | 75 PC/IX | a7 NEXTSTEP |
| 2 XENIS root | c FAT32 (LB) | 80 Old MINIX | b7 BSDI fs |
| 3 XENIS usr | e FAT16 (LB) | 81 Linux/MINIX | b8 BSDI swap |
| 4 DOS 16-bit <32M | f Win95 Extended | 82 Linux Swap | c7 Syrinx |
| 5 Extended | g Venice 82826 | 83 Linux native | d CP/M |
| 6 DOS 16-bit >=32 | 51 Novell | 85 Linux extended | e1 DOS access |
| 7 OS/2 HFS | 52 Microport | 93 Amoeba | e3 DOS/R |
| 8 AIX | g GNUX | 94 Amoeba BBT | f2 OS secondary |
| 9 AIX boot | 64 Novell Alternate | as BSD/388 | ff BBT |
```

```
Command (m for help): n
```

```
Command action

e extended

p  primary partition (1-4)

p

Partition number (1-4): 1

First cylinder: 1

Last cylinder or +size or +sizeM +sizeK +128M
```

```
Command (m for help): p
```

```
Command action

e extended

p  primary partition (1-4)

p

Partition number (1-4): 2

First cylinder (279-8912): 279

Last cylinder or +size or +sizeM +sizeK ({279-8912}): +372M
```

```
Command (m for help): n
Command action
e extended
p primary partition (1-4)
e
Partition number (1-4): 3
First cylinder (6937-8912): 6937
Last cylinder or +size or +sizeM +sizeK ([6937]-8912): 8912
```

```
Command (m for help): n
Command action
1 logical (5 or over)
p primary partition (1-4)
1
First cylinder (6937-8912): 6937
Last cylinder or +size or +sizeM +sizeK ([6937]-8912): 7924
```

```
Command (m for help): n
1 logical (5 or over)
p primary partition (1-4)
1
First cylinder (7925-8912): 7925
Last cylinder or +size or +sizeM +sizeK ([7925]-8912): 8912
```

```
Command (m for help): t
Partition number (1-6): 1
Hex code (type L to list codes): 82
Changed system of partition 1 to 82 (Linux swap)
```

```
Command (m for help): t
Partition number (1-6): 5
Hex code (type L to list codes): b
Changed system of partition 5 to b (Win95 FAT32)
```

```
Command (m for help): t
Partition number (1-6): 6
Hex code (type L to list codes): b
Changed system of partition 6 to b (Win95 FAT32)
```

```
Command (m for help): p
```

```
Disk /dev/hdd: 15 heads, 63 sectors, 8912 cylinders
Units = cylinders of 945 * 512 bytes

| Device Boot | Start | End | Blocks | Id | System |
|---|---|---|---|---|---|
| /dev/hdd1 | * | 1 | 278 | 13123+ | 82 | Linux swap |
| /dev/hdd2 | | 279 | 6936 | 314505 | 83 | Linux native |
| /dev/hdd3 | | 6937 | 8912 | 93360 | 5 | Extended |
| /dev/hdd5 | | 6937 | 7924 | 466798+ | b | Win95 FAT32 |
| /dev/hdd6 | | 7925 | 8912 | 466798+ | b | Win95 FAT32 |
```

```
Command (m for help):
```

## 管理任务

创建分区的工作就此结束。唯一要做的事是将分区表写入磁盘。你使用 `w` 命令执行此操作。`disk` 程序会将分区表写入驱动器，然后进行几次系统调用让 Linux 识别分区表。它还会发出关于创建或修改分区的警告。对于旧版本的 `disk` 和 Linux 内核，建议重启机器以确保更改生效。如果是这种情况，旧版本的 `disk` 通常会打印消息。如果你想验证更改已保存，可以运行带 `l` 参数的 `disk`；这等于在 `disk` 中运行 `p` 命令。

## 格式化分区

虽然有很多 Linux 工具，但我们专注于 Linux 原生类型：交换空间和第二个文件系统 (`ext2`)。

### 格式化交换文件系统

要格式交换分区，运行 `mkswap` 程序并指定分区。例如，要格式化你之前创建的分区，输入：

```
# mkswap /dev/hdd1
```

如果你希望 `mkswap` 在格式化时检查坏块，使用 `-c` 命令行开关，如下所示：

```
# mkswap -c /dev/hdd1
```

自然，这需要更长的时间。

### 格式化 ext2 文件系统

`ext2` 文件系统是 Linux 的原生文件系统。你的数据通常驻留在这类文件系统上。你使用 `mk2fs` 命令来格式化此类分区。

与 `mkswap` 类似，唯一需要的参数是你想要格式化的分区名称。如果你想检查坏块，也可以使用 `-c` 命令开关。如果你不确定硬盘是否处于完美状态，强烈建议使用它。

```
# mk2fs -c /dev/hdd2
```
