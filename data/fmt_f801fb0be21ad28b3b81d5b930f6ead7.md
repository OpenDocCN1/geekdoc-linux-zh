
- 如果 `auditd` 未运行而 `rsyslog` 守护进程运行，拒绝消息将记录在 `/var/log/messages`。

## 第五部分：学习 Linux 安全技术

> 注意：当 `auditd` 和 `rsyslogd` 都在运行，且你的系统上有 `setroubleshoot` 守护进程时，拒绝消息会被发送到 `audit.log` 和 `messages` 日志文件。然而，`messages` 文件中的拒绝信息会被 `setroubleshoot` 守护进程转换成更易于理解的格式。

### 在审计日志中查看 SELinux 消息

如果你运行了审计守护进程，可以使用 `aureport` 命令快速查看是否已记录了 AVC 拒绝信息。接后的示例展示了如何使用 `aureport` 和 `grep` 搜索 AVC 拒绝。至少有一条拒绝已记录在 `/var/log/audit/audit.log` 中。

```
# aureport | grep AVC
Number of AVC's: 1
```

在发现 `audit.log` 中记录了 AVC 拒绝后，你可以使用 `ausearch` 来查看拒绝消息。接后的示例显示了使用 `ausearch` 命令查看已记录的 AVC 拒绝。

```
# ausearch -m avc
Type=AVC(141180414.986:69860): avc: denied ( create ) for pid=21875 comm=vsftpd name="services"
scontext=system_u:r:fptd_t:s0:c0:c1023
tcontext=system_u:object_r:user_home_t:s0 tclass=file
```

显示内容提供了关于谁尝试访问的信息以及他在尝试时的安全上下文。在 AVC 拒绝消息中查找这些键值：
- `type=AVC`
- `avc: denied`
- `pid=`
- `exe=`
- `subj=`

这为你提供了足够的数据，要么开始修复问题，要么追踪恶意活动。

### 在消息日志中查看 SELinux 消息

如果你运行了 `rsyslog`，可以通过 `grep` 搜索 `/var/log/messages` 文件来查找 AVC 拒绝。对于 RHEL 7、Fedora 21 或任何 Linux systemd 系统，你可以运行 `journalctl` 命令来检查 AVC 拒绝日志。每条日志消息中都包含一条审计命令行，你可以运行它来获取有关每个 AVC 拒绝的信息。例如：

```
# journalctl alert
Sep 18 23:58:03 fedora20.example.com setroubleshoot [13449]:
Linux is preventing /usr/sbin/vsftpd from getattr on the
directory /home/chris/Music. For complete SELinux messages. run sealert -1 8f52dd56-8025-4208-af41-72d9bdaa46b
```

从示例来看，一个 SELinux 用户尝试以特定用户身份登录 FTP 服务 `vsftpd`。由于 FTP 使用明文密码，该操作被认为是不安全的，因此被 SELinux 拒绝。注意该 AVC 拒绝消息，你可以通过运行 `sealert -1` 命令来获取更多信息。

`sealert` 工具允许你获取关于特定 AVC 消息的更多信息。`sealert` 提供的信息格式可以帮助你诊断问题。接后的示例展示了 `sealert` 在考虑之前的 AVC 拒绝时提供的信息，这在前一个示例中已经显示过。注意使用的命令与之前的消息日志文件中建议的完全相同。使用的长数字

```
# sealert -1 8f52dd56-8025-4208-af41-72d9bdaa46b
```

## 第 24 章：使用 SELinux 增强 Linux 安全性

实现此目的的命令是 `semanage` 和 `restorecon`。在接下来，这些命令用于为 `/abc/www/html` 目录及其所有内容添加正确的安全上下文类型：

要实际将新的安全上下文类型应用于目录中的文件，你需要使用 `restorecon -R` 命令。实现方法如下：

```bash
# restorecon -R -v /srv/www/html
```

现在，`httpd` 守护进程有权访问位于非标准位置的 HTML 文件。

### 服务的非标准端口

与上述描述的问题类似，你可能决定让服务监听在非标准端口上。当你更改端口时，服务通常无法启动。

例如，出于安全考虑，你决定将 ssh 从端口 22 移动到非标准端口 4736。SELinux 不知道该端口，导致服务启动失败。要修复此，你必须首先找到 ssh 的安全上下文类型。可以通过执行以下代码来实现：发布 `semanage port -1` 命令并将结果通过管道交给 `grep` 搜索 ssh。

```bash
# semanage port -1 | grep ssh
ssh_port_t tcp 22
```

在前面的示例中，需要的类型是 `ssh_port_t`。现在，使用 `semanage` 命令将该类型添加到端口 47347，如下所示：

```bash
# semanage port -a -t ssh_port_t -p tcp 47347
```

接下来，编辑 `/etc/ssh/sshd_config` 文件，向文件中添加 `Port 47347`。然后重启 `sshd` 服务，以配置其监听非标准端口 47347。

### 使用安全上下文标签移动文件

你使用 `cp` 命令将文件从 `/etc` 移动到临时目录 `/tmp`。然后，你使用 `mv` 命令将它移回。现在，该文件拥有临时目录的安全上下文，而不是原始上下文，当你使用该无法启动的服务时，系统会收到 AVC 拒绝消息。

多亏了 `restorecon -R` 命令，这是一个很容易修复的方法。只需运行 `restorecon -R file`，文件就会恢复其原始上下文。

### 布尔值设置错误

另一个常见问题是错误设置了布尔值 `Boolean`。这可能会导致多个 AVC 拒绝。

例如，如果你系统的脚本不再能够连接到网络，并且你在日志中收到 AVC 拒绝，你需要检查 `http` 相关的布尔值。使用 `getsebool -a` 命令并将其传递给 `grep` 以搜索任何影响 `httpd` 的布尔值。示例显示了这些命令的使用：

```bash
getsebool -a | grep http
httpd_network_connect --off
```

`getsebool` 命令显示了 `httpd_network_connect` 被设置为关闭 `off`。要更改此，请使用以下命令：`setboolean -P httpd_network_connect`。注意使用了 `-P` 选项来使设置永久。现在，你的脚本应该能够连接到网络了。

随着你遇到 SELinux 的各种问题，你的故障排除技能将会提高。同时，还有另一个极好的资源可以帮助你排除故障：`http://docs.readthedocs.com`。红帽文档《Red Hat Enterprise Linux》有一整章章节（第 8 章）专门用于 SELinux 的故障排除。

## 整合在一起

显然，SELinux 是一个相当复杂且严格的工具。你现在对 SELinux 基础有了良好且坚实的掌握。以下是在你的系统上开始使用 SELinux 的建议。

你可以使用默认的 `targeted` SELinux 模式来保护大多数基础网络服务 `httpd`、`vsftpd` 等，而无需分配特殊的用户角色或以降低你的系统性能。在这种情况下，你需要做的是：将文件放在标准位置（或运行命令来为非标准位置分配正确的文上下文），确保对布尔值开启你无论如何都需要的低安全性功能，并观察 AVC 拒绝情况以发现问题。

- 从 `permissive`（允许）运行模式开始。这允许 SELinux 允许操作而不拦截。
- 在 `Permissive` 模式下运行当前系统相当一段时间。检查日志并查看在默认 SELinux 设置可能会出现哪些问题。然后你可以更改布尔值或文件上下文，以便允许不当的拒绝。在解决问题后，开启 `enforcing`（强制）模式。
- 总体，在测试环境或使用 `Permissive` 模式一次实施一项 SELinux 配置更改。观察每项配置更改产生的影响，然后再进行下一项。然后你可以使用 `audit2allow` 命令选择性地允许导致 AVC 拒绝的操作在服务允许策略的范围内。

## 获取更多关于 SELinux 的信息

几个额外的信息源可以帮助你在 Linux 系统上使用 SELinux：
