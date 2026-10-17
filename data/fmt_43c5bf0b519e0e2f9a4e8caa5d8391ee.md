
- `selinux-doc` —— 包含存储在 `/usr/share/selinux-doc` 目录中的 SELinux 文档列表。
- `selinux-policy-mls` —— 包含 SELinux 的多级安全转换表。
- `selinux-policy-targeted` —— 包含用于将面向目标的 SELinux 策略集成到运行中的 Linux 系统中的示例策略文件，以及用于对 SELinux 进行运行时更改所需的上下文文件和 `booleans` 文件。
- `setools` —— 包含用于管理运行中策略部分（这些部分定义了用户对 Linux 系统不同组件的访问权限）的工具。

#### 检查 SELinux 是否开启

安装 Fedora 后，你可以检查 `/etc/selinux/config` 文件（该文件链接到 `/etc/sysconfig/selinux`），查看 SELinux 是否已启用，如果已启用，哪些策略正在生效。该文件为配置为使用 SELinux 的 Fedora 系统设置了两个关键变量：

- `SELinux 状态` `SELinux State` —— `SELINUX` 变量设置 SELinux 的状态。如果在 Fedora 安装期间启用了 SELinux，初始值通常为 `SELINUX=enforcing`（这将强制执行 SELinux 的安全策略）。如果在安装期间禁用了 SELinux，则设置为 `SELINUX=disabled`。第三种选择是设置 `SELINUX=permissive`，这会基于你设置的策略打印警告，而不是强制执行它们。
- `SELinux 策略类型` `SELinux Policy Type` —— `SELINUXTYPE` 变量指示要使用的策略类型。`SELINUX=targeted` 仅保护选定的网络守护进程（如位于 `/etc/selinux/targeted` 目录中的文件所设置的那样）。

就大多数实际用途而言，如果使用 SELinux，你希望启用 SELinux 面向目标策略（这是默认策略）。虽然面向目标策略并未锁定 SELinux 下的所有 Fedora 组件，但它确实锁定了最容易受到攻击影响、最需保护的那些守护进程。标准的 Linux 安全机制保护操作系统中的其他所有内容。

##### 检查 SELinux 状态

您可以重写默认设置，通过在启动 Fedora 时从 GRUB 屏幕的内核行末尾添加以下内容，在 Linux 引导提示符下将 SELinux 置于宽容模式：

```bash
setenforce 0
```

在 SELinux 处于宽容模式（`setenforce 0`）下，您仍然可以登录并使用系统，任何潜在的毁灭性权限失败只会导致错误消息。如果 SELinux 处于宽容模式，您也可以在启动提示符下输入 `setenforce 1` 将 SELinux 返回到强制模式。您可以使用 SELinux 管理窗口永久更改 SELinux 状态。

##### 检查 SELinux 状态

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
/sbin/mingetty			system_u:object_r:getty_exec_t:s0
/usr/sbin/sshd			system_u:object_r:sshd_exec_t:s0
/lib/libc.so.6			system_u:object_r:lib_t:s0 ->
					system_u:object_r:libc_t:s0
/lib/ld-linux.so.2		system_u:object_r:lib_t:s0 -->
					system_u:object_r:ld_so_t:s0
```

按空格键分页浏览输出。除了显示 SELinux 已启用并正在强制模式外，此输出还显示了已设置的处理上下文和文件上下文。

要从图形界面查看和更改基本 SELinux 设置，您可以打开 SELinux 管理窗口。从 GNOME 桌面，选择“系统 $\rightarrow$ 管理 $\rightarrow$ SELinux 管理”。从该窗口中，您可以设置 SELinux 是禁用、强制还是宽容。您还可以选择要使用的 SELinux 策略（默认是 targeted）。

更改策略类型或将 SELinux 服务从关闭改为打开需要您重新标记整个文件系统。不应轻易更改策略。如果您决定通过 SELinux 管理窗口更改策略，该更改也需要重新标记文件系统。通过此窗口更改策略后，下次重启计算机时文件系统将自动重新标记（或者您可以选择复选框以阻止下次重启时重新标记文件系统）。

> 注意：重新标记文件系统可能是一个漫长且耗时的活动。请记住，更改策略是对操作系统的一项重大更改。文件系统中的节点越多，下次启动计算机时重新标记文件系统所需的时间就越长。

您可以使用带有 `-Z` 选项的 `id` 命令来检查您操作的安全性上下文。以下示例显示您当前的上下文是 root 用户，您的角色是 `$system_r$` 角色，类型是 `$unconfined_t$`。

```bash
# id -Z
unconfined_u:unconfined_r:unconfined_t:s0:c0,c1023
```

SELinux 能够产生大量错误消息。默认情况下，这些消息被重定向到 `/var/log/messages` 文件。

#### 使用 SELinux

虽然 SELinux 支持许多高级功能，例如分类（对仅某些部门可用的资源进行分类）和多级安全性（MLS）以实现受限信息流（机密、绝密），但系统管理员通常只关注域和上下文类型隔离。Fedora 在使 SELinux 可用于典型的 Fedora 服务器和桌面方面取得了巨大进步。如果您安装了 `setroubleshoot`，当发生 SELinux 强制执行时，将通过 GUI 和 `/var/log/messages` 通知您，并提供有关如何启用被拒绝的特定访问的提示。

大多数 GNU 实用程序已修改以接受 `-Z` 选项，以查看进程域（`ps -eZ`）、文件（`ls -Z`）等。如果您认为 SELinux 拒绝了您对特定资源的访问，例如通过 Apache 运行的 PHP 脚本，运行 SELinux 管理 GUI 将允许您设置布尔值以关闭特定守护程序或该守护程序特定功能的 SELinux。

以下是在典型服务器上使用 SELinux 的一些快速示例：

```bash
setsebool -P httpd_enable_homedirs on # 允许 Apache 读取用户主目录
restorecon -r /var/www/html # 通过咨询上下文数据库重置文件上下文
chcon -t public_content_rw_t /var /http/incoming # 手动设置文件上下文
```

您可以使用 `sesearch` 命令按如下方式探索当前加载的 SELinux 策略：
