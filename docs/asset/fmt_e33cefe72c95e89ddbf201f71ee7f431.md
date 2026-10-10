
另一个备选服务器是 `NCPtpd`，可从 `http://www.ncftpd.com` 获取。该服务器独立于 `xinetd`（通常用于启用和启动 `wu-ftp` 服务器）运行，并提供其自身的优化的守护进程。此外，`NCPtpd` 具有在内存中缓存 FTP 服务器目录列表的能力，从而提高了用户获取可用文件和目录列表的速度。尽管 `NcFTPd` 相比 `wu-ftpd` 有许多优势，但 `NcFTPd` 不是 GPL 许可软件，其许可费用根据最大并发服务器连接数收取（51 个或更多并发用户为 199 美元，50 个及以下并发用户为 129 美元，但对于符合合域名的教育机构免费）。由于这种许可限制，`NcFTPd` 未随 Fedora 打包，你不会在书籍 DVD 上找到它。

> 注意
> 不要将 `ncpft` 客户端与 `ncpftpd` 混淆。Fedora 包含的 `ncpft-3.1.7-4` 软件包是客户端软件，是 `ftpd-0.17-22` 的替代品，并包含了 `ncpftget` 和 `ncftput` 命令，用于通过命令行或远程文件资源定位地址传输文件。`ncpft` 是 FTP 服务器，可以从 `www.ncpftpd.com` 下载。

另一个 Linux FTP 服务器软件包是 `ProFTPd`，受 GNU GPL 许可。该服务器与许多 Linux 发行版配合，并已被许多 Linux 服务器使用，包括 `ftp.kernel.org` 和 `ftp.sourceforge.net`。`ProFTPd` 正在被活跃维护和更新，以修复漏洞并增强安全性。其开发者建议你使用最新版本（编写时为 `1.2.10`）以避免利用和漏洞风险。访问：`http://www.proftpd.org` 下载副本。

另外一个 FTP 服务器软件包是 `Bsftpd-ss1`，它基于 BSD `ftpd` 并根据 BSD 许可分发。`Bsftpd-ss1` 通过安全扩展提供同时的标准访问和安全访问；安全访问需要特殊的客户端。更多详细信息，请访问：`#bsdftpd-sscl.sc`。

最后，另一种替代方案是使用 Apache 和 HTTP 协议进行服务。使用 Web 服务器提供数据下载可以减少在服务器上监控和维护单独软件服务（或目录）的需求。这种提供文件的方法还减少了资源需求，并为远程用户下载时提供了更好的灵活性（例如允许他们一次下载多个文件）。有关 Apache 的更多信息，请参阅第 17 章“Apache 服务器管理”。

# 安装 FTP 软件

作为工作站安装的一部分，FTP 客户端软件已经安装。你可以使用查询中的 RPM、`grep` 和 `sort` 命令验证系统中是否安装了 FTP 相关软件：

```bash
$ rpm -qa | grep ftpd | sort
```

示例结果可能取决于安装了哪些软件包。你的 Fedora 文件系统中，`/usr/bin/pftp` 链接到 `/usr/bin/ftp`，而 `vsftpd` 服务器位于 `/usr/sbin` 目录。匿名 FTP 目录位于 `/var/ftp` 目录下。其他安装的软件包包括额外的文本和图形界面 FTP 客户端。

如果未安装 `vsftpd`，你可以在“添加/删除应用程序”对话框的“FTP 服务器”找到它。

> 注意
> 如果你有一个连接互联网的 FTP 服务器，请养成检查 Fedora 网站 `http://fedora.redhat.com` 的习惯，获取最新的系统错误说明和安全漏洞修复。

# 448 第 20 章 使用 FTP 进行远程文件服务

由于 FTP 编写于加密和安全需求之前，它没有提供发送加密密码的机制。账户信息以明文发送到 FTP 服务器上；具有足够知识的网络嗅探器可以找到你连接到服务器的密码。许多站点使用匿名 FTP 服务器来防止普通账户密码在互联网上传输。如果你有一个连接互联网的 FTP 服务器，请养成检查 Fedora 网站 `http://fedora.redhat.com` 的习惯，获取最新的系统错误说明和安全漏洞修复。`shadow` 文件（在 20.1 中仅显示了部分）包含了 `/passwd` 文件未找到的额外信息，如账户过期、密码过期、账户是否被锁定。密码字段中的 `*` 表示该账户无法登录。

# 20.1 Shadow 文件用户条目

在 Fedora 安装后，`shadow` 密码看起来如下所示：

```bash
# cat /etc/shadow
ftp:*:19999:0:99:/var/ftp:/sbin/nologin
```

## 第 20 章 使用 FTP 提供远程文件服务

![](img/4473647b35365e8747aa8fb2cf969fd5_480_0.png)

图 20.1 以太客户端可以过滤并嗅探 FTP 会话以获取用户名和密码。

## wu-ftpd 的 xinetd 配置

`xinetd`（读音为 "zy-net-d"）是扩展互联网守护进程（Extended Internet services daemon），处理网络服务的连接。`xinetd` 是类似于 `inet` 的工具（用于其他 Linux 发行版和其他 Red Hat 衍生版）的首选替代品。然而，除了相比 `inet` 的几项改进外，`xinetd` 还允许你对 FTP 等守护进程网络请求应用单独的访问策略。

该守护进程控制你系统上的许多服务，允许你在 `/etc/xinetd.d` 目录下的配置文件中设置。本节显示了如何编辑相关文件以启用 `wu-ftpd` 服务器的使用。

## 为 wu-ftpd 服务器配置 xinetd

当你使用 RPM 安装 `wu-ftpd` 时，RPM 包可能包含一个 `xinetd` 文件 `/etc/xinetd.d/wu-ftpd`，如 Linux 20.2 所示。你需要编辑该文件，因为其默认设置禁用了入站 FTP。

> 不要被 `wu-ftpd` 文件的第一行误导。尽管行显示为 `default: no`，但除非你专门进行配置，否则 FTP 服务是关闭的。该行是一行注释，因为它以井号 (`#`) 开头并被 `xinetd` 忽略。FTP 服务是否开启由文本行 `disable = yes` 决定。

## 列表 20.2 用于 wu-ftpd 的 xinetd 配置文件

```
# default: on
# description: The we-ftpd FTP 服务器提供 FTP 连接。它使用 \
# 普通的、未加密的用户名和密码进行身份验证。
service ftp
```

```
{
  disable = yes
    socket_type = stream
    wait = no
    user = root
    server = /usr/sbin/in.ftpd
    server_args = -1 -a
    log_on_success += DURATION
    nice = 10
}
```

使用编辑器将 `disable = yes` 行更改为 `disable = no`。保存文件并退出编辑器。你必须重启 `xinetd`，因为配置文件仅在启动时解析。要以 root 身份重启 `xinetd`，请执行命令 `/etc/rc.d/init.d/xinetd restart`。这将调用在任何级别用于启动或停止 `xinetd` 守护进程（从而启动或关闭系统）的 shell 脚本。`xinetd` 报告其状态如下：

```
# /etc/rc.d/init.d/xinetd restart
Stopping xinetd: [ OK ]
Starting xinetd: [ OK ]
```

完成后，FTP 服务器将对所有入站请求开放。

## 非常可靠的 FTP 服务器 (vsftpd) 软件包

Red Hat Linux 发行版的之前的版本允许你编辑 `/etc/xinetd.d` 目录下的名为 `vsftp` 的文件来启用并启动非常安全的 FTP 服务器 `vsftpd`。在 Fedora 中，你现在只需简单使用 `system-config-services` 客户端或 `service` 命令来启动 `vsftpd`。例如，使用如下 `service` 命令启动服务器：

```
# service vsftpd start
Starting vsftpd: [ OK ]
```

使用 `system-config-services` 客户端或 `service` 命令来启动、停止或重启 `vsftpd` 服务器。不要在系统上同时运行两个 FTP 服务器！

## 提示

你还可以使用 `/etc/rc.d/init.d` 目录下名为 `vsftpd` 的 shell 脚本来启动、停止、重启和查询 `vsftpd` 服务器。你必须有权限使用 `vsftpd` 脚本来控制服务器，但任何用户都可以使用 `status` 关键字来查询服务器（查看其是否运行以及查看其进程 ID）：

```bash
$ /etc/rc.d/init.d/vsftpd status
```

## 配置非常可靠的 FTP 服务器
