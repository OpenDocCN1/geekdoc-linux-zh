
## 最近一次成功的代理登录

最近一次成功的代理登录字段包含用户对代理成功登录的最后一次日期的引用。

## 该用户将使用的身份验证机制

支持以下身份验证机制：

- RSA SecurID 挑战/响应和计时令牌身份验证
- Digital Pathways 的安全网络密钥 (SNK)，一种挑战响应系统
- BellCore 的 S/Key 一次性密码系统
- 可重复使用的密码

可以通过在 `authsrv` 实用程序命令中指定 `proto` 选项的适当值，指示 `authsrv` 使用上述其中一种机制来对特定用户进行身份验证（参见表 11.1 中的 `proto` 命令语法）。

无论为每个用户定义的身份验证机制如何，都可以通过使用本节后面描述的 `authsrv` 管理实用程序，由 `authsrv` 守护进程处理用户条目的创建、修改、禁用或删除。

让我们在 `/etc/xinetd.d/authsrv` 文件中输入适当的配置，开始配置 `authsrv` 守护进程（参见清单 11.14）。

### 清单 11.14 authsrv 的 xinetd 配置

```
service authsrv
{
    flags             = REUSE
    socket_type       = stream
    wait              = no
    user              = root
    server            = /usr/local/etc/authsrv
    log_on_failure    += USERID
    disable           = no
}
```

如果你的系统使用 `inetd`，请将清单 11.15 中的行添加到 `/etc/inetd.conf` 文件中。

### 清单 11.15 authsrv 的 inetd 配置

```
authsrv stream tcp nowait root /usr/local/etc/authsrv authsrv
```

请注意，为了让服务器将 `authsrv` 关键字识别为服务，你必须在 `/etc/services` 中创建如下 `authsrv` 条目：

```
authsrv     7777/tcp
```

在重启 `xinetd` 服务后，你将拥有一个正在监听 TCP 端口 `7777` 连接的可用 `authsrv` 守护进程。在你的 `/usr/local/etc/netperm-table` 文件中定义 `authsrv` 选项。配置文件中的一般条目类型为

`authsrv: attribute-group`

除了为 `tn-gw` 概述的标准属性外，*attribute-group* 字段还可以采用以下其中一种构造：

- *directory directory* 此构造指定在执行代理命令之前用作工作目录的目录。
- *badsleep seconds* 此构造指定连续五次身份验证失败的用户应被阻止再次进行身份验证的时间（以秒为单位）。
- *database path* 此构造指定身份验证数据库文件的路径。
- *nobogus true* 此构造指定当尝试使用不存在的用户登录时，身份验证服务器是否应报告该行为。
- *[permit | deny]-operation [user users | group groups] service destination [options] [time start end]* 此构造指定在一天中的特定时间是否允许或拒绝特定用户或组的某些操作。
- *secureIDhost firewall* 此构造指定用于 RSA SecureID 身份验证的防火墙名称。

例如，考虑清单 11.16 中 `/usr/local/etc/netperm-table` 的摘录。本示例中的此配置

- 指示 `authsrv` 仅允许来自本地防火墙主机的连接，这是一个好主意。
- 显示数据库文件位于目录 `/usr/local/etc/fw-authdb` 中。
- 显示身份验证失败的用户应被禁止使用该服务 `20` 分钟。
- 指示 `authsrv` 报告使用不存在的用户登录的尝试。

### 清单 11.16 在 `netperm-table` 中定义 `authsrv` 规则

```
authsrv: permit-hosts localhost
authsrv: database /usr/local/etc/fw-authdb
authsrv: badsleep 1200
authsrv: nobogus true
```

下一步是手动输入 `authsrv` 命令（作为 `root` 用户）在数据库中创建用户。假设你想创建一个新用户名 `toro`，它将使用密码身份验证。正如你在清单 11.17 中看到的，你进入 authsrv 界面，并立即由 authsrv# 提示符欢迎你。在该提示符下，你首先添加新用户 toro，并附上其全名 (Toro T. Bravo)。默认情况下，新用户是禁用的，因此你需要显式启用新输入的用户 (enable toro)。然后，你指定 toro 用户名将使用的身份验证协议。最后，你指定要使用的初始密码。list 命令允许你查看当前位于 authsrv 数据库中的用户。

### 清单 11.17 在 *authsrv* 身份验证数据库中创建新用户

```
[ramon]$ sudo /usr/local/etc/authsrv
authsrv# list
Report for users in database
user           group       longname     status proto    last
----           -----       ------       -----  ------   ----
authsrv# adduser toro 'Toro T. Bravo'
ok - user added initially disabled
authsrv# enable toro
enabled
authsrv# proto toro password
changed
authsrv# pass toro 'scP@ssw0rd'
Password for toro changed.
authsrv# list
Report for users in database
user           group       longname     status proto    last
----           -----       ------       -----  ------   ----
toro                  Toro T. Bravo  y    passw    never
authsrv# exit
```

表 11.1 列出了 authsrv 界面中可用的所有命令。

### 表 11.1 *authsrv* 命令

| 命令 | 描述 |
| :--- | :--- |
| adduser user [full-name] | 将用户添加到身份验证数据库中，可选全名。 |
| deluser user | 从身份验证数据库中移除用户。 |
| disable user | 禁用身份验证数据库中的用户。 |
| enable user [onetime] | 启用之前已被禁用的用户。如果存在 onetime 选项，用户仅在再次进行身份验证时被禁用。 |
| display user | 显示指定用户的状态、身份验证协议和最后登录时间。 |
| group user group | 将用户分配到指定组。 |
| list group | 显示组中的所有成员。 |
| passwd user [passwd-text] | 将用户的密码设置为可选的 passwd-text。如果未提供 passwd-text，系统将提示你输入。 |
| proto user protocol | 设置用户的身份验证协议。协议字段必须具有以下其中一个值：“secureid” (RSA SecureID 令牌身份验证)、“snk” (Digital Pathways 安全网络密钥)、“skey” (BellCore S/Key 一次性密码系统) 或 “password” (传统可重复使用密码)。 |
| rename user newuser [full-name] | 将用户名 user 更改为 newuser，如果提供全名则同时更改全名。 |
| exit | 退出 authsrv 实用程序。 |

现在，你已准备好在 `/usr/local/etc/netperm-table` 中配置带有 auth 选项的代理。例如，考虑清单 11.18 中 FTP 代理 (ftp-gw) 的配置。第一行指示 FTP 代理通过联系本地主机上的 TCP 端口 7777 来对用户进行身份验证。第二行允许受信任网络 10.0.0.0/24 使用 FTP 代理，但要求选择上传文件 (FTP STOR 操作) 的用户进行身份验证。最后一行要求所有其他 (不受信任) 用户向代理进行身份验证。

### 清单 11.18 在 ftp-gw 规则中使用 authsrv 身份验证

```
ftp-gw: authserver localhost 7777
ftp-gw: permit-hosts 10.0.0.* -auth {STOR}
ftp-gw: permit-hosts * -authall
```

## 总结

本章重点关注 FWTk 防火墙工具包，这是一组可用于构建你自己应用层防火墙的进程和配置文件。通过在上一章讨论的 SOCKS 代理之上运行一层，FWTk 工具包可以添加一些高级访问控制机制，使安全管理员能够对需要支持的每个应用程序应用不同的访问规则。

FWTK 为最流行的 Linux 网络应用程序（如 Telnet、FTP、HTTP 和 SMTP）提供了现成的代理，以及可用于通过防火墙转发任意应用程序的通用代理。snap/smapi 代理提供了一种真正的存储转发邮件传输机制，其中邮件可以在防火墙处暂存，并异步转发到目标系统。

本章结束了关于周边安全和防火墙设备的讨论。本书的下一个也是最后一部分将关注在当今全球化和流动办公环境中日益重要的主题：远程访问和身份验证。

