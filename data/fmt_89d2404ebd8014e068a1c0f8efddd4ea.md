
# at `<time>` input `<Ctrl-D>` # 在 `<time>` 启动一个任务
# echo "shutdown -Fr" | at 11 pm # 在下一个周六晚上 11:00 重启系统
# atq `<username>` # 不要忘记 `echo`，否则系统
# at -r `<jobnumber>` # 将从当前 shell 立即重启
# 删除一个任务

如果需要更复杂的批处理调度系统，您可以使用打印机子系统创建一个“批处理队列”。

### 管理 cron 活动

在活跃的批处理环境中，您可能希望对 `cron` 调度设置一些限制。`/usr/adm/cron/queuedefs` 文件可以配置为限制每种事件类型的并发任务数量，设置默认的 `nice` 值，并设置重试限制。事件控制按行列在 `queuedefs` 文件中。这里列出了 `queuedefs` 文件的一个示例：

```
# cron values for each queue of batch jobs:
#    queue.xxjxxnxx
#
# queues:
# a - sh jobs       d - sync event
# b - batch jobs    e - ksh jobs
# c - cron event          f - csh jobs
# xxj - maximum number of jobs in this queue (default 100)
# xxn - nice value at which these jobs will run at (default 2)
# xxw - wait time till next execution attempt (default 60 seconds)
#
#
# here is an example of a low priority (nice 20), 50 entry batch queue
# b.50j20n60w
```

`queue.defs` 文件随附时为空。所有事件类型的默认值（如表 21-4 所示）支持在 `nice` 值为 2 的情况下运行 100 个并发任务，重试限制为 60 秒。这是一个简单的 `queue.defs` 条目：

`c.2j2n90w` — 两个 `crontab` 任务，`nice` 值为 2，每 90 秒重试一次

## 系统资源控制器

AIX 提供了一种机制，用于控制和作为一个单元集体功能的一组程序。该机制称为 `System Resource Controller`（`SRC`，系统资源控制器）。`SRC` 提供简单的命令接口，以显示状态、刷新、启动和停止作为单一实体的系统服务。这些接口降低了管理组成特定服务的所有守护程序和程序的运营和管理复杂性。

组成 `SRC` 服务单元的 `program` 集合称为子系统。组成子系统的守护程序称为 `sub-servers`（子服务器）。子系统可以按其提供的整体服务进行分组，并识别为子系统组。例如，`fpfd` 守护程序是 `inetsd` 子系统的 `sub-server`（子服务器）。`inetsd` 子系统是 TCP/IP 子系统组的成员。`SRC` 允许操作员或管理员在 `sub-server`、子系统或子系统组级别上操作服务。

**表 21-4.**

`queue.defs` 事件类型

| 类型 | 事件类别 |
| :--- | :--- |
| a | at 事件 |
| b | 批处理事件 |
| c | crontab 事件 |
| d | 同步事件 |
| e | ksh 事件 |
| f | csh 事件 |

## SRC 组件

总体而言，`SRC` 由 `srcmstr` 守护进程提供。`srcmstr` 守护进程在系统启动时通过 `/etc/inittab` 文件中的条目启动。

```
srcmstr:23456789:repassw:/usr/sbin/srcmstr    # 系统资源控制器
```

`srcmstr` 守护进程根据 ODM 对象类 `/etc/objrepos/(SRCobjsysy_SRCNotify)` 中的定义识别子系统组件。子系统和子服务（subserver）的配置信息通过使用 `[mk.ch.rm]ssys` 和 `[mk.ch.rm]ssver` 命令进行管理。在大多数情况下，子系统和子服务在每个产品安装时就已经预定义好了，因此你几乎不需要在这个层级进行操作。

一旦子系统组、子系统或子服务（subservet）配置到 ODM 中，就可以使用以下命令进行操作：

- `startsrc` 启动子系统
- `stopsrc` 停止子系统
- `refresh` 重新启动或刷新子系统
- `trace -a, trcon, troff, 和 trestop` 开启/关闭子系统的跟踪
- `lsrsrc` 显示子系统状态

在 `srcmstr` 加载后，可以在系统启动时通过调用 `startsrec` 命令来启动子系统，该命令可以作为启动脚本的一部分或直接通过 `/etc/initab` 执行。一些 SRC 命令示例包括：

- `# startsrec -g tcip` 启动 TCPIP 子系统组
- `# refresh -g nfs` 刷新 NFS 子系统组
- `# stopsrc -s qdaem` 停止 `qdaemon` 子服务

要显示所有已定义子系统的状态，请使用 `lsrc` 命令。请注意，也可以通过使用 `smitty subsys` 和 `smitty subservlet` SMIIT 快速路径或通过基于 Web 的系统管理器来调用子服务（subservet）控制。

```
$ lsrsrc -a

Subsystem      Group    PID    Status
syslog          ras      3670   active
sendmail        mail     4144   active
portmap         portmap  3878   active
inetd           tcip     4388   active
xntpd           tcip     4644   active
snmpd           tcip     5160   active
dpid2           tcip     4904   active
hostmibd        tcip     5418   active
qdaemon         spooler  7224   active
writeserv       spooler  7484   active
dtsrc                 9550   active
ctsrc           rcst     11106  active
IBM_ERRM        rcst_rm  11876  active
i4lmd           iforls   12128  active
IBM_AuditRM     rcst_rm  11362  active
bioc            nfs            active
nfsd            nfs            active
rpc_statd       nfs            active
rpc_lockd       nfs            active
rpc_mountd      nfs            active
lpd             spooler        active
clvm                     inactive
gated           tcpip          inactive
named           tcpip          inactive
routed          tcpip          inactive
rwhod           tcpip          inactive
iptrace         tcpip          inactive
timed           tcpip          inactive
dhcpd           tcpip          inactive
dhcpsd          tcpip          inactive
dhcprd          tcpip          inactive
ndpd-host       tcpip          inactive
ndpd-router     tcpip          inactive
tftpd           tcpip          inactive
mro                        inactive
mrou            tcpip          inactive
rvpd            qos            inactive
policyd         qos            inactive
ilb             iforl          inactive
glb             iforl          inactive
i4lmd           iforl          inactive
i4glb           iforl          inactive
i4gd            iforl          inactive
wsremeserve     tcpip          inactive
ppcontrol       uucp           inactive
pxed            tcpip          inactive
bind            tcpip          inactive
ypserv          typ            inactive
ypupdated       typ            inactive
ypasswd         typ            inactive
dfcp            tcpip          inactive
i4cmmgr         iforl          inactive
seclldapntd     seclad         inactive
automountd      autofs         inoperative
keyserv         keyserv        inoperative
ypbind          yp             inoperative
nis_cachemgr    nisplus        inoperative
rpc.nisd        nisplus        inoperative
rpc.nispassword nisplus        inoperative
```

## 检查清单

以下是进程管理的关键要点检查清单：

- 一个进程由正在执行的程序及其地址空间组成。每个进程由一个称为进程标识符（PID）的正整数命名。
- 你可以使用 `SMIT` 快速路径 `smitty system` 并选择“更改/显示操作系统特性”来设置每个用户的最大进程数。
- 使用 `ps` 命令查看在系统上运行的进程。
- `nice` 值是一个整数，表示进程之间的粗略优先级差异。数字越 `大`，优先级越 `低`。
- 只有超级用户才能提高 `nice` 优先级。在启动进程时，可以使用 `nice` 命令从命令行设置 `nice` 值。
- 进程所有者和超级用户可以使用 `renice` 命令修改现有进程的 `nice` 值。

![](img/82f851021955589d82b22750fb3b1646_493_0.png)

## 第 22 章

## 系统会计

让我看看……那是 12 个 CPU 上 22 分钟的时间，3GB 的磁盘空间，以及 3 小时的连接时间。那是现金还是支票？生活中没有什么东西是免费的！尤其是如果你在一个大型高性能计算机设施上处理数字时更是如此。即使你不对系统资源进行分摊费用，定期监控利用率也是一个好主意。通过收集会计数据，你可以获得系统使用情况的合理概况。哪些是主要的资源消耗者？你多久需要那额外的 10GB 磁盘空间？也许你需要向上级部门证明资源的需求。

AIX 会计系统采用 System V 风格。然而，有一组标准的 BSD 会计系统管理命令被附加到了 System V 环境中。编写自己的会计程序和脚本的站点会发现，AIX 提供了有助于将现有系统从其他 UNIX 环境移植过来的工具和会计数据格式。对于不那么愿意折腾的用户，AIX 提供了管理系统会计数据所需的所有命令和脚本。会计系统基于一组三个组件：

- 数据收集
- 管理和报告命令
- 定期数据管理脚本

当启用会计时，数据收集会自动进行。管理和命令使您可以启动和停止会计系统，管理数据文件，并生成报告。定期数据管理脚本由 `cron` 调用（参见后面部分，“Crontab 条目”），以自动关闭数据并生成一般摘要信息。

### 数据收集

数据收集从系统会计开启时开始，在关闭时停止。AIX 采样并记录系统中每个用户的进程使用率和会话数据。收集的信息代表连接时间、进程资源、命令、磁盘使用率和打印队列利用率。

### 连接时间

连接时间数据累积在 `/var/adm/wtmp` 和 `/etc/utmp` 文件中。每次登录 AIX 时，登录过程都会向 `wtmp` 和 `utmp` 写入一条记录。数据指示用户名、日期、时间、端口和连接地址。`init` 进程在你退出系统时写入类似的记录。这些数据代表你与系统的连接持续时间。

`rsh` 和 X11 客户端的组合可能会绕过存在 X11 使用环境中的连接数据会计。`xterm` 终端仿真客户端提供了一个标志，指示是否应写入 `/etc/utmp` 记录。`xterm` 终端仿真也有损坏 `/etc/utmp` 文件的历史记录。你可能希望使用一个封装命令，强制远程客户端应用程序的用户遵守连接会计。

`wtmp` 和 `utmp` 文件中的损坏或错误可以通过使用 `fwtmp` 命令将目标二进制文件转换为临时 ASCII 文件，手动编辑可疑条目，然后将临时文件转换回二进制目标文件来修复。新文件将覆盖在此编辑过程中记录的连接数据。

```
# last -f /var/adm/wtmp | more # ← 查找问题数据字段
# /usr/sbin/acct/fwtmp < /var/adm/wtmp > temp.file ← 创建 ASCII 文件
# vi temp.file ← 编辑问题字段
# /usr/sbin/acct/fwtmp -ic < temp.file > wtmp.new ← 创建二进制文件
# last -f wtmp.new | more ← 查看修正后的字段
# cp -pi wtmp.new /var/adm/wtmp ← 覆盖到问题目标
```

### 进程资源使用

操作系统为每个运行的进程记录的资源利用率信息在进程退出时记录在 `/var/adm/pacct` 文件中。对于未退出的进程不记录任何信息。进程会计记录指示 UID、GID、用户名、经过的墙钟时间、CPU 时间、内存使用、字符 I/O 总量和磁盘块 I/O 总量。

### 命令使用

进程数据的一个良好副作用是命令和应用程序使用的审计跟踪。此数据提供了应用程序使用的概况，并可能有助于跟踪安全问题。请注意，经验丰富的黑客在离开现场之前往往会修正会计信息。有关安全审计详情，请参阅第 23 章。

### 磁盘使用

您可以定期收集系统的磁盘使用信息并将其存储在 `/var/adm/dfm` 文件中。使用 `findfs` 脚本收集磁盘使用数据可能会给系统带来负载，因此请在非高峰时段安排 `cron` 任务。DIX 根据用户在文件系统中拥有的文件以及他们可能创建的文件链接，将磁盘使用数据分配给用户。文件的用量统计在拥有该文件链接的用户之间均匀分配。

通过磁盘配额系统，还可以跟踪磁盘使用情况并限制用户和/或组的使用限制。有关磁盘配额系统的详细信息，请参阅第 20 章。

## 打印使用情况

`enq` 命令和 `qdaemon` 进程会记录打印队列系统的利用率统计信息。`enq` 命令会为每个它处理的打印作业写入一条记录。该记录指示打印作业的所有者、作业编号和文件名。当文件被打印时，`qdaemon` 会写入另一条记录，其中包含上述信息以及已打印的页数。对于 PostScript 队列，有公有领域的后端可以提供用于 PostScript 转换和属性的计量记录。

## 计量文件

计量记录存储于位于 `/var/adm` 目录中的一组文件中。表 22-1 列出了文件及收集的数据。

## 计量配置

如果 `startup` 脚本在 `adm` 用户账户下运行，并且先于其他任何用户运行（参见本章“启动和停止计量”一节），计量系统将在需要时创建大多数数据收集文件。但情况并非总是如此，因此你需要知道如何手动更改或创建这些文件。这应以 `adm` 权限执行，但可能需要以 `root` 身份执行以纠正文件所有权。在浏览本配置部分时，请确保 `bos.acct` 文件集已安装。有关安装缺失文件集的详细信息，请参阅第 6 章。

```
# ls1pp -1 bos.acct
```

## 设置收集文件

即使我记得从 `adm` 用户 shell 正确启动计量系统，我通常仍需要修复或创建至少一个数据收集文件（表 22-1）。最常见的需要修复的问题是收集进程数据的 `pacct` 文件的权限。触及文件名或运行 `nulladm` 可以创建缺失的文件存根。

| 文件名 | 收集的数据 |
| :--- | :--- |
| `pacct` | 活动进程数据 |
| `$pacct_.cmd` | 每日活动进程数据 (ruacct) |
| `qacct` | 打印使用数据 |
| `utmp` | 连接会话数据 |
| `dtmp` | 磁盘使用数据 |
