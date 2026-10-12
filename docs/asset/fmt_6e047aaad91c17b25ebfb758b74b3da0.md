
`max log size` 指令设置了 Samba 允许其日志文件达到多大。相关数值以千字节为单位，使用 `0` 表示日志文件大小没有限制——这是个坏主意，除非您喜欢文件系统被日志文件占满。当文件达到列出的大小时，Samba 会将现有文件重命名为带有 `.old` 扩展名的文件，并使用原始名称开始一个新文件。然后，您可以使用 Shell 脚本——在第 20 章中讨论过——备份并压缩这些文件，以便在需要时保留它们用于分析，而不会占满文件系统。

在日志信息部分完成后，是时候转到安全部分了：

```
security = user
```

`security` 语句决定了客户端如何向服务器进行身份验证。在 Samba 2 中，有四种不同的安全模式可用，如果您使用的是 `Red Hat 6.2` 或更高版本，那就是您正在使用的版本。这些模式是：

### 表 18.3 在 `/etc/smb.conf` 中使用的替换变量。

| 变量 | 值 |
| :--- | :--- |
| `%a` | 远程机器的架构，来自 `WiWg` (Windows for Workgroups)、`Win95`、`WinNT`、`Samba` 或 `UNKNOWN`；不完全可靠 |
| `%d` | Samba 服务器的 PID |
| `%g` | 分配给传入用户的主组 |
| `%G` | 传入用户希望访问的主组 |
| `%h` | 运行 Samba 服务器的主机名称 |
| `%H` | 属于传入用户的家目录 |
| `%I` | 远程机器的 IP 地址 |
| `%L` | 服务器的 NetBIOS 名称 |
| `%m` | 远程机器的 NetBIOS 名称 |
| `%M` | 远程主机的主机名 |
| `%N` | 网络信息系统 (NIS) 服务器的名称 |
| `%p` | NIS 提供的家目录的路径 |
| `%P` | 访问目录的根目录 |
| `%S` | 访问的 Samba 共享名称 |
| `%T` | 当前日期和时间 |
| `%u` | 分配给当前 Samba 访问的用户名 |
| `%U` | 客户端请求的用户名 |
| `%v` | Samba 服务器的版本号 |

- `security=domain` -- 通过 Windows NT 域控制器对传入连接进行身份验证。必须通过 Linux `smbpasswd` 命令将 Linux 机器添加到域控制器中，并且必须将 Samba 的 `encrypt passwords` 语句设置为 `yes`。为了让 NT 用户访问 Linux 机器，他们需要在 Samba 服务器上拥有一个与其 NT 账户名称相同的账户。

- `security=server` -- 借助另一个支持 SMB 的服务器对传入连接进行身份验证。要使用的服务器由 `password server` 语句指定。

- `security=share` -- 不需要任何形式的身份验证。它主要适用于无法确保传入的 Samba 请求来自也存在于服务器机器上的账户的打印服务器。

- `security=user` -- 确保 Samba 客户端必须在登录时进行身份验证，就像其他任何用户必须做的一样。因此，当您无论操作系统如何都一致地分配登录信息时，此设置非常有用。如果您的 Windows 账户与 Linux 账户相同，请选择此安全级别。用户安全性通常也适用于与 `Windows 95`、`98` 和 `NT` 机器的连接。然而，由于共享处理中的缺陷，此设置与 `Windows for Workgroups`（`Windows 3.11`）配合不佳。这是默认设置。

安全指定之后，是一行您可能需要根据所选选项进行配置的代码：

```
; password server = <NT-Server-Name>
```

这一行被注释掉了。`password server` 语句——如前文所暗示的——使您能够将 Samba 指向一个或多个支持 SMB 的服务器。通常，这个服务器是另一个 Linux 或 Unix Samba 服务器，或者是 `Windows NT` 服务器。

继续进入更精细的密码问题，请考虑以下几行：

```
; password level = 8
; username level = 8
```

`password level` 语句在处理密码时区分大小写不正确的情况下是必要的——例如 `Windows for Workgroups` (`Windows 3.11`)。您设置的那个整数级别代表密码中有多少个字符有可能被转换为大写或小写。

`username level` 语句的功能与 `password level` 语句相同。

继续对密码处理进行更精细的调整，您会遇到以下几行：

```
; encrypt passwords = yes
; smb passwd file = /etc/smbpasswd
```

在这两行中，第一个是 `encrypt passwords` 语句，它只有两个可能的值：`yes` 或 `no`。激活时，该语句决定 Samba 服务器是否向客户端请求加密密码。`smb passwd file` 语句指向包含 Samba 服务器可能需要验证的加密密码的文件。更多相关的语句如下：

```
; unix password sync = Yes
; passwd program = /usr/bin/passwd %u
; passwd chat = *New*UNIX*password* %\n *ReType*New*UNIX*password* %\n*passwd:*all*authentication*tokens*updated*successfully*
```

如果 `unix password sync` 语句取消注释并与 `encrypt passwords` 一起使用，它确保每当 SMB 加密密码更改时，用户的登录密码也会更改。为了完成此任务，Samba 调用由 `passwd program` 指定的程序。由 `passwd chat` 语句指定的工具调节 Samba 服务器与 `passwd program` 语句中设置的工具之间的讨论。`passwd chat` 包含回答 `passwd program` 请求所需的信息。在上面的代码中，此交互从 Samba 服务器监视 `*New*UNIX*password*` 开始。星号是通配符，接受任何文本，其目的是忽略这三个关键字周围的任何格式或额外语言。当 Samba 服务器接收到这组单词时，它发送 `%n`（即新密码），然后发送换行符 `\n` 结束。

信息发送后，Samba 服务器等待 `*ReType*new*UNIX*password*`，再次使用通配符以确保它只监视关键字。当它接收到此文本时，它发送新密码并再次发送换行符。代码继续到下一行。当服务器看到 `*password*all*authentication*tokens*updated*successfully*` 时，它知道一切正常，并认为密码已更改。

以下行开始了处理用户名的代码：

```
; username map = /etc/smbusers
```

`username map` 语句指向包含如何将远程机器上的用户名转换为本机用户名数据的文件。有关如何设置这些映射文件之一的说明，请参阅“即时解决方案”部分中的“创建用户映射”。该语句的值是映射文件的路径。

您还可以使用以下内容设置 Samba 以不同方式处理各种机器：

```
; include = /etc/smb.conf.%m
```

`include` 语句使您能够为特定机器插入额外的配置文件。在此语句中，您可以使用任何替换方法，除了 `%u`、`%P` 或 `%S` 以外。

接下来是以下行：

```
socket options = TCP_NODELAY SO_RCVBUF=8192 SO_SNDBUF=8192
```

`socket options` 语句设置了 Samba 服务器与客户端通信所使用的`网络套接字`。`套接字`是网络客户端和服务器进行通信的接口点

发送和接收数据。设置好套接字后，如果 IP 地址与您的相符，您将会看到下面这一行：

```
interfaces = 192.168.12.2/24 192.168.13.2/24
```

`interfaces` 语句允许您明确告知 Samba 在`广播`信息时使用哪些接口——通常是以太网卡。回顾第 7 章，网络或子网地址块中的最后一个地址被称为`广播地址`，用于向网络中的每台机器发送信息。内核通常会告知 Samba 使用此地址进行其自身的广播。然而，您可以使用以下格式之一的 `interfaces` 语句来覆盖此功能：

- 一个接口名称，通常是 `eth0` 或 `eth1`

- 一个通配接口名称，通常是 `eth*`

- 一个 `IPaddress/netmask` 对

- 一个 `IPaddress/netbit` 对，如前一个示例代码所示

在 `interfaces` 配置好或被注释掉后，文件继续包含以下这一行：

```
remote browse sync = 192.168.3.25 192.168.5.255
```
