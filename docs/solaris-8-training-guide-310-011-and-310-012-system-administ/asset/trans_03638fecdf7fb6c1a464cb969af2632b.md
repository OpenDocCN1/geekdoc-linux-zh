
## 表 1.3 继续
### 定义的八种系统运行状态

| 初始化状态 | 使用时机 |
|---|---|
| 1 | 单用户（系统管理员）状态。此运行级别用于系统管理员执行管理任务且不希望其他用户登录系统时，例如在执行备份和对当前未被登录用户使用的文件系统进行文件系统检查时。 |
| 2 | 用于正常操作，当不需要共享本地文件系统时。多个用户可以访问系统和整个文件系统。所有守护进程都在运行，除了 NFS 服务器和 syslog。使用此运行级别以确保远程主机无法挂载本地文件系统（有关 NFS 的更多信息，请阅读第 17 章“ NFS 环境”）或当您希望 syslogd 守护进程处于非活动状态时。 |
| 3 | 用于正常操作，NFS 资源共享可用。这是大多数系统上的正常运行级别。 |
| 4 | 替代多用户状态（当前未使用）。 |
| 5 | 关机状态。为关闭操作系统以便安全地关闭系统电源。所有用户都已从系统注销，并且操作系统服务以有序的方式停止。完成后，可以安全地关闭系统和所有外设的电源。如果系统硬件支持，系统电源将自动关闭。 |
| 6 | 将系统关闭到运行级别 0，然后重新启动到多用户级别（或 inittab 文件中默认的任何级别）。 |

> 注意
在 Solaris 的早期版本中，此进程称为 swapper，并在 Solaris 8 中重命名为 sched。

## Swapper

内核的第一个任务是启动 swapper 进程。swapper 进程是内核中调度所有其他进程的部分。swapper 的进程 ID 为 0，名为 sched。它的第一个工作是启动 init 进程。

## INIT 阶段

/sbin/init 命令根据 /etc/inittab 中的指示生成进程以设置系统。init 进程是所有其他进程的父进程。它检查 /etc/inittab 文件的内容以确定启动其他进程的顺序以及当其中一个进程结束时该做什么。/etc/inittab 文件中的每个条目都有以下字段：

```
id:runlevel:action:process
```

表 1.4 提供了每个字段的更详细描述。

## 表 1.4
### INITTAB 文件中的字段

| 字段 | 描述 |
| --- | --- |
| id | 唯一标识符 |
| runlevel | 运行级别 |
| action | 进程的运行方式 |
| process | 要执行的命令名称 |

以下示例显示默认的 /etc/inittab 文件：

```
ap::sysinit:/sbin/autopush -f /etc/iu.ap
ap::sysinit:/sbin/soconfig -f /etc/sock2path
fs::sysinit:/sbin/rcS sysinit >/dev/msglog 2>/dev/msglog </dev/console
is:3:initdefault:
p3:s1234:powerfail:/usr/sbin/shutdown -y -i5 -g0 >/dev/msglog 2>/dev/msglog
sS:s:wait:/sbin/rcS >/dev/msglog 2>/dev/msglog </dev/console
s0:0:wait:/sbin/rc0 >/dev/msglog 2>/dev/msglog </dev/console
s1:1:respawn:/sbin/rc1 >/dev/msglog 2>/dev/msglog </dev/console
s2:23:wait:/sbin/rc2 >/dev/msglog 2>/dev/msglog </dev/console
s3:3:wait:/sbin/rc3 >/dev/msglog 2>/dev/msglog </dev/console
s5:5:wait:/sbin/rc5 >/dev/msglog 2>/dev/msglog </dev/console
s6:6:wait:/sbin/rc6 >/dev/msglog 2>/dev/msglog </dev/console
fw:0:wait:/sbin/uadmin 2 0 >/dev/msglog 2>/dev/msglog </dev/console
of:5:wait:/sbin/uadmin 2 6 >/dev/msglog 2>/dev/msglog </dev/console
rb:6:wait:/sbin/uadmin 2 1 >/dev/msglog 2>/dev/msglog </dev/console
sc:234:respawn:/usr/lib/saf/sac -t 300
co:234:respawn:/usr/lib/saf/ttymon -g -h -p "`uname -n` console login: " -T sun -d /dev/console -l console -m ldterm,ttcompat
```

系统首次启动时，init 会启动 inittab 文件中标记为 sysinit 的所有进程。/etc/inittab 中的 initdefault 条目标识默认运行级别。在此示例中，默认值为运行级别 3（具有网络文件共享的多用户模式）。init 守护进程运行与此运行级别关联的每个进程（即，其运行级别字段中包含 3 的每个条目）。每个进程都使用 action 字段中的条目运行。action 字段可以具有表 1.5 中列出的值之一。

## 表 1.5
### INITTAB 操作字段

| 字段 | 描述 |
|---|---|
| sysinit | 此字段在 init 尝试通过控制台提示访问控制台之前执行进程。init 在继续读取 inittab 文件之前等待其完成。 |
| powerfail | 系统已收到 powerfail 信号。 |
| wait | 此字段等待命令完成后再移动到包含相同运行级别的下一个条目。 |
| respawn | 如果进程死亡，init 将重新启动该进程。 |

注意 许多 Solaris 启动脚本可以通过其“rc”前缀或后缀来识别，这意味着“运行控制”。

## rc 脚本

每个 init 状态都有相应的运行控制脚本系列，称为 rc 脚本，位于 /sbin 目录中，用于控制每个 init 状态。这些 rc 脚本如下：

- rc0
- rc1
- rc2
- rc3
- rc5
- rc6
- rcS

init 进程执行 /sbin/rc<n> 脚本，这些脚本反过来执行位于 /etc 目录中的一系列其他脚本。对于 /sbin 目录中的每个 rc 脚本，相应的目录名为 /etc/rc<n>.d，其中包含用于该运行级别执行各种操作的脚本。例如，/etc/rc2.d 包含用于启动和停止运行级别 2 进程的文件。在启动时，rc 脚本按数字顺序运行，直到达到默认运行级别；例如，要达到运行级别 3，将运行 /sbin/rc1、/sbin/rc2 和 /sbin/rc3。

所有运行控制脚本也位于 /etc/init.d 目录中。这些文件链接到 /etc/rc<n>.d 目录中的相应运行控制脚本。

以下是安装操作系统时放置在 /etc/rc2.d 中的默认脚本列表。如后所述，系统管理员将向此目录添加自定义脚本：

```
ls /etc/rc2.d
K06mipagent
K07dmi
K07snmpdx
K16apache
K28nfs.server
README
S01MOUNTFSYS
S05RMTTMPFILES
S10lu
S20syssetup
S21perf
S30sysid.net
S40llc2
S47asppp
S69inet
S70uucp
S71ldap.client
S71rpc
S71sysid.sys
S72autoinstall
S72inetsvc
S72slpd
S73cachefs.daemon
S73nfs.client
S74autofs
S74syslog
```

尽管脚本在每个目录中显示为文件，但 rc<n>.d 目录包含指向 /etc/init.d 目录的硬链接。在其他 UNIX 系统上，启动脚本有时可以在 /sbin/rc<n>.d 和 /etc/rc<n>.d 目录中找到。Solaris 中放置了链接，以便习惯于其他类型的 UNIX（HP-UX、SunOS 等）的用户可以轻松找到启动文件。此外，他们可能移植的引用这些启动文件的任何脚本都可以在不修改的情况下兼容。此外，通过将所有脚本放在一个位置 /etc/init.d，可以方便地找到启动或停止特定功能所需的脚本，而无需搜索所有 /etc/rc<n>.d 目录。

- S74xntpd
- S75cron
- S75savecore
- S76nscd
- S80lp
- S80PRESERVE
- S80spc
- S85power
- S88sendmail
- S88utmpd
- S89bdconfig
- S90wbem
- S92volmgt
- S93cacheos.finish
- S94ncalogd
- S95lvm.sync
- S96ab2mgr
- S99audit
- S99dtlogin

/etc/rc<n>.d 脚本始终按 ASCII 排序顺序运行。第一个字母（S 或 K）后面的数字指定脚本运行的顺序，可以是任何数值。数字后面的名称与运行顺序无关。脚本的名称形式如下：

```
[K,S][#][A-Z]
```

以 K 开头的文件用于终止系统进程。以 S 开头的文件用于启动系统进程。每个运行控制级别脚本的操作总结如下：

/sbin/rc0 脚本运行 /etc/rc0.d 脚本，执行以下操作：

- 停止系统服务和守护进程
- 终止所有正在运行的进程
- 卸载所有文件系统

/sbin/rcS 脚本运行 /etc/rcS.d 脚本以将系统提升到单用户模式并执行以下操作：

- 建立最小网络
- 如有必要，挂载 /usr
