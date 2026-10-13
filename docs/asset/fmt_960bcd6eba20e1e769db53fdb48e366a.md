
本节描述的其他命令更特定于 Red Hat Linux 和其他 UNIX 系统，但它们提供了在受信任系统之间复制文件、登录和执行命令的简化方法：分别是 `rcp`、`rlogin` 和 `rsh`。此外，Red Hat Linux 还包含一种更安全的远程登录工具，称为 `ssh`。`ssh` 命令也可用于远程执行。

### 使用 telnet 进行远程登录

`Telnet` 是一种由许多不同类型的计算机系统提供的服务，用于使远程用户能够通过 TCP/IP 网络登录到其机器。`telnet` 命令是您用于进行远程登录的客户端程序。使用 `telnet` 最常见的方式是使用主机名。以下是一个典型的 `telnet` 会话：

```
$ telnet maple
Trying 10.0.0.11 ...
Connected to maple (10.0.0.11).
Escape character is '^]'.
Red Hat Linux
Kernel 2.4.20-8 on an i686
login: mike
Password: ********
Last login: Mon Mar 31 13:15:57 from pine
[mike@maple mike]$
```

此示例显示了使用 `telnet` 命令从名为 `pine` 的计算机登录到名为 `maple` 的计算机时会发生什么，输入 `telnet maple`。我的计算机尝试连接到 `maple` 上的 `telnet` 端口（IP地址 10.0.0.11）。由于 `maple` 也是 Red Hat Linux 计算机，一旦连接建立，我会看到标准的 `login:` 提示。我在提示时输入用户名（`mike`）和密码。当登录名和密码被接受时，我会看到名为 `mike` 的用户的 shell 提示符。

Red Hat Linux 系统默认禁用 `telnet` 服务（大多数网络服务也是如此）。因此，要能够使用 `telnet` 登录到您的计算机，请参阅附录 C，了解如何启用 `telnet` 服务的信息。

以下是您可以使用 `telnet` 的一些有用选项：

- `-a` - 自动登录。使用此选项，您的计算机尝试使用本地用户名登录到远程计算机。因此，如果您以 `mike` 登录到自己的计算机，当您使用 `telnet` 登录到远程计算机时，远程计算机假定您想以 `mike` 登录。它只需提示您输入 `mike` 的密码。
- `-l user` - 用户名。此选项类似于 `-a` 选项，只是您可以使用您选择的任何用户名登录，而不是使用当前用户名。
- `-r` — Rlogin 风格界面。此选项让您可以使用波浪线（`~`）选项。例如，要在 rlogin 模式下断开连接，请输入 `~.`（波浪线+句点），或要挂起 `telnet` 会话，请输入 `~~z`（波浪线+Ctrl+z）。只有在远程 shell 挂起时才使用 `~.`（`exit` 是正常退出更好的方式）。如果您使用 `~~z` 暂时挂起已挂起的会话，您将被返回到本地系统 shell。要返回到已挂起的会话，请输入 `fg` 将 `telnet` 放回前台。请参阅本章后面 `rlogin` 的描述，了解 rlogin 模式下可使用的更多功能。

另一种使用 `telnet` 的方式是在命令模式下。不要使用主机名，只需输入单词 `telnet`。您将看到如下 `telnet` 提示符：

```
$ telnet
telnet>
```

此时，您可以使用多个命令。您尚未连接到远程主机。要从 `telnet` 提示符打开到远程计算机的登录会话（例如，到名为 `maple` 的计算机），请输入：

```
telnet> open maple
```

连接远程计算机后，您可以随时通过键入 Ctrl+] 返回到 `telnet` 会话。以下是您在 `telnet` 会话期间可使用的其他选项：

- `?` — 打印帮助信息。
- `!` — 转义到 shell。
- `close` — 如果您有打开的连接，输入 `close` 以关闭它。
- `display` — 显示当前生效的操作参数。
- `logout` — 注销此会话中的任何远程连接并关闭它。
- `mode` — 尝试进入行模式或字符模式。（输入 `mode ?` 可查看 `mode` 选项的其他选项。）
- `quit` — 关闭 `telnet` 并退出。
- `z` — 挂起当前 `telnet` 会话。

如果您挂起 `telnet` 会话或转义到 shell，请通过键入 `fg` 返回 `telnet`。

## 使用 FTP 复制文件

与 `telnet` 类似，`FTP` 是一种可在许多不同操作系统上使用的协议。Internet 上的文件归档存储在称为 FTP 服务器的地方。要从 Red Hat Linux 连接到这些服务器，您可以将其服务器的 URL 输入到 Web 浏览器中，也可以使用 `ftp` 命令或图形 FTP 窗口（如 `gFTP`）。在 Red Hat Linux 提供的其他 FTP 客户端程序中，我最喜欢的是 `ncftp` 命令。

### 使用 ftp 命令

`ftp` 命令可在 Red Hat Linux 上使用，也可在每台 Linux 和 UNIX 系统上使用，用于将文件复制到 FTP 服务器和从 FTP 服务器复制文件。与 `telnet` 类似，`FTP` 具有命令模式，或者（更典型地）您可以使用它直接连接到远程计算机。例如：

```
$ ftp maple
Connected to maple.
220 (vsFTpd 1.1.3)
Name (maple:mike): jake
331 Please specify the password.
Password: ********
230 Login successful. Have fun.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp>
```

在此示例中，`ftp` 连接到名为 `maple` 的计算机（`ftp maple`）。当提示输入名称时，它假定我将使用我在 `maple` 上的当前登录名（`maple:mike`）。我本可以按 Enter 使用名称 `mike`，但我改为以 `jake` 登录并在提示时输入密码。密码被接受，并在打印一些信息后，我被给予 `ftp>` 提示符。

由于 FTP 用于公共服务器，您通常可以使用 `anonymous` 作为用户名登录。通过输入有效的电子邮件地址作为密码，您可以进入匿名 FTP 站点并下载服务器向公众提供的文件。

与 `telnet` 不同，FTP 登录后我没有进入常规的 UNIX shell，而是进入了 FTP 命令模式。FTP 的命令模式包含大量用于在远程文件系统中移动以及复制文件（这是其主要任务）的命令。

### FTP 目录命令

为了熟悉环境并在远程文件系统中移动，您可以从 `ftp>` 提示符使用以下一些命令。这些命令用于处理与 FTP 连接相关的远程和本地目录。

- `pwd` — 显示远程系统上当前目录的名称。
- `ls` — 使用 UNIX `ls` 命令列出当前远程目录的内容。您可以使用任何有效的 `ls` 选项，前提是所连接的特定 FTP 服务器支持这些选项。
- `dir` — 与 `ls` 相同。
- `cd` — 使用 `cd` 命令移动到指定的目录。
- `cdup` — 在文件系统中向上移动一个目录。
- `lcd` — 列出当前本地目录的名称。

如果你想对远程文件或目录进行任何更改，请使用以下命令：

- `mkdir` — 在远程系统上创建目录。
- `rename` — 重命名远程系统上的文件或目录。
- `rmdir` — 删除远程目录。
- `delete` — 删除远程文件。
- `mdelete` — 删除多个远程文件。

根据 FTP 服务器的配置，你可能能够或不能执行上面显示的一些文件和目录命令。一般来说，如果你以匿名用户登录，你将无法修改任何文件或目录。你只能下载文件。如果你有一个真实的登录账户，你通常会拥有与使用标准登录提示进入计算机时相同的读写权限。

## FTP 文件复制命令

在远程系统和本地系统之间复制文件之前，请考虑你想要进行的传输类型。传输模式有两种类型：

- `binary` — 用于传输二进制文件（如数据文件和可执行命令）。这也被称为映像传输。
- `ascii` — 用于传输纯文本文件。

Linux `ftp` 命令似乎在启动 FTP 时将默认设置设为 `binary`。`Binary` 对于二进制或文本文件似乎都能很好地工作。然而，`binary` 传输可能无法正确传输来自非 UNIX 系统的 `ascii` 文件。如果你以 `ascii` 模式传输可执行文件，当你尝试在本地系统上运行时，该文件可能无法工作。

大多数文件复制都是使用 `get` 和 `put` 命令完成的。同样，你也可以使用 `mget` 和 `mput` 命令一次传输多个文件。一些 FTP 服务器甚至允许你使用匹配字符（例如，`get abc*` 获取所有以字母 `abc` 开头的文件）。以下是这些命令的描述：
