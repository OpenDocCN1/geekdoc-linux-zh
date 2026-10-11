

- ftp-gw：用于处理文件传输协议（FTP）连接的 FTP 代理
- http-gw：用于处理到 Web 服务器的 HTTP 连接的 HTTP 代理
- plug-gw：一种通用代理，可配置为处理任何类型的传输层连接
- smap：用于处理互联网邮件服务器连接的 SMTP 代理

让我们更详细地看看每个应用层代理可用的规则。

## tn-gw：Telnet 代理

前一节描述了 NetACL 规则，并使用 telnet 作为示例来说明其工作原理。FWTK telnet 代理默认位于 /usr/local/etc/tn-gw。

您需要配置 xinetd 或 inetsd 服务，使其使用 tn-gw 代理而不是原生的 telnet 服务。如果您的服务器使用 xinetd，请创建一个名为 /etc/xinetd.d/telnet 的文件，其内容如清单 11.6 所示。

### 清单 11.6 telnet 的 xinetd 配置

```
service telnet
{
    flags         = REUSE
    socket_type   = stream
    wait          = no
    user          = root
    server        = /usr/local/etc/tn-gw
    log_on_failure  ++ USERID
    disable       = no
}
```

如果您使用 inetsd，请将清单 11.7 中显示的这行添加到 /etc/inetsd.conf 文件中。

### 清单 11.7 telnet 的 inetsd 配置

```
telnet stream tcp nowait root /usr/local/etc/tn-gw tn-gw
```

Telnet 代理的基本操作如下：

1. 用户会被告知（可能是在您的安全策略中），应通过 telnet 连接到代理防火墙的私有接口（或唯一接口），而不是目标系统。
2. 用户将获得以下提示（受访问控制和身份验证的限制）：
   ```
   [ramon]$ telnet fwtK-internal.example.com
   Trying 10.0.0.2...
   Connected to fwtK-internal.
   Escape character is '^]'.
   Welcome to the TIS Firewall Toolkit TELNET Proxy!
   tn-gw->
   ```
3. 用户在提示符处输入外部 telnet 命令：
   ```
   tn-gw-> connect anyhost.anydomain.com
   Trying 203.204.205.206 port 23...
   Connected to anyhost.anydomain.com.
   Escape character is '^]'.
   Red Hat Linux release 7.0 (Guinness)
   Kernel 2.2.16-22 on an i686
   login:
   ```
4. 用户继续通过代理连接，直到输入远程逃逸命令。此时，到远程系统和代理服务器的连接都将断开。

除了配置 NetACL 之外，还可以使用 `/usr/local/etc/netperm-table` 文件来控制 FWTK telnet 代理的行为。对于 telnet 代理，有几个 `/usr/local/etc/netperm-table` 配置参数需要您了解。该代理在配置文件中的通用格式为 `tn-gw: attribute-group`，其中 `attribute-group` 可以采用以下格式之一：

- `authserver host port`：此格式指定运行身份验证服务器的主机和端口。身份验证服务器的配置在本章稍后的“在 FWTk 中使用强身份验证”部分中有介绍。
- `denial-msg file`：此格式指定包含一条文本消息的文件，当用户没有使用代理所需权限时显示该消息。
- `help-msg file`：此格式指定包含一条文本消息的文件，当用户向代理请求帮助时显示该消息。
- `welcome-msg file`：此格式指定包含一条文本消息的文件，当用户成功登录到代理时显示该消息。
- `denydest-msg file`：此格式指定包含一条文本消息的文件，当用户被禁止连接到请求的目标时显示该消息。
- `directory directory`：此格式指定在执行代理命令前更改默认根目录（chroot）的目录。
- `userid user`：此格式指定代理应运行所使用的用户 ID。
- `groupid group`：此格式指定代理应运行所使用的组 ID。
- `prompt prompt`：此格式指定代理使用的提示符。
- `timeout seconds`：此格式指定代理终止连接的闲置时间（以秒为单位）。
- `permit-hosts host-description [-dest-host-description] [-auth][-passok]`：此格式指定允许使用代理的主机（host-description），以及允许其代理到的目的地（-dest-host-description）、是否需要提供 authsrv 身份验证（-auth）以获得使用代理的权限，以及是否允许其修改密码（-passok）。authsrv 身份验证将在本章稍后详细讨论。
- `deny-hosts host-description`：此格式指定不允许使用代理的主机。

例如，考虑清单 11.8 中显示的 tn-gw 配置部分。此示例执行了几个重要步骤：

- 指定包含拒绝、欢迎和帮助消息文本的文件。
- 请求在闲置 10 分钟后终止连接。
- 允许来自 10.0.0.0/24 网络中客户端的代理连接，但仅限于目的地为 63.64.65.0/24 网络的连接。
- 不允许来自其他任何主机的代理请求。

### 清单 11.8 在 netperm-table 中定义 tn-gw 规则

```
tn-gw: deny-msg        /usr/local/etc/tn-deny.txt
tn-gw: welcome-msg     /usr/local/etc/tn-welcome.txt
tn-gw: help-msg        /usr/local/etc/tn-help.txt
tn-gw: timeout         600
tn-gw: permit-hosts    10.0.0.* -dest 63.64.65.*
tn-gw: deny-hosts      *
```

请注意，清单 11.8 包含 deny-hosts 属性组的专用版本：

```
tn-gw: deny-hosts unknown
```

![](img/3258bbaf790525f8c4eb25fabff7844a_344_0.png)

该属性强制代理对客户机的 IP 地址执行反向 DNS 查找，以寻找有效的主机名（在 DNS 术语中称为 PTR 记录）。如果不存在这样的绑定，连接将被拒绝。

## ftp-gw：FTP 代理

ftp-gw FTP 代理的工作方式与 tn-gw 非常相似。让我们先从指导您的 xinetd 或 inetd 服务使用 ftp-gw 而不是原生 FTP 服务开始。如果您的服务器正在使用 xinetd，请通过创建一个名为 /etc/xinetd.d/ftp 的文件来实现，其内容如清单 11.9 所示。

### 清单 11.9 FTP 的 xinetd 配置

```
service ftp
    {
        flags           = REUSE
        socket_type     = stream
        wait            = no
        user            = root
        server          = /usr/local/etc/ftp-gw
        log_on_failure  += USERID
        disable         = no
    }
```

如果您使用 inetd，请将清单 11.10 中显示的这行添加到 /etc/inetd.conf 文件中。

### 清单 11.10 FTP 的 inetd 配置

```
ftp stream tcp nowait root /usr/local/etc/ftp-gw ftp-gw
```

以下是 FTP 代理的工作原理：

1. 用户会被告知（可能是在您的安全策略中），应将其 FTP 客户端指向代理防火墙的私有接口（或唯一接口），而不是目标系统。为了建立到公共 FTP 服务器（例如 ftp.sybex.com）的连接，用户首先输入以下内容（假设 fwtvk-internal.example.com 是对应于您的代理防火墙私有接口的主机名）：
   ```
   [ramon]$ ftp fwtvk-internal.example.com
   Connected to fwtvk-internal.
   220 fwtvk-internal.example.com FTP proxy (Version V2.1) ready.
   ```
2. 用户向 FTP 代理提供用户名和要 FTP 到的远程主机名。请注意以下响应中的 `user@remote-hostname` 格式：
   ```
   Name (fwtk-internal:ramon): `anonymous@ftp.sybex.com`
   331-(---GATEWAY CONNECTED TO ftp.sybex.com---)
   331-(220- kermit WAR-FTPD 1.67-04 Ready)
   331-(220 Please enter your user name.)
   331 User name okay. Give your full Email address as password.
   Password:
   230 User logged in, proceed.
   ftp>
   ```
3. 用户继续通过代理连接，直到输入远程逃逸命令（例如，FTP 中的 `bye`）。此时，到远程系统和代理服务器的连接都将断开。

FTP 代理的 `/usr/local/etc/netperm-table` 配置参数与其 Telnet 对应物非常相似：

```
ftp-gw: attribute-group
```

在此格式中，`attribute-group` 可以是用于 `tn-gw` 的任意构造（参见前一节），除了以下例外：

```
permit-hosts host-description [-dest host-description] [-auth (operation1 operation2..)] [-authall] [-log [operation1 operation2..]]
```

此格式指定允许使用代理的主机（`host-description`），以及允许其代理到的目的地（`-dest host-description`），以及它们是否应为特定类型的 FTP 操作提供 authsrv 身份验证（`-auth`），例如检索文件（RETR）或上传文件（STOR）。`-authall` 属性强制代理用户为所有 FTP 操作进行身份验证。

此外，您可以指示 `ftp-gw` 将通过 `syslog` 记录尝试执行 FTP 协议支持的任何类型操作（例如，`RETR`、`STOR` 等）的所有尝试。

例如，考虑清单 11.11 中的 `/usr/local/etc/netperm-table` 配置。此示例为代理 FTP 连接指定 10 分钟的闲置超时，并允许 10.0.0.0/24 块发起 FTP 连接。您将通过本地 `syslog` 设施记录在远程 FTP 服务器上检索和存储文件的所有尝试。

