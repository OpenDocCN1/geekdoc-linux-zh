
在此示例中，`tr` 命令用于文件名字段列表，以重命名该列表中的任何文件，使文件名中包含的任何空格都被转换为下划线：

```
for file in * ; do
    d=`echo $file | tr [:blank:] [_]`
    [ "$file" != "$d" ] || mv "$file" "$d"
done
```

## 流编辑器（sed）

`sed` 命令是一个简单的可脚本化编辑器，因此只能执行简单的编辑，例如删除包含匹配特定模式的文本的行、用另一种字符模式替换一种字符模式，以及其他简单编辑。要更好地了解 `sed` 脚本的工作原理，没有什么能替代在线文档，但以下是一些常见用法的示例。

你可以使用 `sed` 命令基本上做我们之前用 `grep` 示例所做的事情：在 `/etc/passwd` 文件中搜索单词 `home`。这里 `sed` 命令搜索整个 `/etc/passwd` 文件，查找单词 `home`，并打印包含单词 `home` 的任何行。

```
`sed -n -e '/home/p' /etc/passwd`
```

在此示例中，`sed` 搜索文件 `somefile.txt` 并将字符串 `Mac` 的每个实例替换为 `Linux`。输出随后发送到 `fixed_file.txt` 文件。

```
`sed -e 's/Mac/Linux/' somefile.txt > fixed_file.txt`
```

你也可以使用管道获得相同的结果：

```
`cat somefile.txt | sed -e 's/Mac/Linux/' > fixed_file.txt`
```

通过搜索模式并将其替换为空模式，你可以删除原始模式。此示例搜索 `somefile.txt` 文件的内容，并将每行末尾的多余空白（`s/ *$//`）替换为空（`''`）。结果输出到 `fixed_file.txt` 文件。

```
`cat somefile.txt | sed -e 's/ *$//' > fixed_file.txt`
```

## 尝试一些简单的 shell 脚本

有时最简单的脚本可能最有用。如果你反复输入相同的命令序列，那么将这些命令（一次！）存储在文件中是有意义的。以下是几个简单但有用的 shell 脚本。

### 一个简单的电话列表

这个想法一代又一代地从老 UNIX 黑客那里传下来。它其实相当简单，但它运用了刚刚介绍的几个概念。

```
#!/bin/bash
# (@)/ph
# A very simple telephone list
# Type "ph new name number" to add to the list, or
# just type "ph name" to get a phone number
PHONELIST=~/.phonelist.txt
# If no command line parameters ($#), there
# is a problem, so ask what they're talking about.
if [ $# -lt 1 ] ; then
    echo "Whose phone number did you want?"
    exit 1
fi
# Did you want to add a new phone number?
if [ "$1" = "new" ] ; then
    shift
    echo $* >> $PHONELIST
    echo $* added to database
    exit 0
fi
# Nope. But does the file have anything in it yet?
# This might be our first time using it, after all.
if [ ! -s $PHONELIST ] ; then
    echo "No names in the phone list yet!"
    exit 1
else
    grep -q "$*" $PHONELIST    # Quietly search the file
    if [ $? -ne 0 ] ; then
        echo "Sorry, that name was not found in the phone list"
        exit 1
    else
        grep "$*" $PHONELIST
    fi
fi
exit 0
```

### 一个简单的备份脚本

由于没有什么能永远正常工作，而且会发生错误，备份在处理计算机数据时只是生活的一部分。这个简单脚本将备份 Red Hat Linux 系统上所有用户的家目录中的所有数据。

```
#!/bin/bash
# (@)/my_backup
# A very simple backup script
#
TAPE=/dev/rft0

# Rewind the tape device $TAPE
mt $TAPE rew
# Get a list of home directories
HOMES=`grep /home /etc/passwd | cut -f6 -d':'`
# Backup the data in those directories
tar cvf $TAPE $HOMES
# Rewind and eject the tape.
mt $TAPE rewoffl
```

> **交叉引用：** 请参阅第 13 章，了解有关备份和恢复文件的详细信息。

## 系统初始化

当你打开计算机时，在 Red Hat Linux 启动之前就会发生很多事情。以下是每次启动计算机以运行 Red Hat Linux 时发生的基本步骤：

- 1. **启动硬件** — 根据计算机只读内存（称为 BIOS）中的信息，计算机检查并启动硬件。其中一些信息告诉计算机检查哪些设备（软盘、CD、硬盘等）以找到可启动的操作系统。
- 2. **启动引导加载程序** — 通常，BIOS 检查主硬盘上的主引导记录以查看下一步加载什么。安装了 Red Hat Linux 后，将启动 GRUB 引导加载程序，允许你选择启动 Red Hat Linux 或其他已安装的操作系统。
- 3. **启动内核** — 假设你选择启动 Red Hat Linux，则会加载 Linux 内核。该内核挂载基本文件系统并将控制权转移到 init 进程。本节的其余部分描述了内核将系统启动控制权移交给 init 进程后发生的情况。

### 启动 init

在引导过程中，从内核阶段（加载内核、探测设备和加载驱动程序）到 init 的转换由以下行指示：

```
INIT: version 2.84 booting
           Welcome to Red Hat Linux
```

init 程序是 SysVinit RPM 包的一部分，现在处于控制之下。被称为 ``the father of all processes,'' 的输出从 ps 始终将 init 列为 PID（进程标识符）1。其操作由 /etc/inittab 文件指导，该文件在下面重现。

### inittab 文件

下面显示了随 Red Hat Linux 提供的 /etc/inittab 文件的内容：

```
#
# inittab    This file describes how the INIT process should set up
#
#            the system in a certain run level.
#

.
.
.

id:3:initdefault:

# System initialization.

si::sysinit:/etc/rc.d/rc.sysinit

10:0:wait:/etc/rc.d/rc 0
11:1:wait:/etc/rc.d/rc 1
12:2:wait:/etc/rc.d/rc 2
13:3:wait:/etc/rc.d/rc 3
14:4:wait:/etc/rc.d/rc 4
15:5:wait:/etc/rc.d/rc 5
16:6:wait:/etc/rc.d/rc 6


# Trap CTRL-ALT-DELETE
ca::ctrlaltdel:/sbin/shutdown -t3 -r now

# When our UPS tells us power has failed, assume we have a few minutes
# of power left. Schedule a shutdown for 2 minutes from now.
# This does, of course, assume you have powered installed and your
# UPS connected and working correctly.
pf::powerfail:/sbin/shutdown -f -h +2 "Power Failure; System Shutting Down"

# If power was restored before the shutdown kicked in, cancel it.
pr:12345:powerokwait:/sbin/shutdown -c "Power Restored; Shutdown Cancelled"


# Run gettys in standard runlevels
1:2345:respawn:/sbin/mingetty tty1
2:2345:respawn:/sbin/mingetty tty2
3:2345:respawn:/sbin/mingetty tty3
4:2345:respawn:/sbin/mingetty tty4
5:2345:respawn:/sbin/mingetty tty5
6:2345:respawn:/sbin/mingetty tty6


# Run xdm in runlevel 5
# xdm is now a separate service
x:5:respawn:/etc/X11/prefdm -nodaemon
```

### inittab 文件的格式

纯文本 inittab 文件由几个以冒号分隔的字段组成，格式为：

```
`id:runlevels:action:command`
```

id 字段是一个唯一的标识符，长度为一到四个字母数字字符，表示系统启动期间要采取的特定操作。runlevels 字段包含命令将被运行的运行级别列表。常见的运行级别为 0、1、2、3、4、5 和 6（s 和 S 表示单用户模式，等同于 1）。运行级别 7、8 和 9 也可以用作与按需操作关联的特殊运行级别（a、b 和 c，等同于 A、B 和 C）。下一个字段表示 init 要采取的操作类型（有效操作及其结果列在表 12-3 中），最后一个字段是要执行的实际命令。

### 表 12-3：有效的 init 操作

| 操作 | 命令的运行方式 |
|:---|:---|
| once | 进入指定运行级别时，命令执行一次。 |
| wait | 与 once 相同，但 init 会等待命令完成后再继续处理 inittab 中的其他条目。 |
| respawn | 进程被监控，如果原始进程终止，则启动新实例。 |
| powerfail | 接收到 UPS 单元相关软件发出的 SIGPWR 信号时执行命令。 |
| powerwait | 与 powerfail 相同，但 init 会等待命令完成。 |
| powerwaitok | 接收到 SIGPWR 信号且 /etc/powerstatus 文件包含单词 OK 时执行命令。这通常由 UPS 软件完成，表示已恢复正常电源水平。 |
| ondemand | 当 init 手动指示进入特殊运行级别 a、b 或 c（分别等同于 A、B 和 C）时执行命令。实际上不会发生运行级别的更改。如果原始进程终止，程序将被重新启动。 |
| sysinit | 在系统引导阶段执行命令；runlevels 字段被忽略。 |
| boot | 在系统引导阶段执行命令，在处理完所有 sysinit 条目之后；runlevels 字段被忽略。 |

