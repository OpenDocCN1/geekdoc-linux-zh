
在包含 `RSYNC_ENABLE` 的行中，将 `false` 改为 `true`，然后保存更新后的文件。在启动 rsync 守护进程之前创建 rsync 配置文件。

> 大多数 Linux 系统使用 Internet 服务管理器（如 inetd 或 xinetd）来管理针对 ftp、tftp、rsync 和 vnc 等按需服务的入站请求。Internet 服务管理器在接收到入站请求时会自动启动相应的守护进程。虽然 Ubuntu 仓库中有这些 Internet 服务管理器，但通过编辑 `/etc/init/rsync` 来启动以守护模式运行的 rsync 文件。如果你随后安装了 xinetd 并想通过它管理 rsync 请求，将需要定义此文件并创建 `/etc/xinetd.d/rsync` 以确保你的系统上启用了 rsync 服务。

`/etc/defaults/rsync` 文件决定了是否启用 rsync。rsync 本身的实际配置存储在 `/etc/rsync.conf` 文件中，该文件在 Ubuntu 或 Debian 系统上默认不存在。要创建该文件，请使用你喜欢的文本编辑器和命令：

```bash
$ sudo emacs /etc/rsync.conf
```

一个定义你系统中远程同步 `/home` 目录的最小 rsync 配置文件如下：

```ini
uid = root

transfer logging = true

log format = %H %o %f %b

log file = /var/log/rsync.log

hosts allow = 192.168.2.255/3
```

# 附录章节

```ini
[homes] =
path = /home
comment = Home Directories
auth users = wwh
syncs file = /etc/rsynccd.secrets
```

该文件的第一部分设置了 rsync 守护进程运行的参数。按照顺序，rsync 守护进程以 `(uid)` 身份运行，记录所有传输 `(transfer logging)`，使用特定的日志格式 `(log format)` 和日志文件 `(log file)`，允许来自 192.168.6.0 子网的任何主机 IP 地址的访问 `(hosts allows)`。文件的第二部分识别了一个名为 home 的可同步实体，它映射到该系统上的目录。对或从该目录的同步是以用户 `wwh` 的身份进行的，其密码必须在 `/etc/rsynccd.secrets` 文件中提供。

保存此文件后，使用 `sudo` 命令和你你喜欢的文本编辑器创建 `/etc/rsynccd.secrets` 文件，命令如下：

```bash
$ sudo edit /etc/rsynccd.secrets
```

该文件应该包含 `/etc/rsync.conf` 文件中每个 `auth users` 条目的条目。在这种情况下，此文件中的每个条目包含一个用户名、一个冒号以及该用户的明文密码，如下所示：

`wwh:hellothere`

接下来，保存此文件，并使用如下命令确保你系统上喜欢的用户对该文件只有只读权限：

```bash
$ sudo chmod 600 /etc/rsynccd.secrets
```

你现在可以使用以下命令启动 rsync 守护进程：

```bash
$ sudo /etc/init.d/rsync restart
```

你现在可以使用如下命令在你系统中创建 `/home` 目录的本地副本，其中 `system-name-or-addr` 是配置 rsync 守护进程的系统名称或 IP 地址：

```bash
$ rsync -Havz system-name-or-addr:home /media/LACIE/home
```

此示例中 rsync 命令的参数含义如下：

- `-H`: 如果在复制的任何目录中存在硬链接，则保留它们。
- `-a`: 使用归档模式，保留所有权、符号链接、设备文件等，这本质上是你指定其他选项的快捷方式。
- `-v`: 详细模式，识别每个被复制或被考虑复制的文件。（你可能不想使用此选项，但它很有趣，至少在你第一次运行几次 rsync 时是这样。）
- `-z`: 在传输文件时使用压缩。

# 备份和恢复文件

在本节创建的 `rsync.conf` 文件只是一个最小示例，有关 rsync 可用选项的详情，请查看 rsync 的帮助页。

# 安装和使用 BackupPC

本节介绍了如何安装、配置和使用 BackupPC 来接入各种主机。如果你网络中的机器超过一台，或者你是在企业或学术环境中工作，BackupPC 软件非常值得尝试。其基于 Web 的界面易于设置和使用；各种类型的支持备份易于配置、启动和监控；它可以备份你的 Linux、Windows 和 Mac OS 系统。

# 第四部分 附录章节

尽管 backupcc 在备份 Microsoft Windows 和 Mac OS 系统方面表现出色，但你应该注意一些问题。backupcc 并不适用于备份 Windows 系统以进行裸机恢复（bare-metal restore）。backupcc 在 Ubuntu 上使用 `smclient` 应用程序备份 Windows 磁盘，因此它不会保存 ACL（访问控制列表）以及任何由当前运行的 Windows 客户端正在打开的文件（如 Outlook 等许多程序都是如此）。同样，backupcc 不会保留 Mac OS 属性。请检查 http://backupcc.sourceforge.net/faq/limitations.html 以了解使用 backupcc 的当前限制列表。该文档短得令人惊讶！

关于关于 BackupCC 的更多信息，你可以加入通过 SourceForge BackupCC 网站提供的许多邮件列表。这些是以下列表：

- `backupcc-announce`：一个低流量列表，用于发布新版本（http://lists.sourceforge.net/listinfo/backupcc-announce）
- `backupcc-devel`：BackupCC 开发人员的邮件列表。（http://lists.sourceforge.net/listinfo/backupcc-devel）
- `backupcc-users`：你可以在这里提问和回答关于 BackupCC 问题的邮件列表（http://lists.sourceforge.net/listinfo/backupcc-users）

# 安装和配置 BackupCC

像 BackupCC 这样的专用的备份解决方案并不是作为默认 Ubuntu 或 Ubuntu 安装的一部分的，它们对于大多数人来说可能过剩。Ubuntu 和 Ubuntu 系统提供的各种包管理工具可以轻松地安装 BackupCC（位于 `backupcc` 软件包中）以及它所需的软件包。

由于 BackupCC 使用基于 Web 的界面，它要求你的系统中已安装（配置）了 Web 服务器，首选是 Apache。同样，BackupCC 可以为各种备份相关事件发送电子邮件通知，它需要一个邮件传输代理（MTA）。如果你的系统中尚未安装 MTA，可以安装 `exim` 软件包，但就 MTA 而言，这并不是我的个人首选。如果你安装了 BackupCC，我建议按照第 9 章“设置邮件服务器”中的描述安装并配置 Postfix。完成后，BackupPC 将检测到系统中已安装了 MTA，而不再尝试安装它来满足需求。

一旦 `backuppc` 软件包已安装在你的系统上，你的包管理软件将运行其配置脚本。在此阶段，各种包管理器会询问你正在使用哪种 Web 服务器配置，以便它们恰当地配置 backupcc，并自动运行脚本来设置你通过该服务器访问 backupcc 的初始账户。此过程会显示类似于图 B-2 所示的对话框，它会告诉你 Web 版 BackupCC 界面的密码。

此对话框显然适用于每个包管理工具——图 B-2 显示了如果你使用 `aptitude` 管理工具安装 `backupcc` 软件包时会看到的屏幕。有关 Ubuntu 和 Ubuntu 系统可用的各种包管理工具的更多信息，请参阅第 23 章。

一旦看到类似图 B-2 所示的对话框，写下 backupcc 界面的密码并按 Return键或点击“前进”（Forward）继续。除非你擅长记住像“b3j2Byf”这样的密码，否则我建议将默认密码更改为你的管理员密码之一，你可以通过下面的命令来实现（图 B6-2 中的对话框也解释了这一点）：

```bash
sudo htpasswd /etc/backuppc/htpasswd backuppc
```
