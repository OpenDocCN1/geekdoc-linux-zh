
```text
eric       pts/1    192.168.1.100   Sat Feb 26 09:55 - 09:55  (00:00)
belandja   pts/4    192.168.1.100   Sat Feb 26 09:54 - down     (14:02)
hart       pts/1    192.168.1.100   Sat Feb 26 09:53 - 09:54  (00:01)
root       pts/3    :0.0             Sat Feb 26 09:46 - down     (14:11)
belandja   pts/2    192.168.1.100   Sat Feb 26 09:12 - 10:14  (01:01)
hart       pts/1    192.168.1.100   Sat Feb 26 08:44 - 09:53  (01:08)
root       pts/0    0                Sat Feb 26 08:44 - down     (15:12)

wtmp begins Mon Feb 14 19:00:40 2005
```

你可以使用单独的命令快速提取特定账户的最后登录时间。这可以快速检查未使用的账户或不应被使用的账户。以下是 lastlog 命令的示例：

```text
Athena:~ # lastlog
Username         Port     From               Latest
root             pts/2    athena.universal   Sun Feb 27 12:30:43 -0500 2005
bin                       **Never logged in**
daemon                    **Never logged in**
lp                        **Never logged in**
games                     **Never logged in**
man                       **Never logged in**
.                         **Never logged in**
.                         **Never logged in**
ldap                      **Never logged in**
dhcpd                     **Never logged in**
belandja  1      192.168.1.100   Sun Feb 27 12:29:40 -0500 2005
eric      2      192.168.1.100   Sun Feb 27 12:23:43 -0500 2005
hart      1      192.168.1.100   Sat Feb 26 10:08:46 -0500 2005
peter                     **Never logged in**
pol       pts/3  192.168.1.240   Sun Feb 27 14:25:20 -0500 2005
mark      pts/4  hermes.universal Sun Feb 27 14:31:03 -0500 2005
ted       tty5                   Sun Feb 27 14:29:25 -0500 2005
```

此命令提供系统中所有账户的列表，以及它们最后登录系统的时间和登录来源。由于系统账户数量众多，列表可能会变得相当庞大。你可能会想使用 grep 解析此命令的输出，以删除从未使用过的所有账户：

```text
Athena:~ # lastlog | grep -v -e "**Never"

Username   Port      From              Latest
root       pts/2     athena.universal  Sun Feb 27 12:30:43 -0500 2005
belandja   1         192.168.1.100     Sun Feb 27 12:29:40 -0500 2005
eric       2         192.168.1.100     Sun Feb 27 12:23:43 -0500 2005
hart     1        192.168.1.100   Sat Feb 26 10:08:46 -0500 2005
pol      pts/3    192.168.1.240   Sun Feb 27 14:25:20 -0500 2005
mark     pts/4    hermes.universal Sun Feb 27 14:31:03 -0500 2005
ted      tty5                      Sun Feb 27 14:29:25 -0500 2005
```

这种方式解析输出是可以接受的，如果你正在查找已知活跃的单个账户。然而，原生的 lastlog 命令确实提供了有关系统进程账户的额外信息。验证它们是否未用于交互式登录可能会非常有用。

知道某个特定账户被不当使用是一回事。能够识别使用该账户的个人则困难得多。验证账户的登录失败次数是一个重要步骤。过多的登录失败可能是密码破解攻击的迹象——可能已成功。faillog 命令允许你检查每次登录尝试对每个账户失败的次数：

```text
Athena:~ # faillog
Username   Failures  Maximum  Latest
root       3         0        Wed Feb 16 03:49:05 -0500 2005 on 0
belandja   0         0        Mon Feb 14 19:02:11 -0500 2005 on 1
eric       0         0        Tue Feb 15 18:06:28 -0500 2005 on 2
hart       0         0        Tue Feb 15 06:57:10 -0500 2005 on 4
```

账户上出现大量登录失败的迹象可能表明该账户的密码已被破解。也可能是个诡计。制定健全的账户密码策略并包含 PAM 模块 pam_tally 在达到一定次数的失败尝试后锁定账户，是你可以采取的重要步骤。这样，你可以减轻密码收集攻击带来的部分风险。这也有助于确保最后登录到特定账户的人知道密码。

在本节中，你看到了提取用户登录信息的众多方法。你可以使用这些信息来帮助调查资源问题。这些信息也可以作为调查系统可疑行为的起点。

## 系统调优

服务器的初始性能基于操作系统供应商设置的一系列参数。在 SLES 的情况下，这些参数被选定以满足广泛的服务器类型。每个服务可能需要不同的资源。有些服务是内存或带宽密集型的，而
其他则是 CPU 密集型的。这些各种因素默认情况下被平衡，以提供响应迅速的服务器，无论其初始任务如何。

然而，无法预料的是所提供硬件的可用资源。SUSE 规定了一系列最低要求以提供稳定的环境。在大多数情况下，满足这些最低要求不是问题。随着资源限制开始导致性能问题，可以向服务器添加内存或磁盘空间。

在某些情况下，服务器的任务超出了设计的常规。在这些情况下，你必须考虑对原始配置中的基本假设进行更改。

在基于 Linux 和 Unix 的系统中，操作系统的核心程序称为内核。内核就像任何其他程序一样构建。它在其结构中包含了配置团队的原始假设。这些假设决定了哪些设备类型可用，例如 IDE 或 SCSI 磁盘，内存如何管理，以及是否可以动态加载额外模块。在内核配置中添加和移除功能可以提高灵活性和性能。

当出现这种情况时，你通常需要修改实际的 Linux 内核本身。这可以通过几种不同的方式完成。一个选项是重新编译内核以包含额外功能。当可用时，首选方法是利用默认内核的灵活性，简单地调整其部分运行时参数。

### 调优内核参数

有许多应用程序已移植到 Linux。其中一些，例如数据库应用程序，其资源需求与典型的 Linux 服务显著不同。为了满足这些需求，你必须通过调整特定于应用程序的参数来改变内核的运行方式。

在旧版本的 Unix 中，这些更改需要重新构建内核本身。虽然不是不可逾越的壮举，但对于从未做过的人来说，重建内核无疑是一项艰巨的任务。幸运的是，Linux 内核具有灵活性和动态性。可以在实时中对 Linux 内核进行更改，而无需重新启动。

例如，让我们看看 Linux 内核需要进行哪些更改才能运行 Oracle 10g。这些更改在安装时运行的脚本中提供；就论证而言，假设你想手动进行这些更改。Oracle 10g 的需求如表 7.3 所示。

### 表 7.3

Oracle 10g SUSE LINUX 内核需求

| 内核参数 | 所需最小值（单位取决于参数） | 描述 |
|---|---|---|
| `kernel.shmall` | `2097152` | 共享内存可用内存，以 4KB 块为单位 |
| `kernel.shmmax` | `2147483648` | 共享内存段的最大大小 |
| `kernel.shmni` | `4096` | 共享段的最大数量 |
| `kernel.sem` | `250 32000 100 128` | 信号量 |
| `fs.file-max` | `65536` | 内核分配的文件句柄最大数量 |
| `net.ipv4.ip_local_port_range` | `1024 65000` | 所需可用端口 |

### 注

调优内核是一项应谨慎进行的任务。所做的更改可能会产生无法运行的环境。互联网上有许多站点讨论 Linux 内核及其参数。访问以下其中一个以获取更多信息：

- http://www.suse.de/~agruen/kernel-doc/
- http://www.kernelnewbies.org/
- http://www.bb-zone.com/SLGFG/chapter4.html

你可以使用 sysctl 命令查询正在运行的内核当前使用的值。指定 -a 开关会列出所有参数。可以使用类似以下语法的命令检查每个单独参数：

```text
Athena:~ # sysctl kernel.shmmax
kernel.shmmax = 33554432
```

如你所见，此参数值远低于 Oracle 所需的最低值。要设置该值，请使用以下语法：

```text
Athena:~ # sysctl -w kernel.shmmax=2147483648
kernel.shmmax = 2147483648
```

此语法为内核参数设置新值并确认新值。
