
# cat /usr/share/doc/selinux-policy/example.te

```text
policy_module(myapp, 1.0.0)

###########################################
#
# 声明
#

type myapp_t;
type myapp_exec_t;
domain_type(myapp)
domain_entry_file(myapp, myapp_exec_t)

type myapp_log_t;
logging_log_file(myapp, myapp_log_t)

type myapp_tmp_t;
files_tmp_file(myapp_tmp_t)
...
allow myapp_t myapp_t:file manage_file_perms;
files_tmp_filetransans(myapp, myapp_tmp_t, file)
#
```

你可以从前面的示例代码中看到策略代码使用了特殊的语法。要创建和修改策略规则，你需要学习这种策略语言语法，学习如何使用 SELinux 策略编译器，并学习如何将策略规则文件链接起来形成模块；你可能需要上几整天的课程才能完成。在此时，你可能会放弃 SELinux。然而，使用布尔值来修改策略要容易得多。

## 通过布尔值管理 SELinux

SELinux 策略编写和模块创建是一项相当复杂且耗时的活动。创建不正确的策略规则可能会损害你 Linux 系统的安全性。坦率地说，SELinux 提供了布尔值。

布尔值是一个用于切换设置开启或关闭的开关。布尔开关允许在不了解策略编写的情况下更改 SELinux 策略规则的部分。这些策略更改也可以无需重启系统即可完成！

要查看 SELinux 中使用的所有布尔值列表，请使用 `getboolean -a` 命令。以下是 Fedora Linux 系统上带有布尔值的 SELinux 策略规则示例：

```bash
# getboolean -a
abrt_anon_write --> off
abrt_handle_event -- on

zebra_write_config -- off
zoneiminder_anon_write --> off
zoneiminder_run_sudo -- off
```

要查看可以通过布尔值修改的特定策略，再次使用 `getboolean` 命令。这次向它传递策略名称，如下例所示：

```bash
# getboolean httpd_can_connect_ftp
httpd_can_connect_ftp --> off
```

要切换策略，可以使用 `setboolean` 命令。这种方法会临时更改策略。要使更改永久，请使用 `-P` 选项。`setboolean` 命令具有开启策略（1 或 true）和关闭策略（0 或 false）的设置。

使用 `setboolean` 的示例是限制执行文件的使用。为了防止这种情况发生，需要关闭 `allow_exec_content` 策略。

```bash
# setboolean -P allow_exec_content off
```

## 第五部分：学习 Linux 安全技术

使用 `getboolean` 命令验证布尔值设置已生效：

```bash
# getboolean allow_exec_content
allow_exec_content --> off
```

布尔值使得修改 SELinux 策略变得简单得多。总的来说，`getboolean` 等 SELinux 命令行工具很好用。然而，如果你使用 GUI 工具，SELinux 也有一个。对于 Fedora，可以通过 `dnf install policycontrols` 安装。要使用该工具，只需输入命令 `system-config-selux` 即可出现界面。

## 监控 SELinux

SELinux 为监控和记录活动的工具提供了大量信息。它记录所有拒绝访问的情况，这可以帮助你判断是否存在攻击。这些 SELinux 日志文件对于排除 SELinux 问题同样有用。

### 理解 SELinux 日志

SELinux 在检查安全上下文策略规则时使用名为 AVC 的缓存。当拒绝访问时（称为 AVC 拒绝），会被拒绝消息。

这些记录的拒绝消息有助于诊断和解决 SELinux 策略违反问题。拒绝消息记录的位置取决于 `auditd` 和 `rsyslog` 守护进程的状态：

- 如果 `auditd` 守护进程正在运行，拒绝消息记录在 `/var/log/audit/audit.log` 中。
- 如果 `auditd` 未运行而 `rsyslog` 守护进程正在运行，拒绝消息记录在 `/var/log/messages` 中。

> **注意**
>
> 如果 `auditd` 和 `rsyslog` 运行且你的系统中安装了 `troubleshootd` 守护进程，拒绝消息会被发送到 `audit.log` 和 `messages` 文件。但是，`messages` 文件中的拒绝信息会被 `troubleshootd` 守护进程转换为更易理解的格式。

### 在审核日志中查看 SELinux 拒绝

如果你运行了 `auditd` 守护进程，可以使用 `aureport` 命令快速查看是否记录了任何 AVC 拒绝。下面的示例显示了如何使用 `aureport` 和 `grep` 搜索 AVC 拒绝。至少有一个拒绝记录在 `/var/log/audit/audit.log` 中：

```bash
# aureport | grep AVC
Number of AVC's: 1
```

## 第 25 章：使用 SELinux 增强 Linux 安全性

当你发现 `audit.log` 中记录了 AVC 拒绝（denial）信息后，可以使用 `ausearch` 来查看拒绝消息。接下来的示例展示了如何使用 `ausearch` 命令查看 AVC 拒绝消息：

```bash
# ausearch -m avc
type=AVC msg=audit(1580397837.344:274): avc: denied ( getattr ) for
pid=106
comm="httpd" path="/var/myserver/services" dev="dm-0" ino=655836
scontext=system_u:system_r:httpd_t:0 tcontext=unconfined:object_r:var_t:0 class=file permissive=0
```

显示内容提供了关于尝试访问者的信息，以及他们在解释信息时的安全上下文。请在 AVC 拒绝消息中寻找这些关键词：

- `type=AVC`
- `avc: denied`
- `comm="httpd"`
- `path="/var/myserver/services"`

这可以为你提供足够的数据来开始修复问题或追踪恶意活动。在这里，`/var/myserver/services` 目录被 httpd 服务读取了错误的 SELinux 文件内容。

### 在消息日志中查看 SELinux 消息

如果你运行了 `auditd` 服务，可以通过 `grep` 搜索 `/var/log/audit/audit.log` 文件来查找 AVC 消息。对于最新的 RHEL 和 Fedora 系统或使用 systemd 的 Linux 系统，你也可以运行 `journalctl` 命令来检查 AVC 日志消息。每条日志消息中都包含一条 AVC 消息，你可以查看以获取有关 AVC 拒绝的信息，如下例所示：

```bash
# journalctl | grep avc
type=AVC msg=audit(1580397837.346:275): avc: denied ( getattr ) for
pid=106
comm="httpd" path="/var/myserver/services" dev="dm-0" ino=655836
scontext=system_u:system_r:httpd_t:0 tcontext=unconfined:object_r:var_t:0 class=file permissive=0
```

由于你已经知道存在 AVC 拒绝，你可以解析 `/var/log/audit/audit.log` 文件来逐步解决问题：

```bash
# sealert -a /var/log/audit/audit.log
Linux is preventing httpd from getattr access on the file
/var/myserver/services.
```

如果你认为 httpd 默认应该被允许对 services 文件进行 `getattr` 访问，那么你应该将其报告为错误（bug）。

### 部分：学习 Linux 安全技术

你可以生成一个本地策略模块来允许这种访问。现在通过执行以下命令来临时允许这种访问：

```bash
# ausearch -c 'httpd' --raw audit2allow -M my-httpd
# semodule -i my-httpd
```

额外信息：

| 源上下文 | 目标上下文 | 目标对象 |
| :--- | :--- | :--- |
| system_u:system_r:httpd_t:0 | unconfined_u:object_r_var_t:0 | /var/myserver/services [ ] |

原始审计消息：

```text
type=AVC msg=audit(150389737.346:275): avc: denied { getattr } for pid=1066 comm="httpd" path="/var/myserver/services" dev="dm-0" ino=655836 scontext=system_u:system_r:httpd_t:0 tcontext=unconfined_u:object_r_var_t:0 tclass=file permissive=0
```

Hash: httpd,httpd_var_t_file,getattr

在这种情况下，如果你想允许 httpd 服务访问被拒绝的目录中的内容，可以运行输出中显示的 `ausearch` 和 `semodule` 命令。这将创建并应用一个新的 SELinux 策略，以允许对该内容的访问。此时没有权限问题，httpd 应该能够访问该内容。

## 故障排除 SELinux 日志

显然，日志文件对于诊断和解决 SELinux 策略违规至关重要。日志文件或直接查询系统日志（`journalctl` 命令）是你排查 SELinux 问题的第一步。确保你的 Linux 系统首先正在记录消息是非常重要的。

确定日志是否正在记录的一种快速方法是检查相应的守护进程正在运行：`auditd`、`rsyslogd` 和/或 `troubleshootd`。使用相应的命令 `systemctl status auditd.service`。当然，命令取决于你的 Linux 发行版及其版本。更多细节请参见第 15 章。如果守护进程未运行，请启动它以便开始记录。

> **注意**：有时由于审计策略规则，AVC 拒绝不会被记录。`dontaudit` 规则减少了日志中的误报，但在排除故障时会导致问题。要修复此，请使用 `semodule -DB` 命令临时禁用所有 `dontaudit` 规则。

## 排除常见的 SELinux 问题

当你开始使用 SELinux 时，很容易忽视显而易见的问题。每当访问被拒绝时，你都应该检查传统的 Linux DAC（访问控制）权限。例如，使用 `ls -l` 命令检查文件的所有者、组以及读、写、执行分配是否正确。

对于 SELinux，几个常规项目可能会导致问题：

- 为服务使用非标准目录
- 为服务使用非标准端口
- 移动文件导致上下文丢失
- 布尔值设置错误

### 为服务使用非标准目录

由于各种原因，你可能会将服务存储在非 `/var/www/html` 的目录。当你这样做时，需要 SELinux 知道这种非标准行为。否则，它会拒绝访问请求。例如，你决定将 HTML 文件存放在 `/var/www/html` 不同的位置。你需要让 SELinux 知道你想访问 `/abc/html` 目录的文件。为了完成此操作，使用的命令是 `semanage` 和 `restorecon`。在下面的代码段中，这些命令用于为 `/abc/html` 添加正确的上下文类型：

```bash
# semanage fcontext -a -t httpd_content_t "/abc/html(/*)?"
# restorecon -R /abc/html
```

现在 httpd 可以访问该目录。

### 为服务使用非标准端口

与前面的示例类似，当你决定使用非标准端口时，服务通常无法启动。要修复此，你必须找到所需的上下文。使用 `semanage` 命令，将其添加到端口：

```bash
# semanage port -a -t ssh_port_t -p tcp 22
# semanage port -l | grep ssh
ssh_port_t  22
```

此时，编辑 `/etc/ssh/sshd_config` 文件添加 `Port 22` 行。然后重启 sshd 服务以监听端口。

### 移动文件并丢失上下文

你使用 `cp` 命令将文件临时从 `/etc` 移动到 `/tmp` 目录。使用 `mv` 命令将其移回。现在文件具有临时目录的上下文，而不是原始的安全上下文，当你使用该文件时系统会获取 AVC 消息。

有一个简单的修复方法，使用 `restorecon` 命令。只需输入 `restorecon file`，文件即可恢复其上下文。

### 布尔值设置错误

另一个常见问题是布尔值设置错误。这会导致多个 AVC 拒绝。例如，如果你的脚本不再能够连接网络并且你在日志中收到 AVC 拒绝，你需要检查 httpd 的布尔值。使用 `getboolean -a` 命令并将其通过 `grep` 以搜索任何影响 httpd 的布尔值。

```bash
# getboolean -a | grep http
httpd_can_network_connect  --> off
```

`getboolean` 命令显示布尔值 `httpd_can_network_connect` 为 `off`。要更改此布尔值，使用以下命令：

```bash
# setboolean -P httpd_can_network_connect on
```

显然，SELinux 是一个相当复杂且丰富的工具。你现在对 SELinux 基础知识有了良好的坚实基础。在你开始在系统上实施 SELinux 之前，这里有一些建议。

## 第 25 章：使用 SELinux 增强 Linux 安全性

默认的针对型（targeted）SELinux 模式可用于保护大多数基础网络服务（httpd、vsftpd、Samba 等），而无需分配特殊用户角色或以其他方式降低系统。在这种情况下，你需要做的主要工作是将文件存放在标准位置（或运行命令为非标准位置导入适当的文件上下文），确保对你认为无论如何都不安全的的服务开启相应的布尔值，并监控 AVC 拒绝（denials）以发现问题。

- 从允许（permissive）运行模式开始。这允许 SELinux 认为不安全的请求执行成功，同时记录这些不安全行为。
- 在允许模式下运行你的当前系统一段时间。检查日志并查看在默认 SELinux 设置下可能会出现哪些问题。然后，通过更改布尔值或文件上下文，使得被恰当拒绝的功能能够被允许。在解决问题后，开启强制（enforcement）模式。
- 总的来说，请在测试环境中或使用允许模式一次实现一个 SELinux 配置。在移动到下一个配置之前，查看每种配置更改产生什么影响。然后你可以使用 `audit2allow` 命令，允许被 AVC 拒绝拦截的操作在服务的策略中被选择性允许。

## 获取有关 SELinux 的更多信息

几个额外的信息源可以帮助你了解系统上的 SELinux：

**你的系统的 man 页面（帮助文档）**
执行命令 `man -k selinux` 可以找到你可以为系统上当前安装的所有 SELinux 实用程序查看的 man 页面。如果你正在为常用服务（如 httpd、vsftpd、Samba 等）调试 SELinux 问题，可能有一个专门介绍如何修复该服务 SELinux 问题的 man 页面。例如：

```bash
$ man -k selinux | grep vsftpd
systemd_vsftpd_generator_selinux (8) - SELinux for systemd_vsftpd_generator
```

**红帽企业 Linux 手册**
位于 https://docs.redhat.com，该网站包含一本关于 SELinux 的入门手册。

**Fedora 项目 SELinux 指南**
位于 https://docs.fedoraproject.org，该网站有一份《增强 Linux 指南》。然而，该指南没有针对每个 Fedora 版本进行更新，因此你可能需要查看旧版本来找到它。此外，SELinux 指南并不位于安全手册中，但 SELinux 手册也是一份很好的查阅手册。

**SELinux 项目 Wiki**
这是官方的 SELinux 项目页面。该网站位于 https://github.com/selinuxproject 提供了资源。

## 第五部分：学习 Linux 安全技术

## 总结
