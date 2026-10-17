
作为共享，您可以将打印机的使用限制为某些用户，拒绝其公共访问。以下示例设置了仅允许 `alice` 和 `bob` 用户访问打印机（如果您需要，可以添加其他用户）。用户需要对打印机池目录具有写权限。

```
path = /var/spool/samba
writeable = Yes
valid users = alice bob
public = no
printable = Yes
printer = printer
oplocks = No
share modes = No
```

虽然首选 SWAT，但您也可以 `Linuxconf` 和 `Webmin` 来配置 Samba。

## 变量替换

对于分配给参数的字符串值，您可以结合替换。这为指定可能取决于上下文的值（例如用户名）提供了更大的灵活性。例如，假设某个服务需要为每个登录的用户使用单独的目录，此类目录的路径可以使用 `%u` 变量指定，该变量会替换为当前用户名。字符串 `path = /tmp/%u` 对于 `alice` 用户将变为 `path = /tmp/alice`，对于 `bob` 用户将变为 `path = /tmp/d`。表 35-3 列出了几个较常用的替换变量。

| 变量 | 描述 |
| :--- | :--- |
| `%S` | 当前服务的名称 |
| `%P` | 当前服务的根目录 |
| `%u` | 服务的用户名 |
| `%g` | 用户的主组名 |
| `%U` | 会话用户名（请求的） |
| `%G` | 会话用户的主组名 |
| `%H` | 用户的主目录 |
| `%v` | Samba 版本 |
| `%h` | 运行 Samba 的互联网主机名 |
| `%m` | 客户端机器的 NetBIOS 名称 |
| `%L` | 服务器的 NetBIOS 名称 |
| `%M` | 客户端机器的互联网名称 |
| `%N` | 您的主目录服务器的名称 |
| `%p` | 服务主目录的路径 |
| `%d` | 当前服务器的进程 ID |
| `%a` | 远程机器的架构 |
| `%I` | 客户端机器的 IP 地址 |
| `%T` | 当前日期时间 |

## 测试 Samba 配置

在对 `smb.conf` 文件进行更改后，可以使用 `testpar` 查看条目是否正确输入。`testpar` 检查 Samba 条目的语法和有效性。默认情况下，`testpar` 检查 `/etc/samba/smb.conf` 文件。如果您在使用其他文件，可以将其作为参数传递给 `testpar`。可以使用 `smbd` 检查 Samba 服务的连接。在 SWAT 中，`Status` 页面可以列出共享。

## 第 35 章: Samba

| 选项 | 说明 |
| --- | --- |
| `password` | 访问服务器上指定服务所需的密码。如果没有提供密码，将提示用户输入密码。 |
| `- smb.conf` | 指定 `smb.conf` 文件的路径。 |
| `- B IP_address` | 指定广播 IP 地址。 |
| `- O socket_options` | 列出套接选项。 |
| `- R name resolve` | 仅使用这些名称解析服务。 |
| `- M host` | 向主机发送弹出消息。 |
| `- i scope` | 使用此 NetBIOS 范围。 |
| `- N` | 不询问密码。 |
| `-n netbios name` | 使用此名称作为我的 NetBIOS 名称。 |
| `-d debuglevel` | 设置调试级别。 |
| `- P` | 以打印机身份连接到服务。 |
| `-p port` | 连接到指定端口。 |
| `-l log basename` | 日志/调试文件的基础。 |
| `-h` | 打印此帮助信息。 |
| `-I IP_address` | 指定要连接的 IP 地址。 |
| `- E` | 将消息写入 `stderr` 而非 `stdout`。 |
| `-U username` | 指定在远程系统上登录的用户。 |
| `-L host` | 列出指定主机上可用的共享。 |
| `-t terminal` | 终端 i/o 代码 [`sjis` \| `euc` \| `jsis8` \| `jun` \| `hex`]。 |
| `-m max protocol` | 设置最大协议级别。 |
| `-W workgroup` | 设置工作组名称。 |
| `-T<cx>` | 命令行 tar 操作。 |
| `-D directory` | 从此目录开始。 |
| `-c command_string` | 执行用分号分隔的命令。 |
| `-b xmit/send buffer` | 更改传输/发送缓冲区（默认: 65520）。 |

**表 35-4.** `smclient` 选项

你也可以提供访问服务的密码。将其作为跟在服务名后的参数输入。如果你不提供密码，系统会提示你输入。

你可以添加多个选项，例如用户名 `username` 或可用服务的列表。通过 `-I` 选项，你可以使用其 IP 地址指定系统。你使用 `-U` 选项和登录名称作为你想在远程系统上使用的远程登录名。如果需要密码，请在密码前加上 `%`。通过 `-L` 选项，你可以获取服务器提供的服务列表，例如共享目录或打印机。以下命令将列出主机 `turtlemytrek.com` 上可用的共享：

```
smclient -L turtlemytrek.com
```

要访问远程系统上的特定目录，请将目录作为 `smclient` 命令的参数输入，随后跟上任何选项。对于 Windows 文件，路径名使用反斜杠 `\`，对于 Unix/Linux 文件，使用正斜杠 `/`。一旦连接，将显示 sm 提示符，你可以使用 `get` 和 `put` 等 `smclient` 命令来传输文件。`quit` 或 `exit` 命令将退出 `smclient` 程序。在接接的示例中，`smclient` 使用登录名 `dylan` 访问 `turtlemytrek.com` 系统上的 `reports` 目录：

```
smclient //turtlemytrek.com/myreports -I 192.168.0.1 -U dylan
```

在大多数情况下，你可以使用服务器名称来指代服务器，如下所示：

```
smclient //turtlemytrek.com/myreports -U dylan
```

如果你正在访问 Samba 服务器上特定账户的家目录，可以只需指定 `homes` 服务。在下一个示例中，用户在被提示输入该账户密码后，访问了 Samba 服务器上 `aleina` 账户的家目录：

```
smclient //turtlemytrek.com/homes -U aleina
```

你还可以使用 `smclient` 访问位于 Windows 客户端上的共享资源。指定 Windows 客户端的计算机及其共享文件夹。在下一个示例中，用户访问了名为 `lizard` 的 Windows 客户端上的 `windata` 文件夹。该文件夹配置允许任何人访问，因此用户在密码提示时按了回车键。

```
$ smclient //lizard/windata
added interface ip=192.168.0.2 nmask=255.255.255.255
Got a positive name query response from 192.168.0.3 ( 192.168.0.3 )
Password:
```

```
Domain=[WORKGROUP] OS=[Windows 5.1] Server=[Windows 2000 LAN Manager]
smb: \> ls
D 0 Sat Sep 8 17:29:19 2001
D 0 Sat Sep 8 17:29:19 2001
hi A 10 Sat Sep 8 17:29:27 2001\mynnewdoc.doc A 0 Sat Sep 8 16:59:13 2001
  39997 blocks of size 1048576. 39930 blocks available
smb: \> mget
Get file hi? y
getting file hi of size 10 as hi (1.22069 kb/s) (average 1.2207 kb/s)
smb: \> quit
```

登录后，你可以执行 `smclient` 命令来管理文件和目录。`smclient` 命令列在表 35-5 中。Shell 命令如下：

| 命令 |  |
| --- | --- |
| `? [command]` | 如果没有命令参数，将显示所有可用命令。使用命令参数显示特定命令的信息。 |
| `1 [shell command]` | 如果没有 shell 参数，将运行本地 shell。如果提供了 shell 命令，将执行该命令。 |
| `cd [directory name]` | 更改服务器目录。如果没有指定目录，将显示当前工作目录。 |
| `del mask` | 请求服务器删除当前目录下匹配掩码的文件。 |
| `dir mask` | 获取并显示服务器上匹配当前目录的文件列表。 |
