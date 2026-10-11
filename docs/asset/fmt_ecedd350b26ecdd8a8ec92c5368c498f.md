
## 运行级别
| 运行级别 | 名称 | 描述 |
| :--- | :--- | :--- |
| 3 | 扩展多用户模式 (Extended Multi User) | 系统具有与多用户模式相同的功能，但启动了所有额外的网络服务（如 `NFS`）。 |
| 4 | 未使用 (Not used) | 通常不使用，但需要时可以定义。 |
| 5 | 图形模式 (Graphical Mode) | 系统具有与扩展多用户模式相同的功能，但启动了所有额外的网络服务（如 `NFS`）。 |
| 6 | 重启 (Reboot) | 用于重启系统的特殊运行级别。 |

## `/etc/initab` 文件

当 `init` 守护进程需要通过启动或停止守护进程来更改系统状态时，它会查询 `/etc/initab` 文件。在启动时将系统带到特定的运行级别时也会查询该文件。下所示为 `/etc/initab` 的示例：

特定运行级别下的系统。

`# 作者：Miquel van Moorenburg, <micquels@drinkel.nl.mugnet.org>`

由 `Marc Ewing` 和 `Donnie Barnes` 针对 `RHS Linux` 进行修改

```bash
# 默认运行级别。RHS 使用的运行级别为：
# 0 - 停止（不要将 initdefault 设置为此项）
# 1 - 单用户模式
# 2 - 多用户模式，不带 NFS（如果没有网络，则等同于 3）
# 3 - 完整多用户模式
## 4 - 未使用
## 5 - X11
# 6 - 重启（不要将 initdefault 设置为此项）
# id5:initdefault:
```

```bash
# 系统初始化。
si:sysinit:/etc/rc.d/rc.sysinit
10:0:wait:/etc/rc.d/rc 0
11:1:wait:/etc/rc.d/rc 1
12:2:wait:/etc/rc.d/rc 2
13:3:wait:/etc/rc.d/rc 3
14:4:wait:/etc/rc.d/rc 4
15:5:wait:/etc/rc.d/rc 5
16:6:wait:/etc/rc.d/rc 6
```

```bash
# 在每个运行级别都要运行的内容。
ud:once:/sbin/update
```

```bash
# 捕获 CTRL-ALT-DELETE
ca:ctrlaltld:/sbin/shutdown -t3 -r now
# 当我们的 UPS 报告断电时，假设我们还有几分钟电。
# 计划在 2 分钟后关机。
# 当然，这假设你已经安装了电源，且 UPS 连接并正常工作。
pf:powerfail:/sbin/shutdown -f - ++2 "Power Failure; System Shutting Down"
```

```bash
# 如果在关机启动前恢复恢复，
# 则取消它。
pr:12345:powerokwait:/sbin/shutdown -c "Power Restored;
Shutdown Cancelled"
```

# Linux 初始化 431

```bash
# 在标准运行级别下运行 getys
1:2345:respawn:/sbin/minget tty1
2:2345:respawn:/sbin/minget tty2
3:2345:respawn:/sbin/minget tty3
4:2345:respawn:/sbin/minget tty4
5:2345:respawn:/sbin/minget tty5
6:2345:respawn:/sbin/minget tty6

# 在运行级别 5 中运行 xdm
# xdm 现在是一个独立的服务
x5:respawn:/etc/X11/prefdm -nodaemon
[root@localhost]#
```

`/etc/initab` 文件中条目的格式如下：

`label : runlevel(s) : action : command`

`label` 只是一个标识符，允许 `init` 守护进程按字母顺序检查此文件；`runlevel` 指定了 `/etc/initab` 中的该行对应的运行级别；`command` 告诉 `init` 守护进程在执行运行级别时执行什么；而 `action` 告诉 `init` 守护进程如何执行该命令。

因此，`/etc/initab` 文件中的行 `id:5:default` 告诉 `init` 守护进程，运行级别 5 是启动初始化 Linux 系统时的默认运行级别。此外，`si:sysinit:/etc/rc.d/rc.sysinit` 行告诉 `init` 守护进程在系统初始化进入运行级别之前运行 `/etc/rc.d/rc.sysinit`。该程序初始化系统的硬件组件，设置 `PATH` 和 `HOSTNAME` 等环境变量，检查文件系统并执行守护进程加载所需的任务。`/etc/rc.d/rc.sysinit` 程序的输出会在图 9-11 所示的系统启动期间显示在终端屏幕。

![](img/6148a12ef656b46c092b21c2e023d928_448_0.png)

图 9-11 由 `/etc/rc.d/rc.sysinit` 引起的系统启动

# 432 第9 章 系统初始化

由于默认运行级别是单用户，因此在接下来看到的 `/etc/initab` 文件中，只有 `5:wait:/etc/rc.d/rc 5` 这一行会被执行。该行执行 `/etc/rc.d/rc 5` 命令并等待其完成后再处理 `/etc/initab` 文件的其余部分。`/etc/rc.d/rc5` 命令执行 `/etc/rc.d/rc5d/` 目录下所有以 `S` 或 `K` 开头的文件。该目录中的每个文件都是启动特定守护进程的符号链接，且这些每个文件都按字母顺序执行；`S` 或 `K` 分别表示进入此运行级别时启动（`Start`）或杀死（`Kill`）该守护进程。`/etc/rc.d/rc5d` 的一些示例内容如下：

```bash
[root@localhost ~#] ls /etc/rc.d/rc5d
K03rhns K34yppavassd K65krb524 S06reconfig S56kinet
K05ind K35dhchpd K65krb56d S08ipchains K60lpd
K09kyjunker K35mb 74ntpt S08iptables S80ends
K12mysqld K35ycner 74ups S09isdn S83isci
K15httpd K04mars-nwe 74pserv S10network S90crond
K15postgrsl K45paratch 74ypb S12log S90ifs
K16rarpd K45named 75xted S13portmap S90xf
K20bootparam K44radsv 84bbkg S17keytable S95acron
K20infns K50amnd 84ospf S20random S95at
K20rastad K50tux 84ripid S99ifconf
K20usersder K65rooted 84ripng S26amapd S99local
K20rwalld K61init 85zebra S28autofs S99line
K22squid K65admin 89cm52 S85ccmia
K28amd K25sshd 96irda S55sshd
K30cmerv K65prop S50kudu S56rawdevices
[root@localhost ~#]
```

从上述输出可以看出，`init` 守护进程进入此运行级别时启动 `cron` 守护进程（`S90crond`），如果内存中存在则杀死 `ldap` 守护进程（`K61ldap`）。此外，目录中的文件按字母顺序执行；文件 `65ident` 会在文件 `65admin` 之前执行。记住，运行级别 1（单用户模式）仅包含用户登录和执行系统任务的守护进程；如果你告诉 `init` 守护进程切换到运行级别 1，它将在 `/etc/initab` 中找到相应的条目（`1:1:wait:/etc/rc.d/rc 1`），并执行 `/etc/rc.d/rc1` 中以 `S` 或 `K` 开头的文件。由于单用户模式下启动的守护进程很少，此目录中的大多数文件以 `K` 开头：

```bash
[root@localhost ~#] ls /etc/rc.d/rc1
K00linuxconf K20rastad K45named K74apd S88kyl
K03rhns K20usersder K46radv T74tcp K89cm52
K05anacon K20rwalld K50nmp 74ups S90network
K05ad K20rwhod S50tux
05ind K25squid S5xinetd K74ypferd K92ipchains
K09junker K25sshd K54xpe K75gated K92iptables
```

# Linux 初始化 433

| `K1wine` | `K28amd` | `K55routed` | `K75nets` | `K95kudu` |
| :--- | :--- | :--- | :--- | :--- |
| `K10xfs` | `K30mcserv` | `K60crond` | `K80random` | `K95reconfig` |
