
你的企业 Linux 操作系统安装程序可能已经为你设置了 POP3。在启动 POP3 之前，你应该使用你喜欢的包管理器查询 POP3 是否已经安装。

Red 将 IMAP4 和 POP3 软件捆在一起。当你查询 RPM 数据库获取 POP3 时，你需要在 IMAP 名称下查找它：

```
root@main# rpm -q imap
```

# 第四部分：配置您的企业 Linux 互联网服务

## 配置 IMAP

要配置 IMAP4，你遵循与 POP3 相同的步骤：

1. 安装包含 IMAP4 守护进程的包。
2. 编辑文件 `/etc/xinetd.d/imapconf` 使 IMAP4 服务可用。对于此文件，使用你喜欢的文本编辑器更改该行：

```
disable = yes
```

3. 在命令行提示符处输入以下命令重启 xinetd 守护进程，使步骤 2 中的更改生效：

```
Service xinetd restart
```

4. 检查 IMAP 守护进程是否接受连接。你可以 telnet 到你自己的计算机的 143 端口（所示），以查看 IMAP4 是否接受连接：

```
try@main# telnet localhost 143
trying 127.0.0.1...
telnet:Connected to localhost.
esc character is '.'.
OK localhost IMAP4rev1 v1.26 server ready
```

## 设置别名

要在别文件中创建条目，使用你喜欢的编辑器。每个条目由用户名、冒号、空格和实际地址组成。例如：

```
user: user@example.com
```

保存文件后，运行 `newaliases` 来更新二进制文件。Sendmail 查看 `/etc/aliases.db`。要运行 `newaliases`，在命令行提示符处输入：

```
root@main# newaliases
```

输出应该类似于：

```
newaliases: /etc/aliases.db created
```

如果你想删除别名，只需从文件中删除该行并再次运行 `newaliases`。如果你想更改别名，更改文件中的该行并再次运行 `newaliases`。

## 分发列表

别名文件还可以用于创建分发列表。分发列表是一组接收相同邮件的地址。例如：

```
team: user1@example.com, user2@example.com, user3@example.com
```

当邮件被发送到 `team@` 时，Sendmail 将其递送到列表中的所有地址。

### 第 13 章：配置和管理电子邮件服务器

垃圾邮件（Spamming）是轰炸的一种变。垃圾邮件发送者向许多用户（数百上万）发送垃圾邮件。你可以很容易无意中成为垃圾邮件发送者：例如，如果你选择了邮件的“回复所有”功能并向全球邮件列表发送回复，你就是一个垃圾邮件发送者。

欺骗（Spoofing）是指有人从假地址向你发送电子邮件。如果你认为欺骗对你来说不是大问题，请考虑以下场景：你收到一封系统管理员的邮件，告诉你要出于安全考虑使用特定的密码。当然，许多人会遵守，因为系统管理员最清楚。想象一下，如果伪装者从系统管理员的邮件地址向计算机上的所有用户发送这封邮件会有什么后果。突然之间，伪装者知道了每个人的密码，并可以访问私人和可能敏感的数据。

之所以能够欺骗，是因为 SMTP 不具备身份验证功能。没有身份验证功能，SMTP 无法确定邮件确实来自其声称的地址。如果你的服务器启用了对 SMTP 端口的连接，任何稍微了解 SMTP 工作原理的人都可以连接它并从伪造的地址发送你的电子邮件。除了连接到站点的 SMTP 端口外，用户还可以通过修改浏览器界面来伪造电子邮件。

如果有人入侵了你的邮件系统，你应该向计算机应急响应小组（CERT）报告此次入侵。你可以在 `www.cert.org` 找到 CERT。

#### 一些 SMTP 注意事项

专用邮件服务器。首先，将易受基于 SMTP 攻击的计算机数量减少到最低。根据你组织的规模，只保留一个或几个集中邮件服务器。

只允许来自你防火墙外部的 SMTP 连接到这几个邮件服务器。这保护了你网络上的其他计算机。如果你的站点遭受了垃圾邮件攻击，你只需要清理邮件服务器，而网络中的其他计算机是安全的。

如果你使用包过滤，你只需要配置你的邮件服务器。包过滤根据源和目的地址对数据包进行分析。分析决定是接受数据包并让其通过你的网络，还是将其作为不安全包拒绝。防火墙通常使用包过滤技术，Enterprise Linux 提供了 `iptables` 工具来配置你的包过滤防火墙。

### 第 14 章

#### 配置和管理 FTP 服务器

**本章内容**

- 安装 FTP 服务器
- 配置 FTP 服务器
- 启动和测试 FTP 服务器
- 登录 FTP 服务器

文件传输协议（FTP）是一种 Internet 协议，不仅可以跨 Internet 传输文件，还可以用于本地网络。如果你从网站上下载过文件，你很可能使用了 FTP 来下载该文件。FTP 在你的系统中很容易安装和配置。在本章中，我将向你展示如何安装和配置 FTP 服务器，以及如何使用 `ftp` 客户端访问 FTP 服务器。

##### 安装 FTP 服务器

Red Enterprise Linux ES 和 AS 包含了 `vsftpd` FTP 服务器。`vsftpd` 被称为“非常安全的 FTP 守护进程”，从设计上说，`vsftpd` 是快速、稳定且安全的 FTP 服务器，能够同时处理大量连接。如果你好奇，守护进程（daemon，发音为 *dee-mon*）是一个监听请求并提供其预期服务的进程。取决于你安装系统时选择的选项，`vsftpd` 服务器可能没有安装。你要做的第一件事是检查安装情况，如下：

- 1. **通过选择 Applications > System Tools > Terminal 打开终端窗口。**
- 2. **在命令提示符处输入 `rpm -q vsftpd`。**

如果已安装了 `vsftpd` 服务器，你会在运行此命令的结果中看到 `vsftpd-<version number>`。如果未安装服务器，你会看到一条信息，说明 `vsftpd` 未安装。

如果你的 `vsftpd` 服务器软件已经安装，请跳到“配置 FTP 服务器”部分。如果服务器未安装，请继续执行第 3 。

- 3. 选择 Applications: System Settings: Add/Remove Applications。

如果你没有以 root 身份登录，将提示你输入 root 密码。会出现“Add or Remove Packages”对话框，如图 14-1 所示。

- 4. 向滚动软件包列表直到在列表中找到 FTP 服务器。勾选名称前面的复选框，然后点击 Update 按钮。

系统会提示你将 Enterprise Linux 安装光盘之一插入光驱驱动器。安装完成后，会弹出“Update Completed”对话框。

- 5. 点击“Update Completed”对话框上的 OK，然后点击 Quit 回到“Add or Remove Packages”对话框。

图 14-1：Add or Remove Packages 对话框。

| Add or Remove Packages | |
|---|---|
| 这些包允许你配置 IMAP 或 Postfix 邮件服务器。 | |
| ☑ Windows File Server [2/2] 详情 | |
| 此包组允许你在 Linux 和 MS Windows/Windows 系统之间共享文件。 | |
| ☑ DNS Name Server [1/1] 详情 | |
| 此包组允许你在系统上运行 DNS 名称服务器 (BIND)。 | |
| ☑ FTP Server [1/1] 详情 | |
| 这些工具允许你在系统上运行 FTP 服务器。 | |
| ☑ SQL: Database Server [2/5] 详情 | |
| 此包组允许你在系统上运行 SQL 服务器。 | |
| ☑ News Server [1/1] 详情 | |
| 允许允许你将系统配置为新闻服务器。总安装大小：2,965 Megabytes |

##### 配置 FTP 服务器

安装 `vsftpd` 服务器后，你就可以准备好配置服务器了。由于没有用于配置 FTP 服务器的图形界面，你需要手动编辑配置文件。安装过程将服务器启动文件和配置文件放在系统的多个位置，如下：

- `/usr/sbin/vsftpd`：FTP 守护进程，即运行 FTP 服务的程序。
- `/etc/rc/init.d/vsftpd`：启动服务器的初始化脚本。
- `/etc/vsftpd/vsftpd.conf`：`vsftpd` 的主配置文件。
- `/etc/vsftpd/ftusers`：不允许使用 FTP 服务的用户列表。
