
# 备份入门 (101)

本章标题为“备份入门 (101)”的章节介绍了备份的基本概念，其中许多概念对于家庭使用来说似乎并不实际。它们是否真的不实际取决于你想要通过备份解决的问题。如果你最感兴趣的是保护自己不受磁盘故障或意外删除正在工作的关键文件的影响，你可能不需要担心存档和增量备份——将文件和目录备份到 CD-R 或 DVD 的定点备份（spot backups）可能足够了。同样，如果你不需要从任何时间点恢复任何文件，而只需要文件的最新副本，那么对想要备份的目录进行定点备份可能足够了，频率随你觉得舒服即可。如果你不担心在房子或公寓被毁时丢失所有数据，那么你就不需要担心异地备份（offsite backups）等问题。

底线是我无法告诉你什么让你舒服——这取决于你个人，并定义了你的备份策略。接下来的章节将重点介绍如何使用本章前面提到的某些工具（甚至是 Linux `cp` 命令）来创建重要文件的备份副本。

# 使用 tar 存档和恢复文件

`tar` 程序是最古老、最经典的 Linux/UNIX 工具之一。尽管它可以写入备份设备（如磁带驱动器），但 `tar` 命令通常用于创建可以与其他共享的归档文件、源代码。使用 `tar` 命令创建的归档文件通常具有 `tar` 扩展名。GNU `tar` 命令（Ubuntu 及所有其他 Linux 系统上的 `tar` 版本）提供了内置压缩功能，能够动态压缩归档。压缩后的归档通常具有文件扩展名 `.tgz`，表示它们使用 `gzip` 程序进行压缩（并可以解压），或具有扩展名 `.tar.bz`，表示它们使用 `bzip2` 程序进行压缩（并可以解压）。使用 `tar` 工具产生的归档文件被称为 tar 包（tarballs）。

（注：原文文本中存在大量重复内容，此处已根据逻辑流进行合并整合翻译）

## 第 28 章：备份与还原文件

传统的 Linux/UNIX `cp` 命令提供了许多选项，可以轻松地创建指定目录的副本，并在随后仅更新已更新或在副本中尚不存在的文件。例如，要将 `/home` 下的所有目录备份到挂载在 `/media/LACIE` 的远程驱动器（LACIE 是一个流行的预装 USB 硬盘制造商），你可以使用如下所示的命令：

```bash
$ sudo cp -dpuvx /home /media/LACIE/home
```

此命令中的 `cp` 选项具有以下含义：

- `d`: 不引用符号链接，而是将它们作为符号链接进行复制，而不是复制它们所指向的文件。
- `p`: 保留副本中原始文件的模式和所有权。
- `r`: 递归地复制指定的目录。
- `u`: 仅当原始文件比现有副本新，或者不存在副本时才复制。
- `v`: 显示每个被复制文件的信息。（你可能不想使用这个选项，但它很有趣，在你第一次使用它时是如此。）
- `x`: 不跟随挂载点到其他文件系统。

运行此命令后，你将在系统的 `/media/LACIE/home` 目录中拥有 `/home` 下每个目录的副本。然后你可以断开远程驱动器并将其存放在安全的地方（最好是异地）。每当你想更新备份时，只需取出驱动器并随时重新运行此命令即可更新该副本。

## 使用 rsync 创建远程目录的最新副本

如前所述，`rsync` 是一种常用的命令行实用，允许你将文件推送到远程系统或从远程系统拉取。在向这些系统的目录推拉文件之前，必须在远程系统上配置 `rsync` 程序。

要在 Ubuntu 系统上使用 `rsync`，你必须先启用它，让系统启动 `rsync` 作为后台进程，然后修改 `rsync` 配置文件，为你想要能够远程读写的特定目录添加条目。要启用 `rsync`，请使用你喜欢的文本编辑器编辑 `/etc/default/rsync` 文件，并使用如下命令：

```bash
$ sudo emacs /etc/default/rsync
```

在包含 `RSYNC_ENABLE` 的行中，将 `false` 改为 `true`，然后保存更新后的文件。接下来，在实际启动 `rsync` 守护进程之前，创建 `rsync` 配置文件。

第三部分：Ubuntu 系统管理员

### 注意

大多数 Linux 系统使用如 `inetd` 或 `xinetd` 等 Internet 服务管理器来管理 `ftp`、`tftp`、`rsync` 和 `vnc` 等按需服务的传入请求。这些 Internet 服务管理器会在接收到传入请求时自动启动相应的守护。虽然 Ubuntu 仓库中提供了这些 Internet 服务管理器，但它们默认并未安装。在 Ubuntu 系统上，`rsync` 守护进程的特定系统启动文件位于 `/etc/init.d/rsync`。如果你选择安装 `xinetd` 并用它来管理 `rsync` 请求，你希望禁用此文件并创建 `/etc/xinetd/rsync` 文件，以确保你的系统启用了 `rsync` 服务。

`/etc/default/rsync` 文件决定是否启用 `rsync`。`rsync` 本身的实际配置信息存储在 `/etc/rsyncd.conf` 文件中，该文件在 Ubuntu 系统上不存在。要创建此文件，请使用你喜欢的文本编辑器和如下命令：

```bash
$ sudo emacs /etc/rsyncd.conf
```

一个最小的 `rsync` 配置文件（包含同步你系统中 `/home` 下目录的定义）看起来如下：

```ini
[homes]
path = /home
comment = Home Directories
auth users = root
secrets file = /etc/rsyncd.secrets
transfer logging = true
log format = %h %f %l
log file = /var/log/rsyncd.log
hosts allow 192.168.6.0/24
```

该文件的第一部分设置了 `rsync` 守护进程运行方式的参数：`rsync` 守护进程以 `(uid)` 身份运行，记录所有传输（transfer logging），使用特定的日志格式（log format）并允许来自子网上任何 IP 地址的访问（hosts allow）。第二部分识别每个可同步实体，此处 `home maps` 映射到该系统上的 `/home` 目录。同步由用户完成，该用户的密码必须在 `/etc/rsyncd.secrets` 文件中提供。

保存此文件后，使用 `sudo` 命令和你喜欢的文本编辑器使用如下命令创建 `/etc/rsyncd.secrets` 文件：

```bash
$ sudo emacs /etc/rsyncd.secrets
```

此文件应包含 `/etc/rsyncd.conf` 文件中每个 `auth users` 的条目，如下：

```text
root:your_password
```

（注：此处为示例补充，实际应根据配置设置）

# 第 28 章：文件的备份与恢复

有关 BackupPC 的更多信息，您可以加入通过 SourceForge BackupPC 网站提供的各种邮件列表列表。这些列表如下：

- `backuppc-announce`: 一个低流量的列表，用于发布新版本的公告（http://lists.sourceforge.net/lists/listinfo/backuppc-announce）
- `backuppc-devel`: BackupPC 开发人员的邮件列表（http://lists.sourceforge.net/lists/listinfo/backuppc-devel）
- `backuppc-users`: 标准邮件列表，您可以在此提问和回答关于使用 BackupPC 的问题（http://lists.sourceforge.net/lists/listinfo/backuppc-users）

# 安装与配置 BackupPC

像 BackupPC 这样的专用备份解决方案不会作为 Ubuntu 安装的一部分进行安装，因为对于大多数人来说它们可能大材小用。然而，Ubuntu 上的各种包管理工具可以轻松安装 BackupPC（位于 `backuppc` 软件包中）以及它所需的其他软件包。

由于 BackupPC 使用基于 Web 的界面，它要求您在系统中安装（并配置）Web 服务器，最好是 Apache。同样，BackupPC 可以接收各种相关事件的电子邮件通知，它需要一个邮件传输代理（MTA）。如果系统中尚未安装 MTA，安装 `backuppc` 软件包将安装 `exif`，就 MTA 而言，这并不是我的个人选择。如果您要安装 BackupPC，我建议安装（并配置）Postfix，如第 30 章“设置邮件服务器”所述。在完成操作后，BackupPC 将检测到系统中已安装 MTA，且不再尝试安装依赖项。

一旦软件包在您的系统中安装完成，您的包管理软件将运行其配置脚本。在此阶段，各种包管理器会询问您正在使用哪种 Web 服务器配置，以便您恰当地配置 backuppc，并自动运行脚本来设置您将用于通过 Web 服务器访问 backuppc 的初始账户。此过程将显示类似于图 28-2 所示的对话框，该框向您显示基于 Web 的 BackupPC 界面的初始设置。
