

输出数字 0123456789 的另一种方法是使用如下 until 循环：

```bash
N=0
until [ $N -eq 10 ]; do
   echo -n $N
   let N=N+1
done
```

## 一些有用的外部程序

Bash 非常强大，拥有许多内置命令，但通常它需要一些帮助才能完成真正有用的工作。你经常看到的一些最常用且有用的程序包括 `grep`、`cut`、`tr` 和 `sed`。与所有最好的 UNIX 工具一样，这些程序中的大多数都是设计为使用标准输入和标准输出的，因此你可以轻松地将它们用于管道和 Shell 脚本。

### 通用正则表达式解析器（`grep`）

这个名字听起来可能令人望而生畏，但 `grep` 只是用来在文件或文本中查找模式的一种方式。你可以把它看作是一个有用的搜索工具。熟练掌握正则表达式是一项相当大的挑战，但仅使用最简单的形式就可以完成许多有用的任务。

例如，你可以使用 `grep` 搜索 `/etc/passwd` 文件中所有包含文本 `/home` 的行，从而显示所有常规用户账户的列表，如下所示：

```bash
grep /home /etc/passwd
```

或者，你可以使用以下命令找到所有以 HO 开头的环境变量：

```bash
env | grep "HO"
```

若要查找可用于 `grep` 命令的选项列表，请输入 `man grep`。

### 删除文本行的部分（`cut`）

`cut` 命令可以从一行文本或文件中提取特定字段。它对于将系统配置文件解析为易于理解的片段非常有用。你可以指定想要使用的字段分隔符和你想要的字段，或者你可以基于字节来拆分一行。

下面的示例列出了系统中所有用户的家目录。使用之前 `grep` 命令的示例，这行命令将 `/etc/passwd` 文件中的常规用户列表通过管道传输，然后显示由冒号（`-d ':'`）分隔的第六个字段（`-f 6`）。

### 转换或删除字符（*tr*）

*tr* 命令是一个基于字符的转换器，可用于将一个字符或字符集替换为另一个，或者从一行文本中删除一个字符。

下面的示例将所有大写字母转换为小写字母，并显示结果单词“*mixed upper and lower case*”：

```bash
FOO="Mixed Upper and Lower CaSe"
echo $FOO | tr [A-Z] [a-z]
```

在下一个示例中，*tr* 命令用于一个文件名列表，以重命名该列表中的任何文件，使文件名中包含的任何空格都转换为下划线：

```bash
for file in * ; do
  d=`echo $file | tr [:blank:] [_]
  ["$file" = "$d" ] || mv "$file" "$d"
done
```

### 流编辑器（*sed*）

*sed* 命令是一个简单的可脚本化编辑器，因此它只能执行简单的编辑操作，例如删除包含匹配特定模式文本的行，用一个字符模式替换另一个，以及其他简单的编辑。要想更好地了解 *sed* 脚本是如何工作的，在线阅读文档是无可替代的，但这里有一些常见用法的示例。

你可以使用 *sed* 命令基本上做我们之前在 *grep* 示例中所做的事情：在 */etc/passwd* 文件中搜索单词 home。这里 *sed* 命令搜索整个 */etc/passwd* 文件，查找单词 home，并打印任何包含单词 home 的行。

```bash
sed -n '/home/p' /etc/passwd
```

在这个示例中，*sed* 搜索文件 *somefile.txt*，并将字符串 Mac 的每个实例替换为 Linux。然后将输出发送到 *fixed_file.txt* 文件。

```bash
sed 's/Mac/Linux/g' somefile.txt > fixed_file.txt
```

你可以使用管道获得相同的结果：

```bash
cat somefile.txt | sed 's/Mac/Linux/g' > fixed_file.txt
```

通过查找一个模式并将其替换为空模式，你就删除了原始模式。这个示例搜索 *somefile.txt* 文件的内容，并替换每行末尾（$/ \*$/）多余的空格为无（//）。结果将输出到 *fixed_file.txt* 文件。

```bash
cat somefile.txt | sed 's/\*$/ /g' > fixed_file.txt
```

## 尝试一些简单的 Shell 脚本

有时，最简单的脚本往往最有用的。如果你反复输入相同的命令序列，将这些命令（一次性）存储在一个文件中是有意义的。这里有两个简单但有用的 Shell 脚本。

### 一个简单电话列表

这个想法是从一代又一代老 UNIX 高手那里传承下来的。它真的非常简单，但它运用了刚刚介绍的几个概念。

```bash
#!/bin/bash
# @/ph
# A very simple telephone list
# Type "ph new name number" to add to the list, or
# just type "ph name" to get a phone number

PHONELIST=~/phonelist.txt

# If no command line parameters ($#), there
# is a problem, so ask what they're talking about.
if [ $# -lt 1 ] ; then
    echo "Whose phone number did you want? "
    exit 1
fi

# Did you want to add a new phone number?
if ["$1" = "new" ] ; then
    shift
    echo "$*" >> $PHONELIST
    echo "$*" added to database
    exit 0
fi

# Nope. But does the file have anything in it yet?
# This might be our first time using it, after all.
if [ ! -s $PHONELIST ] ; then
    echo "No names in the phone list yet! "
    exit 1
else
    grep -q "$*" $PHONELIST      # Quietly search the file
    if [ $? -ne 0 ] ; then      # Did we find anything?
        echo "Sorry, that name was not found in the phone list"
        exit 1
    else
        grep "$*" $PHONELIST
    fi
fi
exit 0
```

既然没有什么能永远运行无误且错误总会发生，那么当处理计算机数据时，备份只是生活的一个事实。这个简单脚本将备份 Fedora 系统上所有用户主目录中的全部数据。

```bash
#!/bin/bash
# (@)/my_backup
# A very simple backup script
#

TAPE=/dev/rft0

# Rewind the tape device $TAPE
mt $TAPE rew
# Get a list of home directories
HOMES=`grep /home /etc/passwd | cut -f6 -d: '`
# Backup the data in those directories
tar cvf $TAPE $HOMES
# Rewind and eject the tape.
mt $TAPE rewoffl
```

**交叉参考：** 有关备份和恢复文件的详细信息，请参见第 13 章。

## 系统初始化

当你打开计算机时，甚至在 Fedora 启动之前，就已经发生了很多事情。以下是每次启动计算机运行 Fedora 时发生的基本步骤：

- **1. 启动硬件**
  基于计算机只读存储器（称为 BIOS）中的信息，计算机检查并启动硬件。其中一些信息告诉计算机检查哪些设备（软盘、CD、硬盘等）以找到可启动的操作系统。

- **2. 启动引导加载程序**
  通常，BIOS 检查主硬盘上的主引导记录，以确定接下来要加载什么。安装 Fedora 后，GRUB 引导加载程序将被启动，允许你选择启动 Fedora 或另一个已安装的操作系统。

- **3. 引导内核**
  假设你选择了启动 Fedora，Linux 内核将被加载。该内核挂载基本文件系统，并将控制权传递给 init 进程。本节的其余部分描述了内核将系统启动控制权移交给 init 进程后发生的事情。

## 启动 init

在启动过程中，从内核阶段（内核加载、设备探测和驱动程序加载）到 init 的转换由以下行指示：

```
INIT: version 2.05 booting
```

Welcome to Fedora Core
Press "I" to enter interactive startup.

init 程序，作为 SysVinit RPM 包的一部分，现在处于控制地位。被称为“所有进程的之父”，ps 的输出始终将 init 列为 PID（进程标识符）1。其操作由 /etc/inittab 文件指导，该文件如下所示。

## inittab 文件

以下示例显示了随 Fedora 提供的 /etc/inittab 文件的内容：

```
# inittab	This file describes how the INIT process should set up
#		the system in a certain run level.
.
.
.

id:3:5:initdefault:

# System initialization.

si::sysinit:/etc/rc.d/rc.sysinit

10:0:wait:/etc/rc.d/rc 0
11:1:wait:/etc/rc.d/rc 1
12:2:wait:/etc/rc.d/rc 2
13:3:wait:/etc/rc.d/rc 3
14:4:wait:/etc/rc.d/rc 4
15:5:wait:/etc/rc.d/rc 5
16:6:wait:/etc/rc.d/rc 6

# Trap CTRL-ALT-DELETE.
ca:ctrlaltdel:/sbin/shutdown -t3 -r now

# When our UPS tells us power has failed, assume we have a few minutes
# of power left. Schedule a shutdown for 2 minutes from now.

# This does, of course, assume you have powerd installed and your
# UPS connected and working correctly.
pf:powerfail:/sbin/shutdown -h +2 "Power Failure; System Shutting Down"

# If power was restored before the shutdown kicked in, cancel it.
pr:12345:powerokwait:/sbin/shutdown -c "Power Restored; Shutdown Cancelled"

# Run getty in standard runlevels
1:2345:respawn:/sbin/mingetty tty1
2:2345:respawn:/sbin/mingetty tty2
3:2345:respawn:/sbin/mingetty tty3
4:2345:respawn:/sbin/mingetty tty4
5:2345:respawn:/sbin/mingetty tty5
```

