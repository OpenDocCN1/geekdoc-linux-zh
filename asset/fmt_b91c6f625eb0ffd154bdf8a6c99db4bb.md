
你通过 `rcp` 发送给用户的第一行输入之前，会跟一条名为 `"Message from yourHost!yourTty"` 的消息，这样接收者就可以启动 `write` 命令与你交谈。要退出 `rcp`，请在其中一行输入 `Control-D`。你可以使用 `mesg` 禁用向你的终端的写入。

图 9.17

`rcp` 命令的描述。

## 在非 UNIX 主机之间复制文件：`ftp`

文件传输协议是一种传输文件的通用协议。图 9.19 提供了 `ftp` 命令的简要描述。在接下来的示例中，我从远程“vanguard”复制“writer.txt”到本地主机：

```
$ ftp vanguard
Connected to vanguard.utallas.edu.
vanguard ftp server (SunOS 5.4) ready.
Name (glass)
Password required for glass.
Password: ...secret!
User glass logged in.
$ ls ...obtain directory of remote host.
PORT command successful.
ASCII data connection for /bin/ls (129.110.42.1,4919) (0 bytes).
ASCII ...lots of files were listed here.
uniq
who.c
writer.c
ASCII Transfer complete.
1469 bytes received in 0.53 seconds (2.7 Kbytes/s)
ftp> get writer.c ...copy from remote host.
PORT command successful.
ASCII data connection for writer.c (129.110.42.1,4920). (1276 bytes).
ASCII Transfer complete.
local: writer.c remote: writer.c
1300 bytes received in 0.012 seconds (1e+02 Kbytes/s)
ftp> ls ...obtain directory of local host.
reader.c who.c writer.c
ftp> put who.c ...copy file to remote host.
PORT command successful.
ASCII data connection for who.c (129.110.42.1,4922).
ASCII Transfer complete.
ftp> quit ...disconnect.
Goodbye.
$_
```

| 实用程序：`ftp -n [ host ]` | `ftp` 允许你操作本地主机和远程主机的文件和目录。如果你提供了主机名，`ftp` 会搜索 `.netrc` 文件以查看远程主机是否有匿名 `ftp` 账户（即无需密码）。如果有，它将使用该账户登录远程主机。如果没有匿名账户，它假设你在远程主机上有一个账户并提示你输入 ID 密码。`-n` 选项防止 `ftp` 尝试初始自动登录序列。`ftp` 的命令模式支持许多文件操作命令。这些命令中最常见的已在文中描述。你可以通过按 `Control-C` 终止传输而不退出 `ftp`。 |

9.18

`ftp` 命令的描述。

# 第 9 章 网络

| 命令 | 含义 |
| --- | --- |
| `!command` | 在本地主机上执行命令。 |
| `append localFile remoteFile` | 将本地文件 `localFile` 附加到远程文件 `remoteFile` 中。 |
| `bell` | 在每次文件传输后发出蜂声。 |
| `bye` | 关闭当前远程主机连接并退出 `ftp`。 |
| `cd remoteDirectory` | 将你当前的远程工作目录更改为 `remoteDirectory`。 |
| `close` | 关闭当前的远程主机连接。 |
| `delete remoteFile` | 从远程主机上删除 `remoteFile`。 |
| `get remoteFile [ localFile ]` | 将远程文件 `remoteFile` 复制到本地文件 `localFile`。如果省略 `localFile`，则将使用与远程文件相同的名称。 |
| `help [ command ]` | 显示关于指定命令的帮助信息。如果省略 `command`，则显示所有 `ftp` 命令的列表。 |
| `lcd localDirectory` | 将你当前的本地工作目录更改为 `localDirectory`。 |
| `ls remoteDirectory` | 列出你当前远程工作目录的内容。 |
| `mkdir remoteDirectory` | 在远程主机上创建远程 `remoteDirectory`。 |
| `open hostName [ port ]` | 尝试连接到名为 `hostName` 的主机。如果你指定了可选的端口号，`ftp` 将假设该端口是 `ftp` 服务器。 |
| `put localFile [ remoteFile ]` | 将本地文件 `localFile` 复制到远程文件 `remoteFile`。如果省略 `remoteFile`，则将使用与本地文件相同的名称。 |
| `pwd` | 显示你当前的远程工作目录。 |
| `quit` | 与 `bye` 相同。 |
| `rename remoteFrom remoteTo` | 将远程文件从 `remoteFrom` 重命名为 `remoteTo`。 |
| `rmdir remoteDirectory` | 删除远程目录 `remoteDirectory`。 |

`ftp` 程序中的命令。

# 分布式处理

当你开始在网络中移动并登录不同的主机时，分布式系统的威力就变得引人注目。某些主机提供带有如 `"guest"` 等用户 ID 的限制密码账户，让探索者可以在不造成任何伤害的情况下漫游网络，尽管越来越多的人滥用这种权限，这种做法正在消失。如今，为了登录网络，你几乎必须在远程计算机上有一个账户。用于分布式访问的三种实用是：

- `login`，允许你登录到远程 UNIX 主机，
- `rsh`，允许你在远程 UNIX 主机上执行命令，
- `telnet`，允许你在任何带有 `telnet` 服务器的远程主机上执行命令。

在这些工具中，`telnet` 是最灵活的，因为除了 UNIX 外还有其他系统支持 `telnet` 服务器。

## 远程登录：`login`

要登录远程主机，请使用图 9.20 的 `login`。在下面的示例中，我从本地主机 `"csservrv2"` 登录远程主机 `"vanguard"`，执行了：

```
Utility: login -ec [-UserId]hostName
```

`login` 尝试登录到远程主机 `hostName`。如果你没有通过 `-l` 选项提供 ID，则在登录过程中使用你的本地用户 ID。

如果远程主机没有在 `"$HOME/.root"` 文件中设置为本地主机的等效主机，会被要求远程主机的密码。一旦连接，你的本地 shell 将进入睡眠状态，远程 shell 开始执行。当你完成远程登录后，以正常方式终止它（通常使用 `Control-D`），你的本地 shell 就会唤醒。

你可能会输入几个具有特殊含义的特殊“转义命令”；每个命令前面都有转义字符，默认是波浪号 (`~`)。你可以通过在 `-e` 选项后跟随偏好的转义字符来更改此转义字符。以下是转义命令列表：

| 序列 | 说明 |
| --- | --- |
| `~` | 立即断开远程主机的连接。 |
| `~susp` | 暂停远程登录会话。使用 `fg` 重启远程登录。 |
| `~dsusp` | 暂停远程登录会话的输入，但仍将会话的输出显示到本地终端。 |

图 9.20

`login` 命令的描述。

`date` 工具，并在断开时：

```
$ login vanguard ...远程登录。
Last login: May 19 17:23:51 from csserv2
vanguard% date ...在 vanguard 上执行命令。
Wed May 20 18:50:47 CDT 1998
vanguard%^ ...终止远程 shell。
Connection closed.
$ ...回到 csserv2！
```

## 执行远程命令：`rsh`

如果你只想在远程主机上执行单个命令，`rsh` 展示了它的工作的。在示例示例（图 9.21），我分别在本地“csserv2”主机和远程“vanguard”主机上执行了 `hostname` 工具：

```
$ hostname ...在本地主机上执行。
csserv2
$ rsh vanguard hostname ...在远程主机上执行。
vanguard
$_
```

```
Utility: rsh [-l userId] hostName [command]
```
