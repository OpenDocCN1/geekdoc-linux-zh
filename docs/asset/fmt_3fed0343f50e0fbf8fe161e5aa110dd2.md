
系统首次启动时，`init` 启动 `inittab` 文件中标记为 `sysinit` 的所有进程。`/etc/inittab` 中的 `initdefault` 条目标识默认运行级别。在此示例中，默认值为运行级别 3（具有网络文件共享的多用户模式）。`init` 守护进程运行与此运行级别关联的每个进程（每个条目在运行级别字段中有 3）。每个进程都使用 `action` 字段中的条目运行。`action` 字段可以具有以下值之一：

- `powerfail` 系统已收到电源故障信号。
- `wait` 等待命令完成。
- `respawn` 重新启动命令。

### /etc/bcheckrc

由 `/etc/inittab` 文件设置的第一个脚本是 `/etc/bcheckrc` 脚本，它准备根文件系统和其他关键文件系统，例如 `/usr`。Solaris 使用存储在硬盘上的状态标志来记录文件系统的状况。该标志由 `/etc/bcheckrc` 脚本在启动期间检查，以确定文件系统的状态——干净或不干净。文件系统及其状态在第 3 章“文件系统简介”中讨论。

> 注。许多 Solaris 启动脚本可以通过其“rc”前缀或后缀来识别，这意味着“运行控制”。

### rc 脚本

对于每个 `init` 状态，都有相应的 `rc` 脚本系列，位于 `/sbin` 目录中，用于控制每个 `init` 状态：

- `rc0`
- `rc1`
- `rc2`
- `rc3`
- `rc5`
- `rc6`
- `rcS`

对于 `/sbin` 目录中的每个 `rc` 脚本，都有一个对应的目录名为 `/etc/rcn.d`，其中包含用于该运行级别执行各种操作的脚本。例如，`/etc/rc2.d` 包含用于启动和停止运行级别 2 进程的文件。`rc` 脚本按数字顺序运行，直到达到所需的运行级别；例如，要达到运行级别 3，将运行 `/sbin/rc1`、`/sbin/rc2` 和 `/sbin/rc3`。

所有运行控制脚本也位于 `/etc/init.d` 目录中。这些文件链接到 `/etc/rc*.d` 目录中的相应运行控制脚本。

> 注。在其他 UNIX 系统上，启动脚本有时位于 `/sbin/rc*.d`，有时位于 `/etc/rc*.d` 目录中。Solaris 中放置了链接，以便习惯于其他 UNIX 变体（HP-UX、SunOS 等）的用户可以轻松找到启动文件。此外，他们可能移植的任何引用这些启动文件的脚本都无需修改即可兼容。

以下是位于 `/etc/rc2.d` 中的脚本列表：

```
ls /etc/rc2.d

sun% ls /etc/rc2.d
K20lp          S21perf        S72netsvc      S99bdconfig
K60nfs.server  S30sysid.net   S73nfs.client  S90xtl
K65nfs.client  S47sspp        S74autofs      S91gsconfig
K92volmgt      S69inet        S74syslog      S91gtconfig
README         S70uucp        S75cron        S91leconfig
S01MOUNTSYS    S71rpc         S80PRESERVE    S92rtvc.config
S05RMTPFILES   S71sysid.sys   S80lp          S92volmgt
S18setuname    S72autoinstall S88sendmail    S99audit
S20sysetup
```

`/etc/rcn.d` 脚本始终按 ASCII 排序顺序运行。脚本名称的形式为 `[K,S][0-9][0-9][A-Z]`

以 `K` 开头的 文件用于终止（kill）某些系统进程。以 `S` 开头的 文件用于启动系统进程。每个运行控制级脚本的操作总结如下。

### /sbin/rc0 脚本

- 停止系统服务和守护进程
- 终止所有正在运行的进程
- 卸载所有文件系统

`/sbin/rc1` 脚本运行 `/etc/rc1.d` 脚本，并

- 停止系统服务和守护进程
- 终止所有正在运行的进程
- 卸载所有文件系统
- 将系统以单用户模式启动

> TIP. 使用 `init 1` 运行级别执行系统管理任务，以确保其他用户无法登录并访问系统。

`/sbin/rc2` 脚本设置 `TIMEZONE` 变量，运行 `/etc/rc2.d` 脚本，并

- 挂载所有文件系统
- 如果至少有一个文件系统使用 `quota` 选项挂载，则启用磁盘配额
- 在 `/usr/preserve` 中保存编辑器临时文件
- 删除 `/tmp` 目录中的任何文件
- 为新磁盘创建 `/dev` 中的设备条目（仅当以 `boot -r` 运行 时）
- 打印系统配置（默认不保存核心文件）
- 配置系统记账
- 配置默认路由器
- 设置 NIS 域
- 设置 `ifconfig` 网络掩码
- 启动 `inetd`
- 启动 `named`，如果适用
- 启动 `rpcbind`
- 启动 Kerberos 客户端守护进程，`kerbd`
- 启动 NIS 守护进程（`ypbind`）和 NIS+ 守护进程（`rpc.nisd`），如果适用
- 启动 `keyserv`
- 启动 `statd`、`lockd`
- 挂载所有 NFS 条目
- 启动 `automount`
- 启动 `cron`
- 启动 LP 守护进程
- 启动 `sendmail` 守护进程

`/sbin/rc3` 脚本运行 `/etc/rc3.d` 脚本，并

- 清理 `sharetab`
- 启动 `nfssd`
- 启动 `mountd`
- 如果是引导服务器，则启动 `rarpd` 和 `rpc.bootparamd`

`/sbin/rc5` 脚本运行 `/etc/rc0.d` 脚本，并

- 终止打印机守护进程
- 卸载本地文件系统
- 终止 `syslog` 守护进程
- 卸载远程文件系统
- 停止 NFS 服务
- 停止 NIS 服务
- 停止 RPC 服务
- 停止 `cron` 服务
- 停止 NFS 客户端服务
- 终止所有活动进程
- 启动交互式引导

`/sbin/rc6` 脚本运行 `/etc/rc0.d/K*` 并

- 终止所有活动进程
- 卸载文件系统
- 运行 `/etc/inittab` 中的 `initdefault` 条目

`/sbin/rcS` 脚本运行 `/etc/rcS.d` 脚本以将系统启动到单用户模式，并

- 建立最小网络
- 如有必要，挂载 `/usr`
- 设置系统名称
- 检查 `/` 和 `/usr` 文件系统
- 如有必要，检查并挂载 `/usr/kvm` 文件系统
- 挂载伪文件系统（`/proc` 和 `/dev/fd`）
- 对于重新配置引导，重建设备条目
- 检查并挂载在单用户模式下要挂载的其他文件系统

运行级别 `init S` 与运行级别 1 相似，只是所有文件系统都会被挂载并且可访问。

### 使用运行控制脚本停止或启动服务

拥有每个 `init` 的单独脚本的优势在于，您可以在不重新启动或更改 `init` 状态的情况下单独运行这些脚本来关闭 Solaris 中的进程。

例如，您可以通过键入 `/etc/init.d/nfs.server stop` 并按 Enter 来关闭 NFS 服务器功能。在更改系统配置后，您可以通过键入 `/etc/init.d/nfs.server start` 并按 Enter 来重新启动该功能。

### 向运行控制目录添加脚本

如果要添加脚本，请将脚本放在 `/etc/init.d` 目录中，并在适当的 `rc*.d` 目录中创建链接。为新脚本分配适当的编号和名称，以便按正确顺序运行。

*TIP.* 如果您不希望某个脚本在进入相应的 `init` 状态时运行，请将大写前缀（`S` 或 `K`）更改为小写（`s` 或 `k`）。只有具有大写前缀的文件才会被运行。例如，将 `S99mount` 更改为 `s99mount` 以禁用该脚本。

### 系统关机

Solaris 设计为每周 7 天、每天 24 小时连续运行。然而，有时您需要关闭系统以执行管理任务。另一些时候，应用程序可能会导致系统出现问题，操作系统必须停止以终止失控进程，然后重新启动。您可以使用各种 UNIX 命令以多种方式关闭系统。对于 Solaris 来说，有序地关闭操作系统非常重要。当系统启动时，启动了多个进程，必须在关闭系统电源之前关闭它们。此外，信息已缓存在内存中，尚未写入磁盘。关闭 Solaris 的过程涉及关闭进程并将数据从内存刷新到磁盘。请记住，不当关闭系统可能会导致数据丢失并有损坏文件系统的风险。

*TIP.* 为避免在停电期间系统被不当关闭，请使用能够在电源关闭前关闭系统的不间断电源（UPS）。

### 关闭系统的命令

准备关闭系统时，您需要确定以下哪个命令适合系统和手头的任务：

- `/usr/sbin/shutdown`
- `/sbin/init`
- `/usr/sbin/halt`
- `/usr/sbin/reboot`
