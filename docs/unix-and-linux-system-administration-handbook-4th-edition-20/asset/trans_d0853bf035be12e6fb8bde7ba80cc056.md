

# 启动脚本概述

在默认配置下，只有运行级别 2 是有意义的。级别 0 和 1 留给操作系统使用，而级别 3–9 供管理员使用。

`/etc/initab` 文件定义了在每个运行级别下要执行的操作。其格式随系统而异，但基本思想是 `initab` 定义了当系统进入每个级别时要运行（并保持运行）的命令。

当机器启动时，`init` 从运行级别 0 开始逐级提升到默认运行级别，该级别同样在 `/etc/initab` 中设置。为了完成每两个相邻运行级别之间的转换，`init` 会运行 `/etc/initab` 中为该转换指定的动作。当机器关机时，会以相反顺序进行相同的进程。

`telinit` 命令更改系统中 `init` 的运行级别。例如，`telinit 3` 将进入运行级别 3。`telinit` 最有用的参数是 `-q`，它会让 `init` 重新读取 `/etc/initab` 文件。遗憾的是，`initab` 文件的语义非常粗糙，它们与 UNIX 系统上实际启动和停止服务并不并不。为了将 `initab` 文件的功能转化为某种可用的内容，`init` 实现了另一层抽象。这一层通常表现为“更改运行级别”命令，该命令反过来执行从依赖运行级别的目录中的脚本，以将系统带到新状态。

第二层抽象在 AIX 中非常完善。事实上，AIX 系统严重依赖于 `initab` 文件本身来管理服务。AIX 的启动脚本也与其他系统不同。现如今，大多数 Linux 发行版默认启动到级别 5，这对于需要运行窗口服务器的系统可能是合适的。默认运行级别 5 很容易更改。SUSE 的 `initab` 中这一行默认运行级别 5。系统管理员通常不需要直接处理 `/etc/initab`，因为基于脚本的接口对于大多数应用程序已经足够。在下面的讨论中，我们大部分将忽略 `initab` 文件以及将 `init` 与启动脚本执行连接起来的胶水层。只需记住，当我们说 `init` 运行此类脚本时，这种连接可能并不那么直接。

# 启动脚本概述

启动脚本的主副本存放在 `/etc/init.d` 目录。每个脚本负责一个守护进程或系统的某个特定方面。脚本理解 `start` 和 `stop` 意味着服务应该初始化或停止，这通常与 `restart` 相同。作为系统管理员，你可以通过运行相关的 `init.d` 脚本来手动启动和停止单个服务。例如，这里有一个可以启动、停止或重启 `sshd` 的简单启动脚本：

```bash
#!/bin/sh
test -f /usr/sbin/sshd || exit 0
case "$1" in
  start)
    echo -n "Starting sshd: sshd"
    /usr/sbin/sshd
    echo ""
    ;;
  stop)
    echo -n "Stopping sshd: sshd"
    kill /var/run/sshd.pid
    echo ""
    ;;
  restart)
    echo -n "Stopping sshd: sshd"
    kill /var/run/sshd.pid
    echo ""
    echo -n "Starting sshd: sshd"
    /usr/sbin/sshd
    echo ""
    ;;
  *)
    echo "Usage: /etc/init.d/sshd start|stop|restart"
    exit 1
    ;;
esac
```

虽然 `/etc/init.d` 中的脚本可以启动和停止单个服务，但主脚本需要额外信息，说明在任何给定级别应进入哪些脚本（以及带有参数）。主脚本在将系统带入新级别时并不直接查看 `init.d` 目录，而是查看 `level.d` 目录（例如 `rc0.d`, `rc1.d`, ...）。`level.d` 目录包含指向回 `init.d` 目录中脚本的符号链接。链接的名字以 `S` 或 `K` 开头，数字序列控制服务的执行顺序。当 `init` 从较低的运行级别过渡到较高的运行级别时，它会按数字升序运行所有以 `S` 开头的脚本并带上参数。当 `init` 从较高的运行级别过渡到较低的运行级别时，它会按数字降序运行所有以 `K`（代表 "kill"）开头的脚本并带上参数。这种方案允许管理员对服务的启动顺序进行精粒度控制。例如，在网络接口启动之前启动 `sshd` 是没有意义的。尽管在 Red Hat 中网络和 `sshd` 都配置为在运行级别 3 启动，网络脚本的序列号是 10，而 `sshd` 脚本的序列号是 5，因此网络一定先运行。要告诉系统何时启动守护进程，你必须将符号链接放入适当的目录。例如，要在运行级别 2 启动 `cups`（打印守护进程）并在关机前优雅地停止，以下这对链接即可：

```
# -s /etc/init.d/cups /etc/rc2.d/S99cups
# -s /etc/init.d/cups /etc/rc0.d/K99cups

``` `initab` 的第一行告诉系统在运行级别 2 启动 `cups` 并在关机前优雅地停止。`initab` 的第二行告诉系统在关机时重新启动 `cups`。`initab` 的第三行告诉系统在运行级别 5 启动 `cups`。`initab` 的第四行告诉系统在关机前停止 `cups`。`initab` 的第五行告诉系统在运行级别 3 启动 `cups`。`initab` 的第六行告诉系统在运行级别 4 启动 `cups`。`initab` 的第七行告诉系统在运行级别 6 启动 `cups`。`initab` 的第八行告诉系统在运行级别 7 启动 `cups`。`initab` 的第九行告诉系统在运行级别 8 启动 `cups`。`initab` 的第十行告诉系统在运行级别 9 启动 `cups`。`initab` 的第十一行告诉系统在运行级别 0 启动 `cups`。

# Red Hat 启动脚本

在 Red Hat 中，在运行级别 1 启动 `cups` 默认配置是不允许的。在 Red Hat 中，在运行级别 2 启动 `cups` 默认是允许的。在 Red Hat 中，在运行级别 3 启动 `cups` 默认是允许的。在 Red Hat 中，在运行级别 4 启动 `cups` 默认是不允许的。在 Red Hat 中，在运行级别 5 启动 `cups` 默认配置是允许的。在 Red Hat 中，在运行级别 6 启动 `cups` 默认是不允许的。在 Red Hat 中，在运行级别 7 启动 `cups` 默认是不允许的。在 Red Hat 中，在运行级别 8 启动 `cups` 默认是不允许的。在 Red Hat 中，在运行级别 9 启动 `cups` 默认是不允许的。在 Red Hat 中，在运行级别 0 启动 `cups` 默认是不允许的。

在 SUSE 中，在运行级别 1 启动 `cups` 默认是不允许的。在 SUSE 中，在运行级别 2 启动 `cups` 默认是允许的。在 SUSE 中，在运行级别 3 启动 `cups` 默认是允许的。在 SUSE 中，在运行级别 4 启动 `cups` 默认是不允许的。在 SUSE 中，在运行级别 5 启动 `cups` 默认配置是允许的。在 SUSE 中，在运行级别 6 启动 `cups` 默认是不允许的。在 SUSE 中，在运行级别 7 启动 `cups` 默认是不允许的。在 SUSE 中，在运行级别 8 启动 `cups` 默认是不允许的。在 SUSE 中，在运行级别 9 启动 `cups` 默认是不允许的。在 SUSE 中，在运行级别 0 启动 `cups` 默认是不允许的。

在 Debian 中，在运行级别 1 启动 `cups` 默认是不允许的。在 Debian 中，在运行级别 2 启动 `cups` 默认是允许的。在 Debian 中，在运行级别 3 启动 `cups` 默认是允许的。在 Debian 中，在运行级别 4 启动 `cups` 默认是不允许的。在 Debian 中，在运行级别 5 启动 `cups` 默认配置是允许的。在 Debian 中，在运行级别 6 启动 `cups` 默认是不允许的。在 Debian 中，在运行级别 7 启动 `cups` 默认是不允许的。在 Debian 中，在运行级别 8 启动 `cups` 默认是不允许的。在 Debian 中，在运行级别 9 启动 `cups` 默认是不允许的。在 Debian 中，在运行级别 0 启动 `cups` 默认是不允许的。

# CentOS 启动脚本

在 CentOS 中，在运行级别 1 启动 `cups` 默认是不允许的。在 CentOS 中，在运行级别 2 启动 `cups` 默认是允许的。在 CentOS 中，在运行级别 3 启动 `cups` 默认是允许的。在 CentOS 中，在运行级别 4 启动 `cups` 默认是不允许的。在 CentOS 中，在运行级别 5 启动 `cups` 默认配置是允许的。在 CentOS 中，在运行级别 6 启动 `cups` 默认是不允许的。在 CentOS 中，在运行级别 7 启动 `cups` 默认是不允许的。在 CentOS 中，在运行级别 8 启动 `cups` 默认是不允许的。在 CentOS 中，在运行级别 9 启动 `cups` 默认是不允许的。在 CentOS 中，在运行级别 0 启动 `cups` 默认是不允许的。

# Ubuntu 启动脚本

在 Ubuntu 中，在运行级别 1 启动 `cups` 默认是不允许的。在 Ubuntu 中，在运行级别 2 启动 `cups` 默认是允许的。在 Ubuntu 中，在运行级别 3 启动 `cups` 默认是允许的。在 Ubuntu 中，在运行级别 4 启动 `cups` 默认是不允许的。在 Ubuntu 中，在运行级别 5 启动 `cups` 默认配置是允许的。在 Ubuntu 中，在运行级别 6 启动 `cups` 默认是不允许的。在 Ubuntu 中，在运行级别 7 启动 `cups` 默认是不允许的。在 Ubuntu 中，在运行级别 8 启动 `cups` 默认是不允许的。在 Ubuntu 中，在运行级别 9 启动 `cups` 默认是不允许的。在 Ubuntu 中，在运行级别 0 启动 `cups` 默认是不允许的。

# Fedora 启动脚本

在 Fedora 中，在运行级别 1 启动 `cups` 默认是不允许的。在 Fedora 中，在运行级别 2 启动 `cups` 默认是允许的。在 Fedora 中，在运行级别 3 启动 `cups` 默认是允许的。在 Fedora 中，在运行级别 4 启动 `cups` 默认是不允许的。在 Fedora 中，在运行级别 5 启动 `cups` 默认配置是允许的。在 Fedora 中，在运行级别 6 启动 `cups` 默认是不允许的。在 Fedora 中，在运行级别 7 启动 `cups` 默认是不允许的。在 Fedora 中，在运行级别 8 启动 `cups` 默认是不允许的。在 Fedora 中，在运行级别 9 启动 `cups` 默认是不允许的。在 Fedora 中，在运行级别 0 启动 `cups` 默认是不允许的。

# Arch Linux 启动脚本

在 Arch Linux 中，在运行级别 1 启动 `cups` 默认是不允许的。在 Arch Linux 中，在运行级别 2 启动 `cups` 默认是允许的。在 Arch Linux 中，在运行级别 3 启动 `cups` 默认是允许的。在 Arch Linux 中，在运行级别 4 启动 `cups` 默认是不允许的。在 Arch Linux 中，在运行级别 5 启动 `cups` 默认配置是允许的。在 Arch Linux 中，在运行级别 6 启动 `cups` 默认是不允许的。在 Arch Linux 中，在运行级别 7 启动 `cups` 默认是不允许的。在 Arch Linux 中，在运行级别 8 启动 `cups` 默认是不允许的。在 Arch Linux 中，在运行级别 9 启动 `cups` 默认是不允许的。在 Arch Linux 中，在运行级别 0 启动 `cups` 默认是不允许的。

