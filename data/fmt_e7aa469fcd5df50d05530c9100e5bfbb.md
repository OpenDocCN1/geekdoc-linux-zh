
要将消息发送给用户，请列出他们的登录名。以下示例将关键消息发送给用户 `chris` 和 `aleina` 的控制台：

```
news.=crit chris,aleina
```

你还可以将消息输出到命名管道（FIFO）。动作字段的管道条目以 `|` 开头。以下示例将内核调试消息重定向到命名管道 `|usr/adm/debug`：

```
kern.=debug /usr/adm/debug
```

# /etc/syslog.conf 示例

这里显示 Fedora 系统的默认 `/etc/syslog.conf`。消息被记录在 `/var/log` 目录下的各种文件中。

```
/syslog.conf

# 将所有内核消息记录到控制台 /dev/console

#kern.*

# 记录任何 info 级别或更高级的内容（邮件除外）。

# 不要记录私有的身份验证消息！

*info;mail.none;news.none;authpriv.none;cron.none /var/log/messages

# authpriv 文件具有受限访问。

authpriv.* /var/log/secure

# 将所有邮件消息记录在一个地方 /var/log/maillog

mail.*

# 记录 cron 任务。

cron.* /var/log/cron

# 所有人都能收到紧急消息

*.emerg

# 将 err 级及以上的邮件和新闻错误保存到特殊文件中

uucp,news.crit /var/log/spooler

# 也将启动消息也保存到 boot.log

local7.* /var/log/boot.log

# INN
```

## 第六部分：系统管理

```
news.=crit              /var/log/news/news.crit

news.=err               /var/log/news/news.err

news.notice             /var/log/news/news.notice
```

### Linux 审计系统：auditd

Linux 审计系统提供系统调用审计。审计由一个名为 `auditd` 的服务器执行，日志保存在 `/var/log/auditd` 目录中。它的设计是为了补充 SELinux，SELinux 将其消息发送到 `/var/log/audit/` 文件中的 `auditd` 日志中。审计日志服务为位于 `/var/log/auditd` 等服务提供专门的日志记录。为了细化审计，你可以创建审计规则来检查由特定用户或组生成的系统调用。

你可以使用 `/etc/init.d/auditd` 服务来启动和关闭 `auditd` 服务器。使用 `system-configs` 或 `service` 命令来启动和停止服务器。

```
service auditd start
```

`auditd` 的配置位于 `/etc/audit/auditd.conf`，而 `/etc/sysconfig/audit` 文件由 `/etc/auditd.conf` 处理，该文件包含了日志文件名、日志格式、日志文件最大 `own` 以及当磁盘空间减少时采取的动作等选项。请参阅 `auditd` Man 页面以详细说明所有选项 `/etc/sysconfig/audit` 文件设置启动选项和本地化位置。

`audit` 软件包包含了审计服务器和三个命令：`austrace`、`ausearch` 和 `auditctl`。你使用 `ausearch` 查询审计日志。你可以通过各种 ID、进程、组或事件进行搜索，也可以通过文件名或日期搜索。检查 `ausearch` Man 页面获取完整列表。`audit` 是一个特殊的工具，允许你跟踪特定的进程。它的运行方式与 `trace` 类似，用于记录系统调用和动作。

你可以使用 `auditctl` 工具控制审计服务器的行为。通过 `auditctl`，你可以开启或关闭审计，检查状态，并为特定事件添加审计规则。审计规则组织成预定义的列表，并为系统调用设置了一系列动作。目前有三个列表：`task`（任务）、`entry`（入口）和 `exit`（出口），对应 `never`（从不）、`always`（总是）和 `possible`（可能）。在添加规则时，列表和动作用逗号隔开。使用 `-F` 选项添加规则。通过 `-S` 选项你可以指定特定的系统调用，有几个可以使用的字段，例如 `uid`（用户 ID）、`pid`（进程 ID）和 `exit`（系统调用值）。

```
auditctl -a exit,always -S open -F uid=0
```

### 性能工具

## 第六部分：系统管理

### GNOME 系统监视器

Fedora 提供了 GNOME 系统视视器用于显示信息和监控进程，可以通过系统 | 系统监视器访问。它有四个面板：一个用于系统描述、进程、资源，以及一个用于文件系统（见图 27-2）。资源面板显示 CPU、内存和 Swap 使用的图表。你的文件系统面板列出了文件系统及其挂载位置、类型以及使用量。进程面板列出了你的进程，允许进行排序或搜索。你可以使用字段按名称、进程 ID、CPU 使用率和内存进行排序。视图菜单允许你选择所有进程，通过点击来停止任何进程，或将其隐藏。内存显示了有关虚拟内存、inodes 和标志的信息。

### ps 命令

从命令行，你可以使用 `ps` 命令来列出进程。使用 `-aux` 选项，你可以列出所有进程。将输出管道到带有模式的 `grep` 命令可以允许你搜索特定的进程。管道（`pipe`）将一个命令的输出作为另一个命令的输入。

```
ps -aux | grep ''
```
