
虽然通常不需要重新加载 Samba 守护进程，但你可以使用 `service reload` 来重新加载 Samba 配置文件，而不会影响连接到服务器的客户端。

防火墙：按照第 819 页所示的说明打开服务器防火墙。

打印机：默认的 `smb.conf` 配置文件共享 Samba 服务器上的打印机；不需要配置。

主目录：默认的 `smb.conf` 配置文件共享 Samba 服务器上用户的主目录；不需要配置。

配置：`/etc/sysconfig/samba` 文件导致 `smbd` 和 `nmbd` 分别启动。

# 使用 systemconfig-samba 配置 Samba 服务器

`system-config-samba` 工具（在 RHEL 中不可用）是在你不熟悉 Samba 最佳工具。它执行三个基本功能：配置服务器、配置用户和设置共享。

# SAMBA：Linux 和 Windows 文件共享

![](img/1e024b9f135a8b3cebc6731238212d84_880_0.png)

图 23-2 Samba 用户窗口

要配置服务器，使用 `systemconfig-samba` 显示 Samba 配置窗口（图 23-1）。点击“访问”选项卡，指定要限制访问特定用户还是允许任何人访问此共享。点击确定。

要配置用户，点击“用户”选项卡显示 Samba 用户窗口（图 23-3）。如果用户不存在，点击“添加”。当创建新用户窗口出现时，输入用户名。最后，在两个 Samba 密码框中输入密码。点击确定关闭创建用户窗口，然后点击确定关闭 Samba 用户窗口。

如果你将用户名映射到不同的 Linux 用户，必须在 `/etc/samba/smb.conf`（第 834 页）的 `[global]` 部分添加以下 `username map` 参数（第 838 页）：

```
username map = /etc/samba/smusers
```

Linux 共享：接下来你添加一个*共享*，即从服务器（Linux）系统到客户端（Windows）系统的目录导出。点击工具栏上的加号 (+) 显示创建共享窗口的基本选项卡（图 23-4）。在“文件夹”文本框中，输入要共享的目录的绝对路径（`/tmp` 是一个很好的练习目录）。如果你喜欢，可以输入描述。在这里输入你共享目录的 Linux 主机名和路径可能会用。如果你希望从客户端写入目录，请勾选“可写”复选框；勾选“可见”复选框允许从客户端看到（浏览）该共享。点击“访问”选项卡，指定要限制访问特定用户还是允许任何人访问此共享。点击确定。关闭创建共享窗口。

# 设置 Samba 服务器 829

![](img/1e024b9f135a8b3cebc6731238212d84_881_0.png)

图 23-3 Samba 用户窗口

如果没有 `smb.conf` 中的此行，Samba 将不会查询用户映射文件。

![](img/1e024b9f135a8b3cebc6731238212d84_881_1.png)

图 23-4 创建共享窗口，基本选项卡

# 830 第 23 章 SAMBA：LINUX 和 WINDOWS 文件与打印机共享

你现在应该能够从 Windows 机器（第 825 页）访问该共享了。不需要启动或重启 Samba 服务器。

故障排除：如果服务器运行不正常，请参阅第 840 页的“故障排除”。

## swat: 配置 SAMBA 服务器

为 smb.conf 创建一个副本

> **提示** 按照安装情况，`/etc/samba/smb.conf` 文件包含大量的注释（第 834 页）。`swat` 工具会操作此文件并移除注释。在第一次运行此工具之前，请为 `smb.conf` 备份备用。

`swat` 工具（Samba Web 管理工具，`samba-swat` 软件包）是一个基于浏览器的 `/etc/samba/smb.conf` 文件的图形化编辑器。对于每个可配置的参数，它都提供了帮助链接、默认值和一个用于更改该值的文本框。`swat` 工具设计精良，其 GUI 界面对应于你编辑的 `smb.conf` 文件中的行。你可以使用并学习 `swat`，这样如果你想用文本编辑器修改 `smb.conf`，过渡将非常顺畅。

### 配置 swat

`swat` 工具通过 `xinetd` 运行（`xinetd` 软件包，随 `samba-swat` 安装；第 481 页）。如果你想从本地系统运行 `swat`，请执行以下命令：

```bash
# chkfig swat disable = yes 允许在 /etc/xinetd.d/swat 文件中禁用 no
```

按照下文说明启动或重启 `xinetd` 守护进程。

如果你想从本地系统的其他系统运行 `swat`，必须打开防火墙并编辑 `swat` 文件，以便 `swat` 能够响应远程系统。使用文本编辑器打开 `/etc/xinetd.d/swat`。如有必要，修改 `disable = no` 之后的行。接下来，修改 `_from` 之后的行。在 `默认`状态下，此行仅允许从本地系统（127.0.0.1）访问。在该行中添加你想要访问 `swat` 的其他系统的名称或 IP 地址。用空格分隔系统名称。

```
only_from = 127.0.0.1 172.16.192.150
```

重启 `xinetd` 以重载 `swat` 文件：

```bash
# service xinetd restart [ OK ]
```

重启 `xinetd`（通过 `systemctl`）：

防火墙：如果你从服务器的其他系统运行 `swat` 且该服务运行了防火墙，你必须允许远程系统访问服务器的 901 端口以便其与 `swat` 通信：运行 `swat-config-firewall`，选择 `Other Ports` 标签，并按照第 894 页所示选择 `901 TCP swat`。

现在你应该可以运行 `swat` 了：从本地系统开始，打开浏览器并在地址栏中输入 `http://127.0.0.1:901` 或 `http://localhost:901`。在提示时，输入用户名 `root` 和 root 密码。（如果你提供了 root 以外的用户名，将能够查看配置信息但无法进行更改。从远程系统访问，将 127.0.0.1 替换为服务器的名称或 IP 地址（但不是相邻的安全层）。）

## 设置 SAMBA 服务器

![](img/1e024b9f135a8b3cebc6731238212d84_883_0.png)

## 欢迎使用 SWAT！

请使用其中一个按钮选择配置操作

# Samba 文档

- 守护进程 (Daemons)

  - `smbd` - SMB 守护进程

  - `nmbd` - NetBIOS 命名服务器

  - `winbd` - winbind 守护进程

- 配置文件 (Configuration Files)

  - `smb.conf` - 配置文件

  - `hosts` - hosts 文件

  - `passwd` - 密码文件

- 管理工具 (Administrative Utility)

  - `sambcontrol` - Samba 控制

  - `swat` - Samba 工具

## 不允许加密的访问

如果你从服务器的其他系统运行 `swat` 且该服务运行了防火墙，你必须允许远程系统访问服务器的 901 端口以便其与 `swat` 通信：运行 `swat-config-firewall`，选择 `Other Ports` 标签，并按照第 894 页所示选择 `901 TCP swat`。

现在你应该可以运行 `swat` 了：从本地系统开始，打开浏览器并在地址栏中输入 `http://127.0.0.1:901` 或 `http://localhost:901`。在提示时，输入用户名 `root` 和 root 密码。（如果你提供了 root 以外的用户名，将能够查看配置信息但无法进行更改。从远程系统访问，将 127.0.0.1 替换为服务器的名称或 IP 地址（但不是相邻的安全层。）

## 不允许从远程系统访问

如果你无法再使用 `swat`，你可能错误地更改了 `hosts allow`。在这种情况下，你需要手动编辑 `/etc/samba/smb.conf` 并修复包含 `hosts allow` 的行：

```bash
$ grep hosts smb.conf
hosts allow = 127.0.0.1, 172.16.192.150
hosts deny = ALL
```

前面的条目允许从本地系统访问，并在页面底部出现几个框（图 23-7）。这样你允许 `swat` 工作。在更改 `smb.conf` 后不需要重启 Samba。
