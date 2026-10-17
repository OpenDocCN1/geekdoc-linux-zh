
启动脚本在系统切换到新运行级别时运行。此运行级别通常是多用户级别（如 3 或 5），但只要满足依赖，可以在任何运行级别启动。表 6-8 列出的脚本在系统 `init` 时被调用。

| 表 6-8 | 启动脚本 | 描述 |
| :--- | :--- | :--- |
| `/etc/init.d/network` |  | 系统启动时处理网络硬件和软件的配置。 |
| `/etc/init.d/inetd` |  | `xinetd` 使系统服务可用。例如，当 FTP 连接启动时，可以启动 `vsftp`。 |
| `/etc/init.d/portmap` |  | 为 RPC（远程过程调用）服务（如 NFS 服务器）启动 `portmapper`。 |
| `/etc/init.d/nsserver` |  | 启动 NFS 服务器。 |
| `/etc/init.d/sendmail` |  | 控制 `sendmail` 进程。 |
| `/etc/init.d/ypserv` |  | 启动 NIS 服务器。 |
| `/etc/init.d/ypbind` |  | 启动 NIS 客户端。 |

# 描述启动脚本和服务

网络服务的脚本需要在网络脚本运行。由于网络脚本不在运行级别 1 ，因此运行级别 1 不能使用网络服务脚本。

# 启动目录结构

以下是 SUSE Linux Server 9 环境中启动脚本的目录。

- `/etc/init.d/`. 这是存储启动脚本的目录。
- `/etc/init.d/rcn.d/`. 这些目录存储每个运行级别到 `/etc/init.d/` 的链接。例如，运行级别 5 的目录是 `/etc/init.d/rc5.d`。

`rcn` 目录中的符号链接与运行级别 6–5 中显示的类似。

```
rwxrxr-x 1 root root 6 Jul 09:47 Mfsinit -> ~init
rwxrxr-x 1 root root 10 Jul 09:47 Mfsboot -> ~mfboot
rwxrxr-x 1 root root 10 Jul 21:00 Mfslock -> ~mfslock
rwxrxr-x 1 root root 9 Jul 11:37 Kinetwork -> ~network
rwxrxr-x 1 root root 9 Jul 09:47 Kinet-portmap -> ~portmap
rwxrxr-x 1 root root 8 Jul 08:01 Ssmfs -> ~smfs
rwxrxr-x 1 root root 10 Jul 07:46 Splash-early -> ~splash_early
rwxrxr-x 1 root root 9 Jul 09:46 Fsysylog -> ~sysylog
```

图 6-5

链接的名称带有 S（启动）或 K（杀死）前缀和一个两位数字。

在系统启动期间，带有 S 前缀链接按数字顺序访问（对于相同优先级的脚本则按字母顺序排序）。当访问每个链接时，相应的脚本都会接收到传递的参数。

在正常关机期间，带有 K 前缀脚本按顺序访问，并传递 `stop` 参数给相应的脚本。

这按照预定义的顺序关闭服务，并确保在系统关闭之前所有服务都已关闭。

## 启动脚本结构

以下是位于 `/etc/init.d/` 中的文件骨架。你可以使用该骨架创建你自己的启动脚本：

```
#!/bin/sh
# Copyright (c) 1995-2004 SUSE Linux AG, Nuernberg, Germany.
# All rights reserved.
# Author: Kurt Garloff
# 请将反馈发送至 http://www.suse.de/feedback/
# /etc/init.d/FOO
# 以及它的符号链接
# (usr)/sbin/rcFOO
# 某些示例服务/守护进程 FOO 的模板启动脚本
# 兼容 LSB 服务控制脚本；
# 参见 http://www.linuxbase.org/spec/# 注意：此模板使用了在 /etc/rc.status 中定义的 rc_XXX 函数
# 适用于基于 UnitedLinux (UL) 的 Linux 发行版。如果你想
# 基于此模板编写脚本并确保它在非基于 UL 的符合 LSB
# 的 Linux 发行版上运行，你必须提供 UL 的 rc.status
# 函数，或者修改脚本使其在没有它们的情况下运行。
### BEGIN INIT INFO
FOO
# Provides: $syslog $remote_fs
# Required-Start: $syslog $bind
# Should-Start: $time ypbind sendmail
```

你可以通过输入 `less /etc/init.d` 查看此文件的内容（长达几页），或使用任何文本编辑器编辑该文件。

> 如果你位于 SLES 9 服务器上，我们建议在查看以下信息时显示文件骨架。

## 描述启动 Shell 脚本与服务 349

以下是构建启动脚本模板中一些较重要的部分：

- 通用部分 (General Section)
- 启动部分 (Start Section)
- 停止部分 (Stop Section)
- 重启部分 (Restart Section)
- 强制重载部分 (Force-Reload Section)
- 重载部分 (Reload Section)
- 状态选项 (*)
- 最后选项 (*)

关于 `init`、`/etc/init.d` 脚本和运行级别（runlevels）的更多细节，请参见第 5 节中的“运行级别基础”（Runlevel Basics)。

![](img/667acce1695f6403deb2b60e994760c8_368_0.png)

### 通用部分

在检查传递给脚本的参数之前，通用部分中的命令无论传递了什么参数都会执行。

这些命令测试某些文件和可执行文件的存在性、设置变量，并定义函数或读取配置文件（如下）：

```
# 检查缺失的二进制文件（不应出现过期的符号链接）
# 注意：针对 LSB 兼容性的 stop 的特殊处理
FOO_BIN=/usr/sbin/FOO
test -x $FOO_BIN || echo "$FOO_BIN not installed"
if [ "$1" = "stop" ]; then
  exit 0;
else
  exit 6;
fi;
```

```
# 检查所需的配置文件是否存在并读取它
FOO_CONFIG=/etc/sysconfig/FOO
test -r $FOO_CONFIG || echo "$FOO_CONFIG not existing"
if [ "$1" = "stop" ]; then
  exit 0;
else
  exit 6;
fi;
```

```
# 读取配置
$FOO_CONFIG
```

在通用部分之后，为传递给脚本的每个有效参数都有对应的部分。如果传递了错误的参数，将显示一条简短的帮助信息显示有效参数。

### 启动部分

传递给脚本的参数使用脚本内部的 `case` 语句进行评估，如下：

```
case "$1" in
```

在此示例中，命令行提取第一个参数 (`$1`) 来对后续行进行比较：

```
case "$1" in
  start)
    echo -n "Starting FOO "
    ## 使用 startproc(8) 启动守护进程。如果执行失败
    ## 返回值将由 startproc 适当设置。
    startproc $FOO_BIN

    # 根据 LSB 设置状态
    rc_status
  ;;
```

此部分将第一个参数与 `start` 值进行比较，如果匹配则执行后续代码。

### 停止部分

与启动部分类似，停止部分通过发送 `SIGTERM` 信号来干净地停止进程：

```
stop)
  echo -n "Shutting down FOO "
  ## 使用 killproc(8) 停止进程，如果执行失败
  ## killproc 会根据 LSB 设置返回值。
  killproc -TERM $FOO_BIN

  # 根据 LSB 设置状态
  rc_status
  ;;
try-restart|condrestart)
  ## 仅当服务之前处于激活状态时重启
  ## 注意：try-restart 现在是 LSB 的一部分（1.9）。
  ## RH 有一个名为 condrestart 的命令。
  if test "$1" = "condrestart"; then
    echo "Use try-restart rather than condrestart"
  fi
  $0 status
  if test $? = 0; then
```

```
  else
  rc_reset # 未运行表示失败。
  fi
```

## 描述启动 Shell 脚本与服务 351

### 重启部分

重启部分用于重启服务：
