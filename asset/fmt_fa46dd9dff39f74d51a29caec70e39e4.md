
```
*.debug \auth,authpriv,news,mail /var/debug
```

接下来的四行也是一个指令，它将所有 info、notice 和 warn 优先级消息发送到 `/var/log/messages` 文件。带有 `.none` 扩展的设施的消息不在列表中：

```
*.info;.notice;*.warn \auth,authpriv.none;cron.none /var/log/messages
```

### 热日志配置

默认日志配置文件看起来组织得不太良好，它仅仅反映了相对于日志信息的不同优先级集合。首先，以下行将 info 级别消息发送到 `/var/log/messages`：

```
*.info.mail.none;authpriv.none;cron.none /var/log/messages
```

通过 `authpriv` 设施进行登录尝试的消息发送到 `/var/log/secure` 文件：

```
authpriv.* /var/log/secure
```

所有与邮件服务器相关的消息发送到 `/var/log/maillog` 文件：

```
mail.* /var/log/maillog
```

关于 cron 任务执行的信息发送到 `/var/log/cron` 文件：

```
cron.* /var/log/cron
```

## 第 12 章 构建与维护安全基准

所有用户都会接收到紧急日志消息，这些消息通常指示系统即将关闭。星号 (`*`) 表示消息将发送到所有控制台。

`*emerg *`

## 逐个服务的日志

许多服务都有各自的独立日志系统。虽然 `/var/log/` 目录包含了标准日志服务的文件，但请注意其子目录。许多 `/var/log/` 子目录包含来自某些服务的日志文件。

在接下来的章节中，你将探索三个在各自子目录中配置了自定义日志文件的服务。这些日志文件的格式与 `/etc/syslog.conf` 和 `/etc/rsyslog.conf` 中定义的格式；它们是不同的日志服务。所选三个服务只是示例：其他具有 `/var/log/` 子目录的服务可能在它们的主配置文件中有自己的日志文件。

## CUPS 日志

CUPS 系统默认定义了三个日志：`access_log`、`error_log` 和 `page_log`。通常，通过以下指令将日志信息设置为 info 或 warning ：

```
LogLevel warning
```

可用的日志信息级别位于之前描述的标准层级之内。日志文件的名称可能会略微误导：

- `access.log`——提供有关 CUPS 通过网络访问打印机的信息。
- `error_log`——包含带错误和不带错误的配置消息信息。
- `page_log`——指定从本地或远程系统成功访问打印机的情况。

## Apache 日志

根据发行版的不同，你可能在 `/var/log/httpd/` 或 `/var/log/apache2/` 目录中找到 Apache 日志文件。日志文件的实际名称取决于与相关的安全 Web 网站相关的相应配置文件中的自定义配置。这些文件中的关键指令包括：

- `ErrorLog`——指定接收错误消息的日志文件。
- `CustomLog`——用于记录请求，通常配合 `LogFormat` 指令来指定要记录的信息。
- `TransferLog`——指定基于之前定义的 `CustomLog` 格式或标准通用日志格式的日志文件。

## 第三部分 | 构建分层 Linux 安全策略

| 选项 | 描述 |
| :--- | :--- |
| `%a` | 远程 IP 地址 |
| `%D` | 服务请求的时间，微秒 |
| `%f` | 提供的文件名 |
| `%h` | 远程系统的主机名 |
| `%l` | 远程用户的登录名 |
| `%t` | 请求的时间 |
| `%u` | 远程用户名 |
| `%U` | 请求的统一资源定位符 (URL) |
| `%v` | 提供请求的 Web 站的名称，通常为虚拟主机名 |

Apache 日志文件最有价值的部分可能是基于 `LogFormat` 指令的，它可以收集有关连接到目标 Apache 服务器上配置的 Web 服务器用户的各种信息。表 12-3 描述了一些重要的 `LogFormat` 选项。

这只是从 Web 网站上每次用户点击中记录的信息的一小部分。在你的 Web 网站上收集的所有用户点击信息量很容易变得巨大。然而，这些信息对于解析你的用户行为可能非常有用。

## Samba 日志

Samba 是用于连接基于微软网络的 Linux 服务名称。大多数与 Samba 相关的日志文件由主 Samba 配置文件 `/etc/samba/samba.conf` 中的以下指令驱动。

```
log file = /var/log/samba/log.%m
```

`%m` 被翻译为主机名，或者如果没有网络基本输入输出系统（NetBIOS），则为连接到本地 Samba 服务器的机器的网协议（IP）地址。例如，如果服务器位于 `192.168.0.0/24` 网络上，你可能会在 `/var/log/samba/` 目录下看到类似 `log.192.168.0.10` 的日志文件。普通和错误消息会被发送到该日志。该目录中的某些特定机器日志文件可能是空的，表示该系统被识别为本地网络上的浏览服务器。

## 第 12 章 构建与维护安全基准

## 整合与保护远程日志

`rsyslog` 服务构建在原始系统和内核日志服务的基础上，包括其基础配置文件 `/etc/syslog.conf`。该旧版服务的弱点是它以明文将日志信息发送到远程或中央服务器。换句话说，如果一个想要收集你系统当前状态信息的恶意用户，如果他或她能够识别出配置为中央日志服务器的系统，他们就可以大获一场了——除非该服务通过 `/etc/rsyslog.conf` 文件进行了配置。尽管 `rsyslog` 服务主要在 `/etc/rsyslog.conf` 文件中配置，但该服务默认启动并且相当重要。

## 默认 rsyslog 配置

虽然 `rsyslog` 的优势可以作为远程服务器，但日志信息的远程传输默认被禁用。通常，你应该在客户端和服务器系统上至少安装 `rsyslog` 和 `tunnel` 包。如果你需要加密，在单独包中有两个基本选择，分别基于传输层安全（TLS）和通用服务应用程序接口（GSSAPI）。在 Red Hat 和 Ubuntu 系统上，这些选项在 `rsyslog-utils` 和 `rsyslog-gssapi` 包中可用。

`rsyslog` 服务的启动由一个中心配置文件 `rsyslog` 驱动。该文件的位置随发行版而异。在 Red Hat 系统上，它位于 `/etc/default/` 目录。在 Ubuntu 系统上，取决于发布版本，相应的变量位于 `/etc/rsyslog.conf`（注：此处原文可能有误，通常指配置文件路径）。

[注：由于提供的文本在在此处中断或逻辑不完整，翻译已根据提供的文本片段完成至第12章。]

## 第 12 章 构建与维护安全基线

| 表 12-4 来自 /etc/syslog.conf 的配置规则 |
| 规则 | 描述 |
| :--- | :--- |
| `$FileOwner syslog` | 这将关联文件的用户所有者设置为 syslog 用户。 |
| `$FileGroup adm` | 这将关联文件的组所有者设置为 syslog 用户。 |
| `$FileCreateMode 0640` | 这为通过 syslog 服务创建的文件分配 640 权限。 |
| `$DirCreateMode 0755` | 这为通过 syslog 服务创建的目录分配 755 权限。 |
| `$Umask 0022` | 这设置 umask 的指定值。它可能会覆盖 `$FileCreateMode` 和 `$DirCreateMode` 变量。 |
| `$PrivDropToUser syslog` | 这分配一个与 syslog 服务关联的用户。 |
| `$PrivDropToGroup syslog` | 这分配一个与 syslog 服务关联的组。 |

### syslog 配置规则

某些配置规则为日志文件设置了基本参数。例如，来自 Ubuntu Lucid Lynx 版本的 `/etc/syslog.conf` 的以下指令在概念上应该与其他服务一样熟悉，因为它们设置了相关文件的所有权和权限。表 12-4 描述了该版本配置文件的规则。

`syslog` 开发人员建议管理员使用 `$PrivDropToUserID` 和 `$PrivDropToGroupID` 指令，而不是 `$PrivDropToUser` 和 `$PrivDropToGroup` 指令。如果 `syslog` 用户不存在，`$PrivDropToUser` 和 `$PrivDropToGroup` 指令意味着 syslog 将以 root 管理员权限运行。在这种情况下，如果恶意用户入侵了 syslog 账户，该人员将获得本地系统的完整 root 管理员权限。或者，你只需要仔细确保在密码认证数据库中正确配置了 syslog 用户和组即可。

### 包含/整合 syslog 配置规则
