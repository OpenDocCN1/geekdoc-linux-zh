
`lrwxr-xr-x 2 root root 14 Feb 27 2000 K90 -> ../init.d/named`

`lrwxr-xr-x 2 root root 16 Feb 27 2000 K94 -> ../init.d/pcmia`

`lrwxr-xr-x 2 root root 16 Feb 27 2000 K95 -> ../init.d/syslog`

`lrwxr-xr-x 2 root root 17 Feb 27 2000 K95 -> ../init.d/urandom`

`lrwxr-xr-x 2 root root 17 Feb 27 2000 K99 -> ../init.d/network`

`lrwxr-xr-x 2 root root 13 Feb 27 2000 K99 -> ../init.d/zap`

`lrwxr-xr-x 2 root root 14 Feb 27 2000 S99 -> ../init.d/halt`

`rc` 目录中的脚本被链接到 `/etc/rc.d/init.d` 中的主副本。

当你运行到级别 5 时，`/etc/rc.d/rc5` 中的所有脚本都以 `S` 开头。级别 1、2 和 3 的 init 脚本包含了 `K` 和 `S` 脚本。

# 查看简单的 rc.local 文件

如果你只计划一两个特定的系统任务，最简单的方法是将它们写入 `rc.local`。如果你计划运行一些复杂的初始化程序，你应该创建 `K` 或 `S` 脚本并将它们添加到相应的目录。这种方法可以保持 `rc.local` 的简单，并使你复杂的初始化脚本井井有序。

## 从 init 到 rc.local

`init`（作业 1）是所有进程的父进程。当你启动系统时，Linux 会读取 `/initab` 文件以查看如何设置每个运行级别。在大多数 Linux 发行版中，运行级别范围从 0 到 6：

- 0 - 停止
- 1（或 S）- 单用户模式
- 2 - 无网络的多用户模式
- 3 - 带网络的多用户模式
- 4 - 通常未使用
- 5 - 带有网络和 X 系统的多用户模式
- 6 - 重启

在 Linux 执行完运行级别所需的所有 init 脚本后，它会执行 `/etc/rc.local`。在 Berkeley 风格的 UNIX 中，系统管理员将所有的系统材料放在 `rc.local` 中。你也可以在 Linux 中这样做。

# 572 第 V 部分 高级系统管理与网络管理

```sh
#!/bin/sh

# 此脚本将在所有其他初始化脚本*之后*执行。

# 如果你不想执行完整的 Sys V 风格初始化操作，

# 可以在这里放置你自己的初始化内容。

if [ -r /etc/.issue ]; then

    cat /etc/.issue > /etc/issue

else

    cat << EOI > /etc/issue

Caldera OpenLinux(TM)

Copyright (C) 1996-1998 Caldera, Inc.

EOI

fi

cp -f /etc/issue /etc/issue.net

echo >> /etc/issue
```

`rc.local` 脚本在每次有人登录系统时，都会创建一个简单的信息消息，包括 Linux 发行版的名称、版本号和版权信息。后续文本 `/etc/issue` 存储了该消息。注意，版本号是硬编码在文件中的。

这是 `rc.local` 创建的 `/etc/issue` 文件。

Caldera Linux eServer
Version 2.3
Copyright 1996-1999 Caldera Systems, Inc.

## 为 rc.local 添加复杂性

下一个 `rc.local` 示例来自运行 Red Hat Linux 的 flyingpenguin。Red Hat 的 `rc.local` 基本上与 Caldera 的 `rc.local` 文件执行相同的操作：它显示存储在 `/etc/issue` 中的信息消息。文件之间的区别在于，Red Hat 版本对系统架构的检查比 Caldera 版本更详细。例如，下面的 `rc.local` 文件确定了计算机中有多少个处理器，如果架构是 SMP（对称多处理，即具有多个 CPU），`rc.local` 将将处理器的数量作为系统信息消息的一部分输出。两个 `rc.local` 文件的另一个区别是，Red Hat 版本没有将发行号硬编码到 `/etc/issue` 文件中。它会检查额外文件 `/etc/redhat-release` 是否存在。

```sh
# cat /etc/rc.d/rc.local
#!/bin/sh
#
```

# 第 30 章 系统管理员的 Shell 脚本

```sh
# 此脚本将在所有其他初始化脚本*之后*执行。

# 如果你不想执行完整的 Sys V 风格初始化操作，

# 可以在这里放置你自己的初始化内容。
```

```sh
if [ -f /etc/redhat-release ]; then
  R=$(cat /etc/redhat-release)
arch=$(uname -m)
a="a"
  case "$arch" in
    *) a="an";
      *i*) a="an";
  esac
```

```sh
NUMPROC=$(grep -cl "^cpu[0-9]*" /proc/stat)
if [ "$NUMPROC" -gt 1 ]; then
  SMP=$NUMPROC-processor
  if [ "$NUMPROC" -eq 8 -o "$NUMPROC" -eq 11 ]; then
    a="an"
  else
    a="a"
```

```sh
# 此操作将在每次启动时覆盖 /etc/issue。因此，请在此处对 /etc/issue
# 进行任何你想执行的更改，否则在重启时这些更改将会丢失。

echo "" >> /etc/issue
echo "SR" >> /etc/issue
echo "Kernel $(uname -m) on r $a $SMP$" >> /etc/issue
```

```sh
cp -f /etc/issue
echo >> /etc/issue
```

```sh
# 站点特定的自定义在此处。
# 启动 sshd（安全外壳守护进程）。
#
/usr/local/sbin/sshd
# 启动任何 PCMCIA 设备
if [ -x /etc/rc.d/rc.pcmcmia ];
then
  /etc/rc.d/rc.pcmcmia start
# 检查 rc.modules 文件以查看是否需要加载动态模块。
# 如果需要，继续加载。
if [ -x /etc/rc.d/rc.modules ];
then
  /etc/rc.d/rc.modules
```

> 注意
上述文件的最后部分启动了安全外壳守护进程 `sshd`。这一行是由系统管理员插入的站点特定自定义。

## 来自 rc.local 的脚本提示和技巧

虽然 Shell 脚本是一种容易掌握的技能，但通常有一些会让学者困惑的细微之处。本节介绍了一些在创建新脚本或修改现有脚本时可以使用的技巧，帮助避免常见的陷阱。

### 技巧 1. 在访问文件之前，始终检查文件是否存在。

Red Hat 版本 `rc.local` 中的第一个 `if` 测试检查文件 `/etc/redhat-release` 是否存在。

```sh
if [ -f /etc/redhat-release ]; then
R=$(cat /etc/redhat-release)
```

如果 `redhat-release` 文件是一个普通文件，`rc.local` 继续处理 `then` 子句之后的语句。如果 `redhat-release` 文件不存在，脚本将跳过 `then` 子句并继续处理脚本中的下一个语句。

关于 `if-else` 语法和选项的更多信息，请参见第 18 章。

当你编写访问其他脚本或文件的脚本时，始终先检查文件是否存在。如果你引用的文件不存在，脚本将生成如下错误并立即退出：

```
cat: redhat-release: No such file or directory
```

如果 `redhat-release` 文件是一个普通文件，`rc.local` 继续处理 `then` 子句之后的语句。如果 `redhat-release` 文件不存在，脚本将跳过 `then` 子句并继续处理脚本中的下一个语句。

一个常见的任务是如果文件存在则生成消息。下面的示例展示了如何测试该文件：

```sh
#!/bin/bash
# 检查文件是否存在
if [ -f /etc/redhat-release ]; then
  echo "The file exists"
```
