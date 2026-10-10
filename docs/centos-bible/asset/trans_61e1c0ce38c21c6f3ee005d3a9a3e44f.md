
## SELinux 故障排除工具
- **SELinux 故障排除工具** — 当 SELinux 检测到违反 SELinux 策略的行为时，SELinux 故障排除工具会在桌面面板中启动一个图标。点击该图标将显示 setroubleshoot 浏览器窗口，以便查看问题的描述和潜在的修复方法。你还可以通过选择“应用程序 > 系统工具 > SELinux 故障排除工具”直接启动 setroubleshoot 浏览器。

## SELinux 管理窗口
- **SELinux 管理窗口** — 打开 SELinux 管理窗口（选择“系统 > 管理 > SELinux 管理”）以更改 SELinux 的状态（启用、禁用或执行）或更改默认的策略类型（默认为定向）。你还可以修改用户、文件和目录、策略模块以及网络端口的 SELinux 设置。

## SELinux 命令
- **SELinux 命令** — 可以使用一组命令行工具来修改 SELinux 策略。这些命令包括 `chcon`（用于标记文件和目录）和 `setsebool`（用于开启和关闭 SELinux 属性）。要了解特定守护进程在 SELinux 中的处理方式，请参考各种 SELinux 策略手册页（`fipd_selinux`、`httpd_selinux`、`kerberos_selinux`、`named_selinux`、`nfs_selinux`、`nis_selinux`、`rsysnd_selinux` 和 `ypbind_selinux`）。

# 在 CentOS 中使用 SELinux

如果你使用的是定向 SELinux 策略（随系统默认提供并启用），你仍然可以像往常一样管理 Linux。以下程序描述了使用 SELinux 所需的软件包，并帮助你开始使用默认的定向策略。如果需要更多信息，请访问 [http://selinuxproject.org/page/Main_Page](http://selinuxproject.org/page/Main_Page) 查找大量有用的 SELinux 文档。

# SELinux

对 SELinux 的支持已内置于 Linux 2.6 内核中。实际上，SELinux 在最新版本的 CentOS 中是默认启用的。如果你更喜欢关闭 SELinux，在启动桌面后，你可以打开 SELinux 管理窗口（选择“系统 > 管理 > SELinux 管理”）并将“当前执行状态”设置为“宽容”。宽容模式会导致 SELinux 检查并记录 SELinux 本应失败的地方，但实际上不会阻止操作。

在启用 SELinux 的情况下，你可能还需要安装以下软件包：

- **checkpolicy** — 包含名为 `checkpolicy` 的 SELinux 策略编译器。使用此包来构建或检查 SELinux 的策略。使用 `checkpolicy`，你可以从策略配置文件和策略.conf 文件中的参数创建二进制策略文件。（输入 `man checkpolicy` 以阅读关于 `checkpolicy` 的信息。）
- **libselinux** — 包含 SELinux 应用程序的应用程序编程接口。它包括应用程序程序用于检查 SELinux 状态的组件。
- **policycoreutils (以及 policycoreutils-gui)** — 包含操作 SELinux 系统所需的基本实用工具。命令包括 `fixfiles`（用于检查并可能纠正文件系统上的安全属性）、`restorecon`（用于为选定文件设置安全属性）、`audit2allow`（用于将 `/var/log/messages` 中的消息转换为 SELinux 可使用的规则）、`newrole`（用于在新角色中打开 shell）、`load_policy`（用于加载策略文件）、`run_init`（用于使用正确的上下文运行 init 脚本）、`sestatus`（用于检查 SELinux 当前是否启用）以及 `setfiles`（用于设置文件的安全上下文）。
- **selinux-policy-mls** — 包含 SELinux 的多级安全翻译表。
- **selinux-policy-targeted** — 包含用于将定向 SELinux 策略合并到运行中的 Linux 系统中的示例策略文件，以及使运行时更改 SELinux 所需的上下文文件和 `bool` 工具文件。
- **setools** — 包含用于管理运行策略中定义用户对 Linux 系统不同组件的访问权限的工具。

# 检查 SELinux 是否开启

安装 CentOS 后，你可以检查 `/etc/selinux/config` 文件（该文件链接到 `/etc/sysconfig/selinux`）以查看 SELinux 是否已启用，以及如果启用了，哪些策略正在生效。对于配置为使用 SELinux 的 CentOS 系统，该文件设置两个关键变量：

- **SELinux 状态** — `SELINUX` 变量设置 SELinux 的状态。如果在 CentOS 安装期间启用了 SELinux，则初始值为 `SELINUX=enforcing`（这将强制实施 SELinux 的安全策略）。如果在安装期间禁用了 SELinux，则相反设置为 `SELINUX=disabled`。第三种选择是设置 `SELINUX=permissive`，这将根据你设置的策略打印警告，而不是强制执行它们。
- **SELinux 策略类型** — `SELINUXTYPE` 变量指示要使用的策略类型。`SELINUXTYPE=targeted` 仅保护选定的网络守护进程（如在 `/etc/selinux/targeted` 目录中的文件所设置的那样）。

对于大多数实际用途，如果使用 SELinux，你可能希望启用 SELinux 定向策略（这是默认的）。虽然定向策略并未将 CentOS 的所有组件都置于 SELinux 的锁定之下，但它确实锁定了对保护攻击最为关键的守护进程。标准 Linux 安全保护操作系统中的其他所有内容。

你可以通过在启动 CentOS 时在 GRUB 屏幕的内核行末尾添加以下内容，在 Linux 启动提示符下覆盖默认设置，将 SELinux 置于宽容模式：

```bash
setenforce 0
```

当 SELinux 处于宽容模式（`setenforce 0`）时，你仍然可以登录并使用系统，任何潜在的严重权限失败只会导致错误消息。

# 理解系统管理

如果 SELinux 处于宽容模式，你同样可以通过在启动提示符下输入 **setenforce 1** 将 SELinux 返回到执行模式。你可以使用 SELinux 管理窗口永久更改 SELinux 状态。

# 检查 SELinux 状态

有许多工具可用于检查你的 CentOS 系统中 SELinux 的状态。要检查 SELinux 是否已启用，请输入以下命令：

```bash
# sestatus -v
SELinux status:                   disabled
```

输出表明当前系统未强制执行 SELinux。如果将 SELinux 设置为宽容模式，输出将更接近以下内容：

```
SELinux status:                   enabled
SELinuxfs mount:                  /selinux
Current mode:                     enforcing
Mode from config file:            enforcing
Policy version:                   21
Policy from config file:          targeted
```

要从图形界面查看和更改基本 SELinux 设置，你可以打开 SELinux 管理窗口。从 GNOME 桌面，选择“系统 ➣ 管理 ➣ SELinux 管理”。从该窗口，你可以设置 SELinux 是禁用、执行还是宽容。你还可以设置要使用的 SELinux 策略（定向是默认值）。

更改策略类型或将 SELinux 服务从关闭改为开启，还需要重新标记整个文件系统。切勿轻率地更改策略。如果你确实决定通过 SELinux 管理窗口更改策略，该更改也需要重新标记文件系统。通过此窗口更改策略时，下次重新启动计算机时文件系统会自动重新标记（或者你可以选择复选框以防止在下次重启时重新标记文件系统）。

> 重新标记文件系统可能是一个漫长且耗时的活动。请记住，更改策略是对操作系统的主要更改。文件系统中的节点越多，下次启动计算机时重新标记文件系统所需的时间就越长。

你可以使用带有 `-Z` 选项的 `id` 命令来检查你正在操作的安全上下文。以下示例显示你当前的上下文是 `root` 用户，你的角色是 `system_r_role`，类型是 `unconfined_t`。

```bash
# id -Z
unconfined_u:unconfined_r:unconfined_t:s0-s0:c0.c1023
```

SELinux 能够产生大量的错误消息。默认情况下，这些消息被重定向到 `/var/log/audit/audit.log` 文件。由于该文件包含来自许多不同服务的消息，你可以使用 seAudit 窗口（在终端窗口中输入 `seaudit`）来查看严格与 SELinux 相关的消息。
