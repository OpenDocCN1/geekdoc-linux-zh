
**注意**
此处讨论的 FTP 用户适用于匿名 FTP 配置和服务器设置。
此外，请注意，其他 Linux 发行版可能会使用不同的默认目录，例如用于 FTP 文件和匿名用户 的 `/usr/local/ftp`。

此条目遵循标准的 `/etc/passwd` 条目格式：用户名、密码、用户 ID、组 ID、注释字段、主目录和 shell。要了解有关 `/etc/passwd` 的更多信息，请参阅第 14 章，“管理用户”中的“密码文件”部分。

此条目中的每一项都由冒号分隔。在上面的示例中，你可以看到托管服务器的 Fedora 系统使用阴影密码，因为传统密码字段中存在 `x`。阴影密码系统非常重要，因为它为 Fedora 增加了额外的安全级别；阴影密码系统通常在 Fedora 安装期间安装。

FTP 服务器软件使用此用户账户来为连接到服务器的用户分配权限。通过对匿名 FTP 用户使用默认的 shell 为 `/sbin/nologin`（而不是 `/bin/bash` 或其他标准交互式 shell），这些用户将无法作为普通用户登录。`/sbin/nologin` 不是一个 shell，而是一个通常分配给已锁定账户的程序。作为 root 用户检查 `/etc/shadow` 文件（参见清单 24.2）表明，无法登录此账户，因为使用 `*` 作为密码表示这一点。

### 清单 24.2 阴影密码文件中的 FTP 用户条目

```
# cat /etc/shadow

bin:*::11899:0:99999:7:::

daemon:*::11899:0:99999:7:::

adm:*::11899:0:99999:7:::

lp:*::11899:0:99999:7:::

...

ftp:*:12276:0:99999::17:::
```

阴影文件（仅在清单 24.2 中显示了一部分）包含标准 `/etc/passwd` 文件中未找到的额外信息，例如账户过期、密码过期、账户是否被锁定以及加密的密码。密码字段中的 `*` 表示该账户不是标准登录账户；因此，它没有密码。

尽管系统正在使用阴影密码，但在使用 FTP 时，密码不是以安全方式传输的。因为 FTP 是在加密和安全性必要之前编写的，它没有提供发送加密密码所需的机制。账户信息在 FTP 服务器上以纯文本发送；任何拥有足够技术知识和网络嗅探器的人都可以找到你连接到服务器的账户的密码。许多站点专门使用仅限匿名的 FTP 服务器，以防止普通账户密码通过互联网传输。

图 24.4 显示了 `ethereal` 捕获的 FTP 会话的一部分，可以看到它捕获到用户密码以明文发送。`ethereal` 客户端是一个用于实时显示网络流量的图形浏览器，可用于监视诸如 LAN 上 FTP 登录之类的数据包数据。

![](img/2045828cf45e5632bf056f9ca99d6755_675_0.png)

**图 24.4** `ethereal` 客户端可以过滤和嗅探 FTP 会话以捕获用户名和密码。

### 快速且粗略的 FTP 服务

尽职的 Linux 管理员会花时间仔细安装、设置和配置生产 FTP 服务器，然后才提供公共服务或在互联网上开展业务。然而，通过在安全的 LAN 上遵循几个简单步骤，你可以非常快速地设置服务器：

- 确保安装了 FTP 服务器 RPM 软件包，启用了网络，并且服务器上的防火墙规则允许 FTP 访问。请参阅第 18 章，“网络连接”，了解如何使用 Red Hat 的 `system-config-securitylevel` 客户端进行防火墙设置。
- 如果需要对服务器文件的匿名访问，请填充 `/var/ftp/pub` 目录。通过挂载或复制内容（例如该目录下的目录和文件）来完成此操作。
- 编辑然后保存适当的配置文件（例如 `vsftpd` 的 `vsftpd.conf`）以启用访问。
- 如果你使用的是 `wu-ftpd`，必须像这样启动或重启 `xinetd`：`/etc/rc.d/init.d/xinetd restart`。如果你使用的是 `vsftpd`，必须像这样启动或重启服务器：`service vsftpd start`。

### wu-ftpd 的 xinetd 配置

`xinetd`（发音为“zy-net-d”）是扩展互联网服务守护进程，处理网络服务的传入连接。`xinetd` 是类似工具 `inetd` 的优选替代品（用于其他 Linux 发行版和较旧的 Red Hat 版本）。然而，除了对 `inetd` 的其他几项改进外，`xinetd` 还允许你对不同的网络连接请求（如 FTP）应用单独的访问策略。

此守护程序根据 `/etc/xinetd.d` 目录下配置文件中的设置控制你系统上的许多服务。本节向你展示如何编辑适当的文件以启用使用 `wu-ftpd` FTP 服务器。

### 为 wu-ftpd 服务器配置 xinetd

使用 RPM 安装 `wu-ftpd` 时，RPM 软件包可能包含一个 `xinetd` 配置文件 `/etc/xinetd.d/wu-ftpd`，如清单 24.3 所示。你需要编辑该文件，因为其默认设置禁用了传入的 FTP 请求。

**注意**
不要被 `wu-ftpd` 文件文本的第一行混淆。尽管该行写着 `default: on`，但除非你专门配置其使用，否则 FTP 服务是关闭的。该行是注释，因为它以井号 (`#`) 开头，被 `xinetd` 忽略。FTP 服务是否开启由文本行 `disable = yes` 决定。

## 列表 24.3 wu-ftpd 的 xinetd 配置文件

```text
# default: on

# description: The wu-ftpd FTP server serves FTP connections. It uses \
#          normal, unencrypted usernames and passwords for authentication.

service ftp
{
disable          = yes
          socket_type      = stream
          wait             = no
          user             = root
          server           = /usr/sbin/in.ftpd
          server_args      = -l -a
          log_on_success   += DURATION
          nice             = 10
}
```

使用编辑器将 `disable = yes` 行更改为 `disable = no`。保存文件并退出编辑器。然后你必须重启 `xinetd`，因为配置文件仅在启动时解析。以 root 身份重启 `xinetd`，请执行命令 `/etc/rc.d/init.d/xinetd restart`。这将调用与在任何运行级别启动或停止 `xinetd` 守护进程（从而启动或关闭系统）时调用的同一个 shell 脚本。`xinetd` 应将其状态报告为

```text
# /etc/rc.d/init.d/xinetd restart
Stopping xinetd:                            [  OK  ]
Starting xinetd:                             [  OK  ]
```

重启后，FTP 服务器即可访问所有传入请求。

## 启动 Very Secure FTP 服务器 (vsftpd) 包

Red Hat 的早期 Linux 发行版要求你编辑 `/etc/xinetd.d` 目录下的名为 `vsftpd` 的文件，以启用并启动 Very Secure FTP 服务器 `vsftpd`。在 Fedora 中，你现在可以简单地使用 `system-config-services` 客户端或 `service` 命令来启动 `vsftpd`。例如，使用 `service` 命令启动服务器，如下所示：

```text
# service vsftpd start
Starting vsftpd for vsftpd:                [  OK  ]
```

使用 `system-config-services` 客户端或 `service` 命令来启动、停止或重启 `vsftpd` 服务器。切勿同时在系统上运行两个 FTP 服务器！

你还可以使用 `/etc/rc.d/init.d` 目录下的名为 `vsftpd` 的 shell 脚本来启动、停止、重启和查询 `vsftpd` 服务器。你必须拥有 root 权限才能使用 `vsftpd` 脚本控制服务器，但任何用户都可以使用 `status` 关键字查询服务器（查看它是否正在运行以及其进程 ID 号），如下所示：

```text
$ /etc/rc.d/init.d/vsftpd status
```
