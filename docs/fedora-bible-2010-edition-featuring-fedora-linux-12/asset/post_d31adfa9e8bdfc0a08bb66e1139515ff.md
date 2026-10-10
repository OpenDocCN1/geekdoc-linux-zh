
## 检查 SELinux 状态

您可以重写默认设置，通过在启动 Fedora 时从 GRUB 屏幕的内核行末尾添加以下内容，在 Linux 引导提示符下将 SELinux 置于宽容模式：

```bash
setenforce 0
```

在 SELinux 处于宽容模式（*setenforce 0*）下，您仍然可以登录并使用系统，任何潜在的毁灭性权限失败只会导致错误消息。如果 SELinux 处于宽容模式，您也可以在启动提示符下输入 *setenforce 1* 将 SELinux 返回到强制模式。您可以使用 SELinux 管理窗口永久更改 SELinux 状态。

### 检查 SELinux 状态

检查 Fedora 系统上 SELinux 状态的工具很多。要检查 SELinux 是否启用，请输入以下内容：

```bash
# sestatus -v | less
SELinux status:				disabled
```

输出显示当前系统未强制执行 SELinux。如果将 SELinux 设置为宽容模式，输出将如下所示：

```text
SELinux status:				enabled
SELinuxfs mount:				/selinux
Current mode:				enforcing
Mode from config file:			enforcing
Policy version:				24
Policy from config file:			targeted

Process contexts:
Current context:			unconfined_u:unconfined_r:unconfined_t:s0-s0:c0.c1023
Init context:				system_u:system_r:init_t:s0
/usr/sbin/sshd			system_u:system_r:sshd_t: s0-s0:c0.c1023

File contexts:
Controlling term:			unconfined_u:object_r:devpts_t:s0
/etc/passwd				system_u:object_r:etc_t:s0
/etc/shadow				system_u:object_r:shadow_t:s0
/bin/bash				system_u:object_r:shell_exec_t:s0
/bin/login				system_u:object_r:login_exec_t:s0
/bin/sh				system_u:object_r:bin_t:s0 ->
					system_u:object_r:shell_exec_t:s0
/sbin/agetty				system_u:object_r:getty_exec_t:s0
/sbin/init				system_u:object_r:init_exec_t:s0
/sbin/mingetty				system_u:object_r:getty_exec_t:s0
/usr/sbin/sshd			system_u:object_r:sshd_exec_t:s0
/lib/libc.so.6			system_u:object_r:lib_t:s0 ->
					system_u:object_r:libc_t:s0
/lib/ld-linux.so.2			system_u:object_r:lib_t:s0 -->
					system_u:object_r:ld_so_t:s0
```

按空格键分页浏览输出。除了显示 SELinux 已启用并正在强制模式外，此输出还显示了已设置的处理上下文和文件上下文。

要从图形界面查看和更改基本 SELinux 设置，您可以打开 SELinux 管理窗口。从 GNOME 桌面，选择“系统 $\rightarrow$ 管理 $\rightarrow$ SELinux 管理”。从该窗口中，您可以设置 SELinux 是禁用、强制还是宽容。您还可以选择要使用的 SELinux 策略（默认是 targeted）。

更改策略类型或将 SELinux 服务从关闭改为打开需要您重新标记整个文件系统。不应轻易更改策略。如果您决定通过 SELinux 管理窗口更改策略，该更改也需要重新标记文件系统。通过此窗口更改策略后，下次重启计算机时文件系统将自动重新标记（或者您可以选择复选框以阻止下次重启时重新标记文件系统）。

> 注意：重新标记文件系统可能是一个漫长且耗时的活动。请记住，更改策略是对操作系统的一项重大更改。文件系统中的节点越多，下次启动计算机时重新标记文件系统所需的时间就越长。

您可以使用带有 $-Z$ 选项的 `id` 命令来检查您操作的安全性上下文。以下示例显示您当前的上下文是 root 用户，您的角色是 $system\_r$ 角色，类型是 $unconfined\_t$。

```bash
# id -Z
unconfined_u:unconfined_r:unconfined_t:s0:c0,c1023
```

SELinux 能够产生大量错误消息。默认情况下，这些消息被重定向到 /var/log/messages 文件。

## 使用 SELinux

虽然 SELinux 支持许多高级功能，例如分类（对仅某些部门可用的资源进行分类）和多级安全性（MLS）以实现受限信息流（机密、绝密），但系统管理员通常只关注域和上下文类型隔离。Fedora 在使 SELinux 可用于典型的 Fedora 服务器和桌面方面取得了巨大进步。如果您安装了 setroubleshoot，当发生 SELinux 强制执行时，将通过 GUI 和 /var/log/messages 通知您，并提供有关如何启用被拒绝的特定访问的提示。

大多数 GNU 实用程序已修改以接受 $-Z$ 选项，以查看进程域（`ps -eZ`）、文件（`ls -Z`）等。如果您认为 SELinux 拒绝了您对特定资源的访问，例如通过 Apache 运行的 PHP 脚本，运行 SELinux 管理 GUI 将允许您设置布尔值以关闭特定守护程序或该守护程序特定功能的 SELinux。

以下是在典型服务器上使用 SELinux 的一些快速示例：

```bash
setsebool -P httpd_enable_homedirs on # 允许 Apache 读取用户主目录
restorecon -r /var/www/html # 通过咨询上下文数据库重置文件上下文
chcon -t public_content_rw_t /var /http/incoming # 手动设置文件上下文
```

您可以使用 `sesearch` 命令按如下方式探索当前加载的 SELinux 策略：

```bash
# ssearch --allow -s ftpd_t -p write -c dir -t public_content_rw_t -C
Found 2 semantic av rules:
DT allow ftpd_t public content rw_t : dir | { ioctl read write create getattr setattr lock unlink link rename add_name remove_name reparent search rmdir open } ;
allow ftpd_anon_write |
DT allow ftpd_t public content_rw_t : dir | { ioctl read write create getattr setattr lock unlink link rename add_name remove_name reparent search rmdir open } ;
allow ftpd_full_access |
```

在上面的示例中，我们在策略中搜索任何允许域 ftpd_t (-s) 写入具有上下文类型 public_content_rw_t (-t) 的目录 (-c dir) 的允许规则 (--allow)，并显示我们需要设置以启用该规则的任何布尔值 (-C)。正如输出中所示，如果启用了 allow_ftpd_anon_write，则该规则将处于活动状态。

鉴于 setroubleshoot 的帮助性质，SELinux 管理 GUI 的易用性以及启用或禁用 SELinux 中特定规则的细粒度控制，您需要完全关闭 SELinux 的情况应该很少。

## 学习更多关于 SELinux 的知识

要深入了解 SELinux，有各种技术报告、常见问题解答（FAQ）和组件文档可用。以下是一些您可以尝试的地方：

- **SELinux 常见问题解答** ([docs.fedoraproject.org/selinux-faq/](https://docs.fedoraproject.org/selinux-faq/)) — 此网站提供特定于 Fedora 中 SELinux 实现的信息。
- **SELinux wiki** ([http://fedoraproject.org/wiki/SELinux](http://fedoraproject.org/wiki/SELinux)) — 提供更多关于 SELinux 常见问题解答的最新信息。
- **SELinux 文档** ([www.nsa.gov/research/selinux/docs.shtml](http://www.nsa.gov/research/selinux/docs.shtml)) — 此网站提供与 SELinux 相关的已发表论文、技术报告和演示文稿的链接。

## 总结

虽然您可能将 Fedora 用作单用户系统，但您必须执行的许多保持计算机运行的任务被定义为管理员任务。需要一个名为 root 用户的特殊用户帐户来完成许多使 Linux 系统按您希望的方式运行所必需的任务。如果您管理一个由许多人使用的 Linux 系统，管理任务变得更大。您必须能够添加和支持用户，维护文件系统，并确保系统性能很好地服务于您的用户。

为了帮助管理员，Fedora 附带了各种命令行实用程序和图形窗口，用于配置和维护您的系统。FirstAidKit 程序可用于诊断、修复和恢复系统问题。诸如 mkfs 和 mount 等命令分别允许您创建和挂载文件系统。诸如系统监视器和 top 等工具允许您监控系统性能。

SELinux 在现有 Linux 安全方法之上添加了一层新的安全层。作为系统管理员，您可以选择是否打开 SELinux。您还可以选择哪些系统服务受 SELinux 保护。
