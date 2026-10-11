
正如前面提到的，许多 Linux 发行版已从经典的守护进程转向更现代的 Upstart 守护进程。RHEL 和 Ubuntu 发行版也包含其中。

### Upstart 基础

正如前面提到的，许多 Linux 发行版已从经典的守护进程转向更现代的 Upstart 守护进程。RHEL 和 Ubuntu 发行版也包含其中。

### Upstart 守护进程基础

正如前面提到的，许多 Linux 发行版已从经典的守护进程转向更现代的 Upstart 守护进程。RHEL 和 Ubuntu 发行版也包含其中。

在 RHEL 和 Ubuntu 发行版中，包含了 Upstart 基础。

# 第 15 章：启动和停止服务

## 第四部分：成为 Linux 服务器管理员

图 15.3

服务器启动时 Upstart init 守护进程的操作流程

![](img/47358dd1a47f0ba12c47c96b4fe178b7_419_0.png)

Upstart 对 SysVinit 的后兼容性

Upstart 为 SysVinit 守护进程提供了后兼容。这使得 Linux 发行版能够缓慢迁移到 Upstart。

`/etc/inittab` 文件在某些发行版中仍然存在。RHEL 和 Fedora 发行版仍然使用 Upstart `/etc/inittab` 启动到列出的默认运行级别（runlevel）。Ubuntu 发行版不再拥有该文件。下面的 `/etc/inittab` 文件示例来自运行版本 Fedora 的服务器，该服务器使用 Upstart init 守护进程。

```bash
$ cat /etc/inittab
# inittab 仅供 upstart 用于默认运行级别。
#
```

# 在此处添加其他配置将对您的系统产生没有任何影响。

#

#

:5:initdefault:

正如你从 `/etc/inittab` 文件的注释行看到的，对于维护该文件的 Linux 发行版，它用于更改服务器启动时的默认运行级别。

> 提示
>
> 要更改使用 Upstart 的 Ubuntu 发行版上的默认运行级别，请编辑 `/etc/init/rcysinit.conf` 并将 `env DEFAULT_RUNLEVEL=#` 中的 `#` 从 2 改为 5。但请记住，Ubuntu 上的运行级别 2-5 等于 SysVinit 运行级别 5。因此，此操作是无效的。

某些发行版（如 Ubuntu）通过 `/etc/init/rc-sysinit.conf` 维持了系统初始化与 SysVinit 的兼容性。这是系统启动时使用的配置文件之一，如图 15.3 所示。在下面的示例中，你可以看到 Upstart 会检查 `/etc/inittab` 文件并运行 `/etc/init.d/rc` 目录中可能的所有脚本：

```bash
$ /etc/init/rc-sysinit.conf
# rc-sysinit - System Vinit initialisation compatibility
## 此任务运行旧的 V 风格系统初始化脚本，
# 完成后进入默认运行级别。
...
start on (filesystem and static-network-up) or failsafe-boot
stop runlevel
...
# 默认运行级别，可以通过内核命令行
# 通过创建一个旧的 /etc/inittab 条目来覆盖
env DEFAULT_RUNLEVEL=2
...
emits runlevel
task
```
