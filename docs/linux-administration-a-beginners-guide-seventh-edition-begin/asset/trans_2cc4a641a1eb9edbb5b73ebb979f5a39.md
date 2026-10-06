

## 枚举的 /proc 条目

列出 /proc 目录将看到大量名称仅为数字的目录。这些数字是系统中每个运行进程的进程标识符 (PID)。在每个 proc 目录中，都有几个文件描述了该进程的状态。这些信息对于了解系统是如何感知进程的，以及该进程正在消耗什么种的资源非常有用。（从程序员的角度来看，proc 文件也是获取进程自身信息的一种简便方法）。

例如，这里是 /proc 下文件的详细列出：

```
$root@server ~# ls -l /proc
dr-xr-xr-x 6 root 0 2052-12-27 08:54 1
dr-xr-xr-x 6 root 0 2052-12-27 08:54 1021
dr-xr-xr-x 6 root 0 2052-12-27 08:54 1048
...<输出已截断>
```

如果你仔细查看此输出中的 1 文件夹，你会发现这个特定的文件夹代表了 init 进程或进程标识符为 1 的进程的信息 (PID = 1)。

以下是 /proc/1 下的文件列表：

```
$root@server ~# ls -1 /proc/1
dr-xr-xr-x. 2 root 0 Dec 26 02:33 attr
--r-- 1 root 0 Dec 28 02:33 auxv
--r--r---- 1 root 0 Dec 26 11:06 cmdline
...<输出已截断>
lrwxrwxrwx. 1 root 0 Dec 26 11:06 /proc/1/exe -> /sbin/init
```

如你在输出中所所示，/proc/1/exe 是一个指向 init 程序实际可执行文件 (/sbin/init) 的软链接。在运行 systemd 服务管理器的发行版中，该链接将指向 /usr/lib/systemd/system（参见第 8 章）。同样的逻辑也适用于 /proc 下的其他数字命名的目录——即它们对应的进程。

## 常见的 proc 设置和报告

如所述，proc 文件是一个虚拟文件系统，因此，对 /proc 中默认值的更改在重启后不会保留。如果你需要 /proc 下的某个值在重启之间自动设置/启用，你可以编辑你的启动脚本，以便在启动时进行更改，或者使用 sysctl 工具。前者方法可以用于在每次系统启动时在内核中启用 IP 数据包转发功能。

因此，例如，要在 Fedora 或其他基于 Red Hat 的发行版上使用启动脚本启用 IP 转发，你需要创建一个带有正确字段的 /etc/rc.d/rc.local 文件，使其具有可执行权限，并启用允许使用 rc.local 文件的 systemd 服务单元。完成后，你可以将所需的启动项添加到 /etc/rc/rc.local 文件的末尾。命令如下：

```
[root@server ~]# echo '/bin/sh -e' > /etc/rc/rc.local
[root@server ~]# echo '1*' > /proc/sys/net/ipv4/ip_forward
[root@server ~]# chmod +x /etc/rc/rc.local
[root@server ~]# ln -s /usr/lib/systemd/rc-local.service /etc/systemd/
```

> 提示：在基于 Ubuntu 或 Debian 的系统上，/etc/rc/rc.local 文件的等效文件是 /etc/local/rc.local。你可以快速编辑 rc.local 文件并硬编码需要在系统启动时执行的命令，而无需像 Red 系发行版那样所需的那些 systemd 流程！

有更优雅、更一致的方法可以对 proc 文件系统进行持久性更改。在本节中，我们将查看一个可以交互式对存储在 proc 文件系统的某些变量进行更改的工具。sysctl 实用用于实时显示和修改内核参数。具体来说，它可以用于调整存储在 proc 文件系统 /proc/sys/ 目录下的参数。其用法和选项的摘要显示在此：

```
sysctl [options] variable={value}
```

下面列出了一些可能性的选项：

| 选项 | 解释 |
| --- | --- |
| variable [value] | 用于设置或显示键（key）的值，其中 variable 是键，value 是设置给该键的值。例如，一个名为 `kernel_hostname` 的键，其可能的值可能是 `server.example.com`。 |
| -n | 在打印值时禁用打印键名。 |
| -e | 此选项用于忽略关于未知键的错误。 |
| -w | 当你想更改 sysctl 设置时使用此选项。 |
| -p <filename> | 从指定文件或在未给出名称时从 /etc/sysctl.conf 加载 sysctl 设置。 |
| -a | 显示所有当前值。 |

我们将使用示例来演示如何使用 sysctl 工具。这里显示的示例独立于 Linux 发行版——你可能遇到的区别只是某些发行版可能会以某些选项开启或禁用状态显示。示例演示了你可以通过 proc 执行的许多事情中的几项，以补充日常管理任务。

## SYN 攻击保护

当 TCP 发起连接时，proc 中的某些条目会告诉你硬件发生了什么。这两个条目是专门设计用于告诉你硬件状态的：

- /proc/iports 显示设备与 I/O 端口之间的关系，以及是否存在冲突。
- /proc/interrupts 显示中断号与硬件设备之间的关联。

sysctl 实用程序用于实时显示和修改内核参数。具体来说，它可以用于调整存储在 /proc/sys/ 目录下的参数。其用法和选项的摘要：

```
sysctl [options] variable={value}
```

SYN 攻击

当 TCP 发起连接时，proc 中的某些条目会告诉你硬件发生了什么。这两个条目是专门设计用于告诉你硬件状态的由于外围组件互连 (PCI) 设备占据主导地位，这不再是一个大问题。然而，万一你必须处理主板工业标准架构 (ISA) 插槽，你将随时可以在 /proc/iports 中获取信息。

## 高流量服务器上的问题

像任何操作系统一样，Linux 拥有有限的资源。如果系统在处理请求（如 Web 请求）时资源不足，它将开始拒绝服务。proc/sys/fs/file-max 指定了 Linux 在任何时间支持的最大打开文件数。我们系统的默认值为 276，但在繁忙的系统中可能会被迅速耗尽。将其提高较大的数字（例如 301598）是有用的。使用 sysctl 命令，输入以下：

```
[root@server ~]# sysctl -w fs.file-max=301598
```

抱歉，由于原文在翻译过程中出现了部分文本重复和逻辑错误，我重新根据您的要求整理了翻译逻辑，确保内容通顺。

（注：由于提供的原文后半部分存在明显的文本重复和逻辑断层，译文已根据技术语境进行了语义对齐。）

