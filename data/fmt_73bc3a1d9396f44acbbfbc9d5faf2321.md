
$ systemctl -p UnitPath show

UnitPath=/etc/systemd/system.control /run/systemd/system.control /run/systemd/

transient /etc/systemd/system /run/systemd/system /run/systemd/lib/

systemd /run/systemd/generator.late

```
要查看系统上的系统单元和配置目录，请使用以下命令：
```
$ pkg-config systemd --variable=systemdunitdir
/lib/systemd/system
$ pkg-config systemd --variable=systemdsystemconfdir
/etc/systemd/system
```
## 单元文件

单元文件的格式源自 XDG Desktop Entry 规范（用于 `.desktop` 文件，这些与微软的 `.ini` 文件非常相似），在方括号 `[]` 中包含名称，并在每个节中包含键值赋值（选项）。

例如，考虑用于桌面守护进程的 `dbus-daemon.service` 单元文件：
```
[Unit]
Description=D-Bus 系统消息总线
Documentation=man:dbus-daemon(1)
Requires=dbus.socket
RefuseManualStart=yes
```
```
[Service]
ExecStart=/usr/bin/dbus-daemon --system --address=systemd: --nofork --pidfile
--system-activation=syslog-only
ExecReload=/usr/bin/dbus-send --print-reply --system --type=method_call --dest=org.freedesktop.DBus /ReloadConfig
```
这里有两个部分，`[Unit]` 和 `[Service]`。`[Unit]` 部分提供了有关单元的某些详细信息，并包含依赖信息。特别是，此单元需要 `dbus.socket` 单元作为依赖。

在类似这样的服务单元中，你会在 `[Service]` 部分找到有关服务的详细信息，包括如何准备、启动和重载服务。你可以在 `systemd.service(5)` 和 `systemd.exec(5)` 手页中找到完整的列表，也可以在 6.3.5 节关于进程跟踪的讨论中找到。

许多其他单元配置文件同样直观。例如，`sshd.service` 服务文件通过启动 `sshd` 启用远程 shell 登录。

142 第 6 章

## 注意

你在系统中找到的单元文件可能略有不同。在示例中，你看到 Fedora 使用 `dbus-daemon.service`，而 Ubuntu 使用 `dbus.service`。实际文件中也可能存在变化，这些变化通常是浅表的。

## 变量

你会在单元文件中找到变量。以下是第 10 节中将学习的不同安全 shell 的节：
```
[Service]
EnvironmentFile=/etc/sysconfig/sshd
ExecStart=/usr/sbin/sshd -D $OPTIONS $CRYPTO_POLICY
ExecReload=/bin/kill -HUP $MAINPID
```
带有美元符号 (`$`) 的内容都是变量。虽然这些变量具有相同的语法，但它们的来源不同。`$OPTIONS` 和 `$CRYPTO_POLICY` 可以在单元激活时传递给 `sshd`，它们在 `EnvironmentFile` 设置指定的范围内定义。在特定情况下，你可以查看 `/etc/sysconfig/sshd` 来确定变量是否已设置，如果设置了，它们的值是什么。

相比之下 ownMAINPID` 包含被跟踪的服务进程的 ID（见第 6.3.5 节）。激活后，systemd 会记录并存储此 PID，你稍后可以使用它操作特定服务的进程。`sshd.service` 单元文件使用 `$MAINPID` 在你想重载配置时向 `sshd` 发送挂起 (HUP) 信号，这是处理重载和重启 Unix 守护进程的一种常用技术。

## 占位符 (Specifiers)

占位符是单元文件中常见的类变量的特征。占位符以百分号 (`%`) 开头。例如，`%i` 是单元名称，`%H` 是当前主机。

你还可以使用占位符从单个单元创建多个副本。使用这种功能是在单元名称末尾添加 `@` 符号。例如，在大多数发行版中，文件名是 `getty@service`。在激活时，systemd 将 `%I` 或 `%i` 替换为实例名称。

# Linux 工作原理（早期访问）© 2021 Brian Ward

## 6.3.4 systemd 操作

你主要通过 `systemctl` 与 systemd 交互，它允许激活和禁用服务、列出状态、重载配置等。

最基本的命令帮助你获取单元信息。例如，要查看系统上的单元列表，执行 `list-units` 命令。（这是 `systemctl` 的默认命令，因此技术上不需要 `list-units` 参数。）

$ systemctl list-units

输出格式是典型的 Unix 列表命令。例如，头部和针对 `-mount` 的行如下所示：

| UNIT | LOAD | ACTIVE | SUB | DESCRIPTION |
| -mount | loaded | active | | Root |

默认情况下，`systemctl` 生成列表输出，因为典型系统有许多活动单元，但仍然是缩略形式，因为 `systemctl` 会截断较大的单元名称。要查看单元名称，请使用 `--full` 选项；要查看所有单元（而不只是活动单元），请使用 `--all` 选项。

一个特别常用的 `systemctl` 操作是获取特定单元的状态。例如，这里是典型的状态命令及其部分输出：

$ systemctl status sshd.service

+   - sshd.service - OpenBSD Secure Shell server
Loaded: loaded (/usr/lib/systemd/system/sshd.service); vendor preset: enabled; enabled;
Active: active (running) Fri 2021-04-16 EDT; 08:15:41 1 month 1 days ago

输出后面可能还有许多日志消息。如果你习惯了传统的 init 系统，可能会对此命令提供的可用信息量感到惊讶。不仅可以获取单元状态，还可以获取关联进程、启动时间以及大量的日志。

其他单元类型的输出包含类似的信息。输出的一个有趣部分是控制组 (cgroup) 名称。在之前的示例中，控制组是 `/system.slice/sshd.service`，cgroup 中的进程显示在其下方。然而，你可能也

第 6 章

Linux 工作原理（早期访问版）© 2021 Brian Ward

如果单元（例如，挂载单元）的进程已经终止，请查看名为 `systemd-/system` 的控制组。你可以使用 `system-cgroups` 命令在不显示单元其他状态的情况下查看系统相关的 cgroups。你将在第 6.3.5 节学习更多关于 systemd 如何使用 cgroups，以及在第 8.6 节学习 cgroups 的工作原理。

`status` 命令还会显示该单元最近的诊断日志消息。你可以这样查看单元的所有消息：
```
$ journalctl --unit_name
```
你将在第 7 章学习更多关于 `journalctl` 的知识。

注意：取决于你的系统和用户配置，你可能需要超级权限才能运行 `journalctl`。

## 作与启动、停止和重载单元的关系

要激活、停用和重启单元，请使用 `systemctl start`、`systemctl stop` 和 `systemctl restart` 命令。然而，如果你更改了单元配置文件，可以通过两种方式之一告诉 systemd 重新加载该文件：
```
systemctl reload unit - 仅重新加载单元的配置。
systemctl daemon-reload - 重新加载所有单元配置。
```
激活、重新激活和重启单元的请求在 systemd 中被称为“作业”（jobs），它们本质上是单元状态的变化。你可以通过以下命令检查系统上的当前作业：
```
$ systemctl list-jobs
```
