

# 第3章 启动与关机

```
logfile /var/svc/log/network-ssh:default.log
restarter /var/svc/svc/starter:default
contract_id 65
dependency require_all/none svc/system/filesystem/local (online)
dependency optional_all/none svc/system/filesystem/autofs (online)
dependency require_all/none svc/network/loopback (online)
dependency require_all/none svc/network/physical (online)
dependency require_all/none svc/system/cryptos (online)
dependency require_all/none svc/network/utmp (online)
dependency require_all/none=/restart file:/localhost/etc/ssh/ssh_config (online)
```

此命令行使用了完整的 MRI，但该服务只有一个实例，通过 `svcs -1 ssh` 即可查看。该状态可以取以下值：

- + online - enabled - 已启用并成功启动
- disabled - 未启用且未运行
- degraded - 已启用但在带有限制的情况下运行
- legacy_run - 正在运行；使用少数尚未转换为 SMF 且仍在使用传统 init.d 脚本的服务
- uninitialized - 正在启动并读取配置
- maintenance - 报告需要管理员注意的错误
- offline - 已离线，因为服务正在等待未满足的依赖或由于某些原因无法启动

除了当前的服务状态外，`svcs -l` 会列出服务的日志位置、依赖关系和其他基本要素。

依赖关系允许在服务之间指定任意复杂的关系。这种机制本质上取代了传统 init 系统使用的数字启动脚本，一个前缀为 S20 的脚本会在前缀为 S90 的脚本之前运行。

在上面的示例，SSH 需要本地文件系统、网络接口、加密服务、utmp 以及 `ssh_config` 文件的存在。系统自动挂载（automounter）被标记为可选依赖项；如果自动挂载故意离线（由管理员设置）或处于在线运行状态，SSH 将会运行。

`svcadm` 命令用于更改服务的状态。要禁用 SSH 服务（不要尝试远程此操作！），请使用：

```
solaris$ svcadm disable ssh
```

此示例使用了 SSH 的短 MRI，因为它是无歧义的。禁用是一个持久更改；使用 `svcadm -t` 可以临时禁用 SSH。

在底层，SMP 通过称为 manifest（清单）和 profile（配置文件）的 XML 文件配置服务。manifest 描述了服务的属性，例如其依赖关系以及启动和停止它的指令。manifest 文件存储在 `/var/svc/manifest` 目录下。每个服务实例都有自己的 manifest。

# 一个勇敢的新世界：使用 SMF 启动

manifest 文件中的 `exec_method` 行通常指向启动和停止服务的脚本，类似于 init.d 系统中使用的脚本。例如，SSH 守护进程的启动过程在 `/var/svc/manifest/ssh.xml` 中被定义为：

```xml
<exec_method
type='method'
name='start'
exec='/lib/svc/method/sshd start'
timeout_seconds='60'>
```

被引用的 `/lib/svc/method/sshd` 脚本启动服务。它看起来很像一个可能存在于 `/etc/rc.d` 中的脚本——事过迁变，其本质依然不变。

服务的 profile 文件决定了实例是启用还是禁用。profile 存储在 `/var/svc/profile` 中。

服务的持久化配置实际上存储在 `/etc/repository.db` 中的 SQLite 数据库中。因此，你不应该直接修改 XML 文件的内容。使用 `inetadm` 配合 `svcfcg` 命令可以管理 manifest 和 profile。可以通过 `svcfcg`、`inetadm` 和 `svc.config` 的页面获取更多信息。

SMF 最受关注的功能之一是“重启”（restarts）概念，这是 Solaris 声受瞩目的“预测性自愈”技术的一部分。通过思考仔细定义的依赖系统，SMF 认为可以确定服务死亡并在并在适当的情况下重启。服务失败的原因可能是软件漏洞、硬件问题，甚至是管理员错误。指定的 SMF 重启进程与内核紧密结合，会自动执行相应的恢复操作。

# 一个勇敢的新世界：使用 SMF 启动

Solaris 10 或更高版本系统上的启动过程与传统的自引导非常相似。SPARC 启动与 Intel 系统的启动略有不同，通用概念是底层固件（SPARC 为 PROM，Intel 为 BIOS）读取启动配置，从而加载操作系统内核。

内核扫描 `/etc/system` 以查找可加载模块，然后启动 `init`，`init` 会立即启动 `svc.startd` 进程。`svc.startd` 是 SMF 主启动器，负责根据 SMF 配置仓库中定义的依赖顺序启动服务。

遗憾的是，旧版本 Solaris 的运行级别系统和 init 脚本并没有完全消失。某些服务（在 `svcs -a` 输出中显示为 `legacy-run` 的那些）仍然依赖于 `/etc/rc.d` 目录下的脚本。SMF 里程碑与传统运行级别之间的冲突留下了许多碎片。

# 第3章 启动与关机

为了避免被划伤手指，请记住以下几点：

- 处于 `legacy-run` 状态的服务是从 rc 脚本启动的。
- Solaris 定义了八个运行级别。详情请 init 主页。
- 要更改运行级别，请使用 `init n`，其中 `n` 是新的运行级别。不要尝试使用 SMF 来更改里程碑。

# 重启与关机

传统版本的 `shutdown` 就像是解构。现代系统已经变得更好。`shutdown` 命令是最安全的。

- 例如，`shutdown` 在 9:30 关机以进行计划维护。

```
$ shutdown -h 09:30 "进行计划维护。"
预计停机1 小时。
```

- 还可以指定相对关机时间。例如， 15 分钟后关机：

```
$ shutdown -h +15 "进行紧急维修。"
```

服务的持久化配置实际上存储在 `/etc/repository.db` 中的 SQLite 数据库中。因此，你不应该直接修改 XML 文件的内容。使用 `inetadm` 配合 `svcfcg` 命令可以管理 manifest 和 profile。可以通过 `svcfcg`、`inetadm` 和 `svc.config` 的页面获取更多信息。

SMF 最受关注的功能之一是“重启”（restarts）概念，这是 Solaris 声受瞩目的“预测性自愈”技术的一部分。通过思考仔细定义的依赖系统，SMF 认为可以确定服务死亡并在并在适当的情况下重启。服务失败的原因可能是软件漏洞、硬件问题，甚至是管理员错误。指定的 SMF 重启进程与内核紧密结合，会自动执行相应的恢复操作。

# 关机：最安全的方法

`shutdown` 命令是关机最安全的方法。`shutdown -h` 也可以独立使用。它记录日志、停止运行的进程并关闭系统同步调用，等待文件系统写入并停止系统。

