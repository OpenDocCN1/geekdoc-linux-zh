
Jane 在她的 ISP 有一个拨号账号。她的 ISP 还提供 Web 过滤服务（通过使用 http 代理）。Jane 有两个条目。一个是普通的拨号，另一个启用了过滤器，通过在 NAS 设备上调用名为 `kidsafe` 的过滤器来禁止访问 Web。这防止了 Jane 的孩子们在不通过其 ISP 提供的过滤服务的情况下访问 Web。以下是 Jane 的两个条目：

```
Jane Auth-Type=system
  Service-Type=Framed-User,
.Jane Password="mykids", Suffix=".filtered"
  Service-Type=Framed-User,
  Filter-Id="kidsafe"
```

XYZ 公司拥有一个拨号连接。他们有一个包含 16 个 IP 地址的范围，从 192.168.2.16 到 192.168.2.31。他们还有一个静态 IP 地址 192.168.42.18。ISP 配置了 RADIUS，使得拨入接入的 NAS 用户被告知如何将客户的局域网信息插入到其路由表中。当客户登录时，NAS 知道如何到达客户的地址，然后它可以通过 ISP 网络内部的另一种路由协议进行共享。以下是所使用的 RADIUS 条目：

```
xyzlan Password="xyzpass"

User-Service-Type=Framed-User,

Framed-Protocol=PPP,

Framed-Address=192.168.42.18,

Framed-Netmask=255.255.255.255,

Framed-Route="192.168.2.16/28 192.168.42.18"
```

另一个实用的 RADIUS 功能是用户文件中的 `DEFAULT` 功能。如果 OpenLinux 密码文件中的每个人都使用基于网络访问的 PPP，那么用户文件就可以被非常地简化。只需以下内容：

```
DEFAULT Auth-Type=system

Service-Type=Framed-User,

Framed-Protocol=PPP
```

这是一个非常好的功能，但请记住，像 root 以及服务器上的其他系统账户（以及你可能为 `(httpd)` 添加的具有有效密码的账户）也可以通过 PPP 网络访问进行验证。

RADIUS 有许多功能，使得可以创建这些高度可配置、灵活的用户条目。NAS 厂商也有许多他们自己的功能，通常可以通过将厂商特定属性添加到字典文件中将其加入 RADIUS 中。

## 删除 RADIUS 用户

要删除 RADIUS 用户，可以从 `/etc/raddb` 中的用户文件中删除该用户名和属性，或者在该用户的每行开头放置 `#` 字符。请记住，如果你使用的是带有系统密码的 `DEFAULT` 用户，则必须从你的 OpenLinux 系统中删除用户账户。

## 修改用户密码

通过更改用户文件中用户账户的 `Password` 属性来更改 RADIUS 密码。由于该文件只有 root 用户可以访问，因此只有 root 用户可以更改 RADIUS 密码。

当然，`Auth-type` 设置为 `system` 的用户可以通过普通的 OpenLinux 方式更改他们的密码。这包括任何被 `DEFAULT` 用户条目覆盖的用户。

## 连接到 RADIUS 客户端

在尝试连接到 RADIUS 客户端机器（例如 Lucent Portmaster）之前，需要将客户端的主机和共享密钥（shared secret）添加到服务器上的 `/etc/raddb/clients` 文件中。列表 10-4 显示了该文件的示例。

列表 10-4 `/etc/raddb/clients` 文件，包含 RADIUS 客户端的主机列表及其共享密钥

| RADIUS 客户端 | 共享密钥 |
| --- | --- |
| portmaster | trustme |
| localhost | testing123 |

每个 RADIUS 客户端都需要在此文件中列出，否则 radius 将不会允许其验证用户。为了使此功能正常，此文件中的共享密钥必须在客户端侧单独配置。共享密钥最多包含 14 个 ascii 字符。共享密钥中不允许出现空白字符。clients 文件中的客户端数量没有数量限制。

## RADIUS 计费

RADI 计费守护进程是 RADIUS 认证守护进程的子进程。它在你启动 RADIUS 时启动并监听端口 1646。当用户连接和断开提供的服务时，RADIUS 客户端会发送计费信息。日志位于 `/var/adm/radct/detail`。日志中的每条记录都有时间戳和关于连接的属性以及操作（START 或 STOP）。

## 计费属性定义

- `Acct-Status-Type`. 账户状态类型。为 START 或 STOP。
- `Acct-Delay-Time`. 事件发生到 NAS 发送记录之间的延迟时间。
- `Acct-Session-Id`. 由 NAS 设备分配的会话唯一标识符。
- `Acct-Authentic`. 表示用户是通过 RADIUS 还是本地 NAS 用户验证的。
- `Acct-Session-Time`. 会话连接时间，以秒为单位。
- `NAS-IP-Address`. 用户连接的 NAS 的 IP 地址。
- `NAS-Port-Type`. 用户连接的 NAS 端口类型（Async、Sync、ISDN）。
- `Framed-User-Address`. 为 Framed-User 连接分配给用户的 IP 地址。
- `Framed-IP-Netmask`. 为 Framed-User 连接分配给用户的 IP 网络掩码。
- `Acct-Input-Octets`. 从用户处接收的字节数（octets）。
- `Acct-Output-Octets`. 发送到用户的字节数（bytes）。
- `Calling-Station-Id`. 拨出的电话号码。
- `Calling-Station-Id`. 呼叫站的电话号码。
- `Timestamp`. 记录自纪元（1970/1/1 00:00:00）起到达服务器的秒数。
- `Request-Authenticator`. 当计费记录的数字签名出现问题时出现。
- `-d`. 指定 RADIUS 配置文件的备用目录。默认目录为 `/etc/raddb`。
- `-l`. 指定要使用的 RADIUS 日志文件，而不是使用 syslogset。
- `-s`. 以单线程模式运行 RADIUS，而不会派生子进程来处理每个身份验证请求。
- `-v`. 显示 RADIUS 的版本而不启动 `radiusd` 守护进程。
- `-x`. 调试模式。要将调试输出发送到 syslog，请使用 `-x -1 syslog`。

若要在每次 OpenLinux 机器重启时启动 RADIUS 服务器，请将行 `/usr/local/sbin/radiusd` 添加到 `/etc/rc.d/rc.local` 文件中。要停止 `radiusd` 服务器，请使用此命令：

```
killall radiusd
```

## 排除 radiusd

当 RADIUS 无法工作时，通常是一个相当模糊的症状，即用户无法远程连接到您的服务器。检查 radius 是否是罪魁祸首非常有帮助。排查 `radiusd` 问题的一种方法是使用 `-x` 标志运行程序。这会导致 `radiusd` 将日志消息写入标准输出。这允许系统管理员查看来自 RADIUS 客户端的所有请求以及这些请求是否成功。如果 RADIUS 失败：

- 确保每个 RADIUS 客户端都列在服务器的 `/etc/raddb/clients` 文件中。
- 验证 `/etc/raddb/clients` 文件中的共享密钥与每个 RADIUS 客户端上配置的密钥匹配。
- 检查确保 RADIUS 客户端正在使用正确的 RADIUS 服务器。这应该在您的客户端（即 Portmaster）说明书中得到解释。
- 检查 RADIUS 客户端的文档，确保用户文件定义了所需的所有属性。

您可以通过检查服务器日志来执行额外的故障排除。`radiusd` 会向文件 `/var/log/secure` 发一些信息，并向目录 `/var/log/radacct` 记录客户端信息。在其中，有一个用于 RADIUS 客户端计费信息的目录。检查日志不仅可以查看 `radiusd` 正在使用什么，还可以识别谁在何时登录了 RADIUS 客户端。

`radiusd` 2.1 的一个新功能是允许在不停止停止和重启守护进程的情况下开启和关闭调试。向 `radiusd` 发送 USR 信号将开启调试，发送 US2 信号将关闭调试。调试信息通过 syslog 记录。

此外，`radiusd` 2.1 提供的 `radtest` 程序有助于调试，它为您提供了一个简单的测试工具来确定您的 RADIUS 服务器在做什么。`radtest` 使用 `localhost` (127.0.0.1) 作为源地客户端 IP，因此您需要在您的 RADIUS 客户端文件中为 `localhost` 定义一个密钥密钥。如果不这样做，您将无法使用 `radtest` 测试您的配置。

## 安全考量
