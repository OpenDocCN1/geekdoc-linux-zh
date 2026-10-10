
如果未安装 vsftpd，您可以在“添加/删除应用程序”对话框中的“FTP 服务器”下找到它。

> **注意**
> 如果您托管连接到互联网的 FTP 服务器，请养成习惯，始终访问 Fedora 网站 http://fedora.redhat.com，以获取最新的系统勘误以及服务器软件的安全修复和 bug 修复。

由于 anonftp 和 wu-ftpd RPM 软件包不包含在 Fedora 中，如果您想使用 wu-ftpd 服务器，必须下载并安装它们。从 http://www.wu-ftpd.org/ 获取适用于 Linux 的最新软件包，以从最新源代码进行构建，或从受信任的镜像站点获取 RPM 软件包。

## FTP 用户

安装 Fedora 后，会创建一个 FTP 用户。该用户本身不是普通用户，而是匿名 FTP 用户的名称。`/etc/passwd` 中的 FTP 用户条目如下所示：

`ftp:x:14:50:FTP User:/var/ftp:/sbin/nologin`

> **注意**
> 此处讨论的 FTP 用户适用于匿名 FTP 配置和服务器设置。
>
> 另外，请注意，其他 Linux 发行版可能会使用不同的默认目录（例如 /usr/local/ftp）来存储 FTP 文件和匿名用户。

此条目遵循标准的 `/etc/passwd` 条目格式：用户名、密码、用户 ID、组 ID、注释字段、主目录和 shell。要了解有关 /etc/passwd 的更多信息，请参阅第 10 章“管理用户”中的“密码文件”一节。该条目中的各项由冒号分隔。在上面的示例中，可以看到托管服务器的 Fedora 系统使用影子密码，因为传统密码字段中存在 `x`。影子密码系统很重要，因为它为 Fedora 提供了额外的安全级别；影子密码系统通常在 Fedora 安装过程中安装。

FTP 服务器软件使用此用户帐户来分配连接到服务器的用户的权限。通过为匿名 FTP 用户使用默认 shell `/sbin/nologin`（而不是 `/bin/bash` 或其他标准交互式 shell），该软件使这些用户无法作为常规用户登录。`/sbin/nologin` 不是一个 shell，而是一个通常分配给已锁定帐户的程序。作为 root 检查 `/etc/shadow` 文件（参见列表 20.1）显示，无法登录此帐户，这由使用 `*` 作为密码来表示。

**列表 20.1 影子密码文件中的 ftp 用户条目**

```bash
# cat /etc/shadow
bin:*:11899:0:99999:7:::
daemon:*:11899:0:99999:7:::
adm:*:11899:0:99999:7:::
lp:*:11899:0:99999:7:::
...
ftp:*:12276:0:99999:7:::
...
```

影子文件（列表 20.1 仅显示了其中的一部分）包含标准 `/etc/passwd` 文件中没有的额外信息，例如帐户过期时间、密码过期时间、帐户是否被锁定以及加密密码。密码字段中的 `*` 表示该帐户不是标准登录帐户；因此，它没有密码。

虽然系统中正在使用影子密码，但使用 FTP 时密码并未以安全方式传输。由于 FTP 是在加密和安全需求出现之前编写的，它不提供发送加密密码所需的机制。在 FTP 服务器上，帐户信息以纯文本形式发送；任何具备足够技术知识和网络嗅探器的人都可以找到您在服务器上连接的帐户的密码。许多站点专门使用仅限匿名的 FTP 服务器，以防止普通帐户密码通过互联网传输。图 20.1 显示了 ethereal 捕获的一个 FTP 会话的部分内容，可以看到它捕获了一个用户的密码以明文形式发送。ethereal 客户端是一个图形浏览器，用于实时显示网络流量，可用于监视数据包数据，例如局域网上的 FTP 登录。

## 快速且粗糙的 FTP 服务

负责任的 Linux 管理员会花时间仔细安装、设置和配置生产 FTP 服务器，然后才提供公共服务或在互联网上开展业务。然而，您可以通过遵循几个简单步骤，在安全的 LAN 上快速设置服务器：

- 确保已安装 FTP 服务器 RPM 软件包，已启用网络连接，且服务器上的防火墙规则允许 FTP 访问。请参阅第 14 章“网络”，了解如何使用 Red Hat 的 *system-config-securitylevel* 客户端进行防火墙设置。
- 如果需要匿名访问服务器文件，请填写 `/var/ftp/pub` 目录。通过在此目录挂载或复制内容（如目录和文件）来完成此操作。
- 编辑并保存适当的配置文件（例如 `vsftpd` 的 `vsftpd.conf`）以启用访问。
- 如果您使用的是 `wu-ftpd`，必须像这样启动或重启 `xinetd`：`/etc/rc.d/init.d/xinetd restart`。如果您使用的是 `vsftpd`，必须像这样启动或重启服务器：`service vsftpd start`。

![](img/34e72348d53ca54c2a1d9c871316691b_479_0.png)

**图 20.1 ethereal 客户端可以过滤和嗅探 FTP 会话，以捕获用户名和密码。**

## wu-ftpd 的 xinetd 配置

xinetd（读作“zy-net-d”）是扩展互联网服务守护程序，处理网络服务的传入连接。xinetd 是类似工具（用于其他 Linux 发行版和旧版 Red Hat 发布版本）inetd 的优选替代方案。然而，除了对 inetd 的一些小改进外，xinetd 还允许您对不同的网络连接请求（如 FTP）应用单独的访问策略。该守护程序根据 `/etc/xinetd.d` 目录下配置文件中的设置控制系统中的多项服务。本节介绍如何编辑适当的文件以启用 wu-ftpd FTP 服务器的使用。

### 为 wu-ftpd 服务器配置 xinetd

当您使用 RPM 安装 wu-ftpd 时，RPM 软件包可能包含一个 xinetd 配置文件 `/etc/xinetd.d/wu-ftpd`，如列表 20.2 所示。您需要编辑该文件，因为其默认设置禁用了传入的 FTP 请求。

> **注意**
>
> 不要被 wu-ftpd 文件文本的第一行混淆。尽管该行写着 `default: on`，除非您专门配置其使用，否则 FTP 服务是关闭的。该行是一个注释，因为它以井号（`#`）开头，会被 xinetd 忽略。FTP 服务是否开启由文本行 `disable = yes` 决定。

**列表 20.2 wu-ftpd 的 xinetd 配置文件**

```text
# default: on
# description: The wu-ftpd FTP server serves FTP connections. It uses \
# normal, unencrypted usernames and passwords for authentication.
service ftp
{
	disable	has
	sock	_type	=	stream
	wait	=	no
	user	=	root
	server	=	/usr/sbin/in.ftpd
	server_args	=	-1 -a
	log_on_success	+=	DURATION
	nice	=	10
}
```

使用编辑器将 `disable = yes` 行更改为 `disable = no`。保存文件并退出编辑器。然后必须重启 xinetd，因为配置文件仅在启动时解析。作为 root 重启 xinetd，发出命令 `/etc/rc.d/init.d/xinetd restart`。这将调用在任何运行级别启动或停止 xinetd 守护程序（从而启动或关闭系统）时调用的同一 shell 脚本。xinetd 应报告其状态为：

```bash
# /etc/rc.d/init.d/xinetd restart
Stopping xinetd:	[	OK	]
Starting xinetd:	[	OK	]
```

重启后，FTP 服务器可对所有传入请求访问。

## 启动 Very Secure FTP Server (vsftpd) 软件包

Red Hat Linux 发行版的早期版本要求您编辑 /etc/xinetd.d 目录下名为 vsftp 的文件以启用并启动 Very Secure FTP 服务器 vsftpd。使用 Fedora，您现在可以简单地使用 system-config-services 客户端或 service 命令来启动 vsftpd。例如，使用 service 命令像这样启动服务器：

```bash
# service vsftpd start
Starting vsftpd for vsftpd:	[	OK	]
```

使用 system-config-services 客户端或 service 命令来启动、停止或重启 vsftpd 服务器。不要同时在系统中运行两个 FTP 服务器！

