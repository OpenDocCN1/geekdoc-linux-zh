
| 1, s, S | 这代表单用户模式，最常用于系统维护，以及可能希望运行少数进程且不激活服务的情况。在单用户模式下，网络不存在，X Server 未运行，且某些文件系统可能未挂载。 |

| 2 | 多用户模式。允许多个用户登录，挂载所有配置的文件系统，并启动除 X、守护进程、xineted 守护进程以及 NIS/NFS 之外的所有进程。如果你的机器不需要永久连接，这是 `initdefault` 的良好选择。 |

| 3, 4 | 带有服务的多用户模式。运行级别 3 是 Red Hat Linux 服务器典型的 `initdefault` 值，但运行级别 4（通常留给用户定义）在默认 Red Hat 7.0 配置中几乎相同。 |

| 5 | 带有服务和 X的多用户模式。此运行级别启动 X 服务器并呈现图形登录窗口，视觉上类似于任何昂贵的基于 Unix的工作站。这是 Red Hat Linux 工作站的常见 `initdefault` 值。 |

| 6 | 所有进程被终止，机器优雅地重启。再次，inittab 文件中的注释提到这不是 `initdefault` 的良好选择，甚至比运行级别 0 更糟糕。其结果可能是启动后又重启的无限循环。 |

## 表 12-5（续）

| 运行级别 | 在此运行级别发生的操作 |

| --- | --- |

| 7, 8, 9 | 通常不使用且未定义，这些运行级别具有满足默认选项未涵盖的任何需求的潜力。 |

| a, b, c, A, B | 与 ondemand 动作配合使用。这些级别并没有指定具体的运行级别，但在接到指令时可以“按需”启动程序或守护进程。 |

如果 `inittab` 文件中没有指定 `initdefault`，启动序列将会被中断，系统会提示你指定一个默认运行级别，机器将启动到该级别。

`inittab` 文件中的下一行在进入 `/etc/rc.d/rc.sysinit` 脚本后会进入默认运行级别。该脚本执行初始化例程，例如选择键位映射文件、检查并挂载根文件系统和 `proc` 文件系统、设置时令和主机名、配置交换空间、清理临时文件以及加载系统模块。

接下来的几行控制在每个主要运行级别内执行的命令。在每个级别中，都会调用 `/etc/rc.d/rc` 脚本，并将默认运行级别作为参数传递。它随后会进入相应的目录树（例如，对于运行级别 3，会进入 `/etc/rc3.d` 目录），这将在后文中讨论。

下一行指定了机器处于任何运行级别时，更新守护进程中的应该是一个程序，将内核从内存刷新到磁盘（每 20 秒一次），以确保在发生意外关机时，丢失的数据量最少。

`ctrlalt` 告诉 `init` 执行当同时按下 `Ctrl`、`Alt` 和 `Delete` 键时 PC 用户所预期的操作。系统将在延迟 6 秒后以有序的方式自我重启（切换到运行级别 0）。

接下来的两行（带有注释）处理在你安装了不间断电源（UPS）和软件时的平稳关机。第一行在接收到来自 UPS 电源的信号后两分钟启动停止（切换到运行级别 0）。第二行在电电恢复时取消关机。

`getty` 行启动虚拟控制台以允许登录。这些进程在任何多用户运行级别中始终运行。当连接到虚拟控制台的用户注销时，该 `getty` 进程就会结束，`respawn` 动作指示 `init` 启动一个新的 `getty` 进程。

## 第 12 章 系统任务自动化

最后一行表示，只要系统处于运行级别 5，“首选显示管理器”（xdm, gnome, KDE 等）就会一直运行。这提供了一个图形化登录提示，而不是通常的文本登录，并消除了运行 `startx` 的需要。

## 系统启动与关机

在系统启动期间，会运行一系列脚本来启动所需的服务。这些包括启动网络接口、挂载目录和监控你的系统的脚本。这些脚本大部分都是从 `/etc/rc.d` 的子目录下运行的。在启动时启动这些大多数服务、并在关机时停止这些服务的程序是 `/etc/rc.d/rc` 脚本。接下来的章节将描述运行级别脚本以及你可以用它们做什么。

## 启动运行级别脚本

如前所述，`/etc/rc.d/rc` 脚本是运行级别概念中不可或缺的脚本。任何运行级别的改变都会导致脚本被执行，并将新的运行级别作为参数。这个简单而强大的脚本在此处展示并讨论：

```bash
#!/bin/bash
@ rc
# 此文件负责在运行级别改变时启动/停止服务。
# 它还负责基础事项的最首次设置，
# 例如设置主机名。
@ 原作者:
# Miquel van Smoorlenburg, <miquels@drinkel.nl.mugnet.org>
@ 源函数库。
/etc/init.d/functions
# 现在找出当前和上一个运行级别分别是什么
argv1="$1"
set "/sbin/runlevel"
runlevel=$2
previous=$1
export runlevel previous
# 检查我们是否想处于用户确认模式
if [ "$previous" = "N" ]; then
  grep -i /proc/cmdline >/dev/null || [ -f /var/run/confirm ];
then
  rm -f /var/run/confirm
```

```bash
CONFIRM=yes
else
CONFIRM=
echo "Entering non-interactive startup"
fi
```

```bash
# 获取第一个参数。将新运行级别设置为此参数。
[ "$1" != "" ] && runlevel=$$1
```

```bash
# 告诉 linuxconf：我们处于什么运行级别
[ -d /var/runlevel ] && echo "etc/rcrunlevel.d" > /var/run/runlevel.dir
```

```bash
# 是否存在此新运行级别的 rc 目录？
if [ -d /etc/rcrunlevel.d ]; then
  # 首先，运行 KILL 脚本。
  for i in /etc/rcrunlevel.d/*; do
    # 检查脚本是否存在。
    [ -f $i ] && continue
```

```bash
# 不要运行 [KS2]]foo.rpmpsave.rpmorig 脚本
[ "$i,rpmpsave" != "$i" ] && continue
[ "$i,rpmorig" != "$i" ] && continue
[ "$i,rpmnew" != "$i" ] && continue
```

```bash
# 检查子系统是否已经启动。
subsystem=${i#/etc/rcrunlevel.d/}
[ -f ] \
  [ -f /var/run/lock/${subsystem} ] && continue
```

```bash
# 检查子系统是否已经启动了。
subsystem=${i#/etc/rcrunlevel.d/}
[ -f ] \
  [ -f /var/run/lock/${subsystem} ] && continue
```

```bash
# 检查子系统是否已经启动了。
subsystem=${i#/etc/rcrunlevel.d/}
[ -f ] \
  [ -f /var/run/lock/${subsystem} ] && continue
```

```bash
# 检查子系统是否已经启动了。
subsystem=${i#/etc/rcrunlevel.d/}
[ -f ] \
  [ -f /var/run/lock/${subsystem} ] && continue
```

```bash
# 检查子系统是否已经启动了。
subsystem=${i#/etc/rcrunlevel.d/}
[ -f ] \
  [ -f /var/run/lock/${subsystem} ] && continue
```

```bash
# 检查子系统是否已经启动了。
subsystem=${i#/etc/rcrunlevel.d/}
[ -f ] \
  [ -f /var/run/lock/${subsystem} ] && continue
```

```bash
# 检查子系统是否已经启动了。
subsystem=${i#/etc/rcrunlevel.d/}
[ -f ] \
  [ -f /var/run/lock/${subsystem} ] && continue
```

```bash
# 检查子系统是否已经启动了。
subsystem=${i#/etc/rcrunlevel.d/}
[ -f ] \
  [ -f /var/run/lock/${subsystem} ] && continue
```

```bash
# 检查子系统是否已经启动了。
subsystem=${i#/etc/rcrunlevel.d/}
[ -f ] \
  [ -f /var/run/lock/${subsystem} ] && continue
```
