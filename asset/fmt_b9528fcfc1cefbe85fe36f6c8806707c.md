
# 第15章 应用所有权与权限

当前模式：强制 (`enforcing`)

配置文件模式：强制 (`enforcing`)

策略 `MLS` 状态：启用

策略 `deny_unknown` 状态：允许

内核策略最大版本：`31`

启用 `SELinux` 后，它将对一组策略中定义的对象强制访问规则。接下来的章节将解释 `SELinux` 策略的工作原理。

`SELinux` 为系统上的每个对象都标记了安全上下文（security context）。安全上下文定义了 `SELinux` 应用于对象的策略。安全上下文的格式如下：

```
user:role:type:level
```

`user` 和 `role` 属性用于多层安全模式，可能会变得非常复杂。运行在默认目标（`targeted`）安全模式下的系统仅使用 `type` 属性来设置对象的安全类型，并基于此控制访问。`level` 属性设置安全敏感性类型和许可级别。在目标安全模式下，该属性是可选的，主要用于高安全环境。

要查看分配给对象的安全上下文，可以在 `id`、`ls`、`ps` 和 `netstat` 等常用 `Linux` 命令中添加 `-z` 选项。例如，要查看您的用户安全上下文，请使用以下命令：

```
$ -z id
unconfined_u:unconfined_r:unconfined_t:s0-s0:c0.1023
```

`unconfined_u` 安全上下文意味着该用户账户没有分配特定的安全策略；同样，角色对应的是 `unconfined_r`，类型对应的是 `unconfined_t`。`s0-s0:c0.1023` 层安全上下文意味着对象的安全和许可级别也未设置。

要查看文件的安全上下文，请使用此命令：

```
$ ls -z test1.txt
-rw-rw-r-- rich unconfined_u:object_r:user_home_t:s0 test1.txt
```

再次，`user` 和 `role` 属性是未限制的（`unconfined`），但现在 `type` 属性被设置为 `user_home_t`。您可以在安全策略中使用此属性来设置每个用户账户 `$HOME` 目录下的文件的访问权限。

要检查分配给进程的安全上下文，请使用以下命令：

```
$ ps -axZ | grep postfix
system_u:system_r:postfix_master_t:s0 3910 ? Ss 0:00 monitor -w
system_u:system_r:postfix_fix_t:0 3935 ? S 0:00 pickup -l -t unix -u
system_u:system_r:postfix_qmgr_t:0 3936 ? S 0:00 qmgr -l -t unix -u
$
```

`Postfix` 邮件应用程序所需的进程都已设置为 `system_u` 安全上下文和 `system_r` 角色安全上下文。这些表示系统相关的进程。每个进程的 `type` 安全上下文是不同的，这意味着它们可以分别通过不同的策略进行控制。

> 您在 `SELinux` 文档和文献中经常会看到安全上下文被称为“标签”（`label`）。当 `SELinux` 首次启用时，`SELinux` 必须为系统中的每个对象分配标签，这可能是一个漫长的过程。

`semanage` 实用程序允许您查看和设置系统上用户账户的安全上下文。对于文件和目录，`Linux` 系统在创建它们时会根据父目录的安全上下文设置它们的安全上下文。您可以使用 `chcon` 或 `restorecon` 工具更改分配给文件的默认安全上下文。

`chcon` 的格式如下：

```
chcon -u newUser -r newrole -t newtype filename
```

`newUser`、`newrole` 和 `newtype` 定义了您分配给指定文件的新用户、角色和类型安全上下文。

`restorecon` 实用程序将文件或目录的安全上下文恢复为策略中定义的默认设置。您可以使用 `-R` 选项递归地恢复指定目录下所有文件的安全上下文。

`rerun` 实用程序允许您使用指定的安全上下文启动应用程序，但请要小心。如果应用程序在启动时没有访问任何所需的配置或日志文件的权限，可能会发生（而且通常会发生）一些怪异的事情。

## 使用策略

`SELinux` 根据策略控制对系统对象的访问。在目标（`targeted`）安全模式下，每个策略都定义了特定安全上下文内的哪些对象可以访问另一个类型安全上下文内的对象。这被称为“类型强制”（`type enforcement`）。

例如，标记为类型安全上下文 `postfix_master_t` 的应用程序仅允许访问标记为类型安全上下文 `postfix_master_t` 的文件。这限制了应用程序对系统上某些文件的访问。

`SELinux` 在 `/etc/selinux` 目录结构中以文本文件的形式维护策略。例如，所有目标安全模式的策略都在 `/etc/selinux/targeted` 目录下。

创建您自己的策略可能有点复杂。`SELinux` 经常包含名为模块（`modules`）的策略组，您可以作为标准 `RPM` 包安装它们。使用 `semodule` 实用程序可以列出、安装和删除系统中的策略模块。

为了使操作更简单，`SELinux` 使用了一种在不需要修改策略文件的情况下启用和禁用单个策略的方法。布尔值（Boolean）是一个开关，允许您根据其策略名称从命令行启用或禁用策略规则。要查看策略的当前设置，请使用 `getsebool` 命令：

```
$ getsebool antivirus_can_scan_system
antivirus_can_scan_system --> off
```

要查看系统所有的策略，请包含 `-a` 选项，如列表 15.6 所示。

### 列表 15.6：在 getsebool 命令中使用 -a 选项

```
$ sudo getsebool -a
abrt_anon_write --> off
abrt_handle_event --> off
abrt_upload_anon_write --> on
antivirus_can_scan_system --> off
antivirus_use_jit --> off
auditm_exec_content --> on
authlogin_nsswitch_use_ldap --> off
authlogin_radius --> off
authlogin_ubikey --> off
awstats_purge_apache_log_files --> off
boinc_exemem --> on
cdrecord_read --> off
cluster_can_network_connect --> off
cluster_manage_all_files --> off
cluster_use_exemem --> off
cobbler_anon_write --> off
cobbler_can_network_connect --> off
cobbler_use_cifs --> off
cobbler_use_nfs --> off
collectd_tcp_network_connect --> off
condor_tcp_network_connect --> off
conman_can_network --> off
conman_use_nfs --> off
```

列表 15.6 显示了 `get` 命令的部分输出；红帽 `Linux` 环境默认安装了许多不同的策略。要更改布尔设置，请使用 `getsetbool` 命令：
