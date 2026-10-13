
# 第一部分：红帽 Linux 系统和网络管理

## 列表 5-12 (继续)

| | | | | | |
|---|---|---|---|---|---|
| K09junkbuster K20wall K45arp K65admin K75netfs K92ipchains |
| K10wine K20whod K45named K65rop K80random K92ipmd |
| K10xfs K25squid K46radvd K65rb24bgpd K95kuzdu |
| K12mysqld K25ssnd K50osmmd K65xbdc K84ospifd K95reconfig |
| K15pgpm K28and K50utux K72autofs K84ripid K96rida |
| K15htypd K30cmser K50xineted K73ypbind S00killall |
| K15postgreg K30sendmail K54pxpe K84ripngd S01reboot |

如果你需要重启一个从目录启动的服务，正确且简单的方法是带有 `restart` 参数运行其启动脚本。此过程可确保在服务重新启动时遵循所有正确的步骤（读取配置文件等）。因此，要重启 `syslog`，请从 `rc` 目录运行以下命令：

```
[root@buffy rc.d]$ ./syslog restart

Shutting down kernel logger: [ OK ]

Shutting down system logger: [ OK ]

Starting system logger: [ OK ]

Starting kernel logger: [ OK ]
```

## 使用 chkconfig 管理 rc 脚本

红帽 7.2 自带有一个名为 `chkconfig` 的有用工具。它可以帮助系统管理员管理 `rc` 服务和 `xinetd` 配置文件，无需直接操作它们。它的灵感源于 IRIX 操作系统包含的 `chkconfig` 命令。

输入 `chkconfig --list` 查看 `chkconfig` 已知的所有服务，以及它们在每个运行级别是停止还是启动状态。下面的列表显示了一个简化的示例。`chkconfig` 的输出可能比这长得多，因此可以使用管道过滤。

第一列是已安装服务的名称。接下来的七列代表运行级别，并告诉您服务在该运行级别下是开启还是关闭。

由于在提取 `chkconfig` 输出的系统中启动了 `xinetd`，因此在 `chkconfig` 输出的结尾是 `xinetd` 启动的服务配置开机启动的列表。该列表是简化的，因为有很多服务可以从 `xinetd` 启动，没有显示显示所有。

列表 5-13 显示了 `chkconfig` 如何成为处理所有网络服务并控制哪些服务在开机时启动的有效工具。`chkconfig --list` 的输出：

# 第 5 章：红帽系统配置文件

### 列表 5-13：chkconfig 的输出

| | 0 | 1 | 2 | 3 | 4 | 5 | 6 |
|---|---|---|---|---|---|---|
| atd | off | off | off | on | on | off | off |
| whod | off | off | off | off | off | off | off |
| keytable | off | off | on | on | on | off | off |
| nscd | off | off | off | off | off | off | off |
| syslog | off | off | on | on | on | off | off |
| gpm | off | off | on | off | off | off | off |
| kudzu | off | off | off | on | on | off | off |
| kdate | off | off | off | off | off | off | off |
| lpd | off | off | off | on | on | off | off |
| autofs | off | off | off | off | off | off | off |
| sendmail | off | off | off | off | off | off | off |
| rhnsd | off | off | off | on | on | off | off |
| netfs | off | off | off | off | off | off | off |
| network | off | off | on | on | on | off | off |

# 第一部分：红帽 Linux 系统与网络管理定义

要使用 `chkconfig` 关闭或开启一项服务，请使用以下语法：

```
chkconfig servicename off|on|reset
```

因此，要关闭之前开启的 ftp 守护进程，输入：

```
chkconfig wu-ftptd off
```

要开启 `xinetd`，输入：

```
chkconfig xinetd on
```
