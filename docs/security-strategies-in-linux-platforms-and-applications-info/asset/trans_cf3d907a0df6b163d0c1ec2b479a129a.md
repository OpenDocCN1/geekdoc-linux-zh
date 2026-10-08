

## 第 4 章 | 用户权限与许可

需要写入该目录的权限。用户没有权限覆盖或删除其他用户写入的文件。

虽然其他用户可能可以读取写入 `/tmp` 的内容，但他们无法删除或覆盖这些文件。如果你想在不同的目录上设置粘滞位（sticky bit），可以使用 `chmod` 命令来帮助。以下命令为 `/newtmp` 目录设置粘滞位：

```
# chmod o+t /newtmp
```

或者，以下命令为 `/newtmp` 目录上的所有用户设置读、写、执行权限的粘滞位：

```
# chmod 1777 /newtmp
```

## 跟踪访问日志

Linux 支持服务和内核日志记录。直到最近，这些配置位于 `/sbin/` 目录下的两个不同守护进程 `syslog` 和 `klog` 中。最新版本的 Linux 包含了一个继者 `/sbin/rslog` 守护进程。功能没有改变。系统日志和内核日志是交织在一起的，它们通常属于同一个包 `rsyslog` 或 `syslog`。Ubuntu 和红帽在处理该文件的日志配置时采取了不同的方法。

本节侧重于跟踪访问——即找到那些记录登录尝试、特别是登录失败的日志。这些服务将日志消息归类为若干领域。相关领域是 `auth` 和 `authpriv`。在日志服务配置文件的语言中，`auth` 和 `authpriv` 被称为“设施”（facilities）。虽然两者都传输相同的消息，但 `authpriv` 设施通常与更安全的文件相关联。

本节介绍了通过日志跟踪访问的基础知识。然而，如果你是多个系统的管理员，可能更喜欢在出现问题时向你发送警的系统。那就是日志监控系统。监控的一种选择是 `logwatch` 日志分析服务，在第12 章中描述。

## 授权日志选项

许多 Linux 发行版正从 `syslog` 过渡到 `rsyslog` 包。主要的 `syslog` 配置文件是 `/etc/syslog.conf`。`rsyslog` 包的主要配置文件是 `/etc/rsyslog.conf`。在 Ubuntu 上，它引用 `/etc/rsyslog.d/` 中的 `50-default.conf` 文件。

尽管配置文件的名称和位置发生了变化，但基本指令没有变。具体来说，对于基于 Debian 的系统，直接将登录尝试的信息发送到 `/var/log/auth.log` 文件：

- auth, authpriv. * /var/log/auth.log

对于红帽系统，以下指令将登录尝试的信息发送到 `/var/log/secure` 文件：

- authpriv* /var/log/secure

![](img/c0608a8c8a0777903dfec4ff61fdffa1_126_0.png)

# 图 4-2

Feb 21 10:49:28 RHELserver ssh[27551]: Invalid user test from 60.217.234.134
Feb 21 10:49:28 RHELserver ssh[27552]: input_userauth: invalid user test for user
Feb 21 10:49:28 RHELserver ssh[27551]: pam_unix(sshhd:auth): check pass; user unknown known
Feb 21 10:49:28 RHELserver ssh[27551]: pam_unix(sshhd:auth): authentication failure
user login: uid=0 eid=0 rhost=60.217.234.134: retrieval error
Feb 21 10:49:28 RHELserver ssh[27551]: pam_succeeded if(sshhd:auth): error retrieving information about user test
Feb 21 10:49:30 RHELserver ssh[27551]: Failed password for invalid user test from 60.217.234.134 port 22
Feb 21 10:49:30 RHELserver ssh[27552]: Received disconnect from 60.217.234.134:
Feb 21 10:49:32 RHELserver ssh[27553]: Invalid user test from 60.217.234.134
Feb 21 10:49:32 RHELserver ssh[27554]: input_userauth: invalid user test for
Feb 21 10:49:32 RHELserver ssh[27553]: pam_unix(sshhd:auth): check pass; user unknown
Feb 21 10:49:32 RHELserver ssh[27553]: pam_unix(sshhd:auth): authentication failure
user login: uid=0 eid=0 tty=ssh rhost=60.217.234.134
Feb 21 10:49:32 RHELserver ssh[27553]: pam_succeeded if(sshhd:auth): error retrieving information about user test

远程登录尝试失败。

## 授权日志文件

上述日志文件是保持系统安全的重要工具。得益于 `/etc/logrotate.conf` 文件和定期的 `cron` 脚本，日志每周轮转一次。这样配置的 Linux 系统通常包含几周的日志。以前版本的日志带有一个 `?`，其中 `?` 是一个数字（`?` 是标准的 Linux 字母通配符）。

这些日志的大小可能很重要。任何日志文件大小的跳跃表明活动增加。虽然这种活动的增加可能只是由于用户的 `cron` 任务运行得更频繁。

图 4-2 中的日志片段显示与尝试登录名为 RHELserver 的系统相关的消息，首先作为用户 `test`，然后作为用户 `test1`。它提供了关于协议和用户的信息。

# 102 第 2 部分 | 分层安全与 Linux

# 图 4-2

```text
Feb 21 10:49:28 RHELserver ssh[27551]: Invalid user test from 60.217.234.134
Feb 21 10:49:28 RHELserver ssh[27552]: input_userauth: invalid user test for user
Feb 21 10:49:28 RHELserver ssh[27551]: pam_unix(sshhd:auth): check pass; user unknown known
Feb 21 10:49:28 RHELserver ssh[27551]: pam_unix(sshhd:auth): authentication failure
user login: uid=0 eid=0 rhost=60.217.234.134: retrieval error
Feb 21 10:49:28 RHELserver ssh[27551]: pam_succeeded if(sshhd:auth): error retrieving information about user test
Feb 21 10:49:30 RHELserver ssh[27551]: Failed password for invalid user test from 60.217.234.134 port 22
Feb 21 10:49:30 RHELserver ssh[27552]: Received disconnect from 60.217.234.134:
Feb 21 10:49:32 RHELserver ssh[27553]: Invalid user test from 60.217.234.134
Feb 21 10:49:32 RHELserver ssh[27554]: input_userauth: invalid user test for
Feb 21 10:49:32 RHELserver ssh[27553]: pam_unix(sshhd:auth): check pass; user unknown
Feb 21 10:49:32 RHELserver ssh[27553]: pam_unix(sshhd:auth): authentication failure
user login: uid=0 eid=0 tty=ssh rhost=60.217.234.134
Feb 21 10:49:32 RHELserver ssh[27553]: pam_succeeded if(sshhd:auth): error retrieving information about user test
```

远程登录尝试失败。

![](img/c0608a8c8a0777903dfec4ff61fdffa1_126_0.png)

## 可插入模块 (Pluggable Modules)

本节介绍了通过日志跟踪访问的基础知识。然而，如果你是多个系统的管理员，可能更喜欢在出现问题时向你发送警的系统。那就是日志监控系统。监控的一种选择是 `logwatch` 日志分析服务，在第12 章中描述。

上述日志文件是保持系统安全的重要工具。得益于 `/etc/logrotate.conf` 文件和定期的 `cron` 脚本，日志每周轮转一次。这样配置的 Linux 系统通常包含几周的日志。以前版本的日志带有一个 `?`，其中 `?` 是一个数字（`?` 是标准的 Linux 字母通配符）。

这些日志的大小可能很重要。任何日志文件大小的跳跃表明活动增加。虽然这种活动的增加可能只是由于用户的 `cron` 任务运行得更频繁。

图 4-2 中的日志片段显示与尝试登录名为 RHELserver 的系统相关的消息，首先作为用户 `test`，然后作为用户 `test1`。它提供了关于协议和用户的信息。

# 102 第 2 部分 | 分层安全与 Linux

```text
# apt-cache libpam
```

- pam-apparmor
- pam-blue
- pam-crack
- pam-doc
- pam-gnome-keyring
- pam-kerberos
- pam-ldap
- pam-mount
- pam-radius
- pam-runtime
- pam-sam
- pam-smart
- pam-session

PAM 配置在 `/etc/pam.d/` 中的特定文件中。这些文件（如 `password` 和 `ssh`）准确地描述了受监管的命令或服务。

## PAM 配置文件的结构

PAM 配置文件的结构基于其模块，这些模块位于 `/lib/security/` 目录。如果你在这里找不到需要的模块，可能需要安装另一个 PAM 相关包。PAM 配置文件的每一行按照以下格式设置：

module_type control_flag module_file (arguments)

旧版本的 PAM 需要模块的完整路径。当前版本假设模块位于 `/lib/security/` 目录。如果已安装，更多关于 module_file（例如模块使用的参数）可以从帮助页中获取。这留下了 module_type 和 control_flag 选项。首先，有四种不同的模块类型：

- auth——通过验证密码、组组成甚至 Kerberos 令牌来验证用户。称为身份验证管理。
- account——根据过期日期、时间限制或受限制用户的配置文件检查账户的有效性。称为账户管理。
- password——控制用户密码的更改。也可以控制登录尝试次数。称为密码管理。
- session——使连接工作；它可能会挂载适当的目录并将信息写入系统日志。称为会话管理。

存在一个隐式的默认模块类型 `include`，它合并另一个文件的配置指令。

![](img/c0608a8c8a0777903dfec4ff61fdffa1_128_0.png)

# 第 4 章 | 权限与许可

