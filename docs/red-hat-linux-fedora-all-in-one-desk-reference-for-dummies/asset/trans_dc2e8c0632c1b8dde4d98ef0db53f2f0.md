
上传文件时，你需要使用 gFTP，因为此类传输通常需要提供用户名和密码。Web 浏览器对于匿名下载效果很好，而这正是你通常从互联网下载软件的方式。

我将在接下来的两个章节中简要介绍这两种 GUI FTP 客户端。

## 使用 gFTP

GNOME 自带 gFTP，这是一款图形化 FTP 客户端。要启动 gFTP，请从 GNOME 或 KDE 桌面选择 主菜单→Internet→更多 Internet 应用→gFTP。gFTP 窗口出现（如图 4-1 所示）。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_417_0.png)

图 4-1：
打开到远程 FTP 服务器的连接之前的 gFTP 窗口。

gFTP 窗口有一个菜单栏，其中包含用于执行各种任务的菜单。菜单栏正下方是一个工具栏，包含多个按钮和文本字段。在这里你可以输入远程主机的名称或 IP 地址、登录远程主机所需的用户名和密码。图 4-1 显示了你在填写这些信息后 gFTP 窗口的情形。

使用 gFTP 上传或下载文件，请按以下步骤操作：

- 1. 在 Host 字段中填写远程系统的主机名或 IP 地址。

如果你之前使用过该主机，可以从 Host 字段旁的向下指向箭头出现时显示的下拉列表中选择它。

- 2. **在 User 字段中提供用户名，在 Pass 字段中提供密码，然后单击显示两台计算机图标的按钮（位于 Host 字段左侧）。**

此操作会使 gFTP 连接到你选择的主机，并使用你提供的用户名和密码登录。gFTP 窗口的下半部分显示两台系统之间交换的 FTP 协议消息。

- 3. **观察此区域是否有任何错误消息的提示。**

远程系统的目录列表显示在 gFTP 窗口的右半部分。左半部分显示当前本地目录。

- 4. **要将一个或多个文件从当前系统上传到远程系统，请在左侧列表中选择文件，然后单击右箭头按钮。**

- 5. **要从远程系统下载文件，请在右侧列表中选择文件名，然后单击左箭头按钮。**

- 6. **完成文件传输后，从菜单中选择 FTP→Quit。**

如这些步骤所示，使用 gFTP 等 GUI FTP 客户端传输文件是一项简单的任务。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_418_0.png)

信不信由你，gFTP 不仅用于 FTP 传输。它还可以使用 HTTP 协议传输文件，并使用 Secure Shell（SSH）协议进行安全文件传输。

## 使用 Web 浏览器作为 FTP 客户端

任何 Web 浏览器都可以充当 FTP 客户端，但此类程序最适合匿名 FTP 下载，在这种情况下 Web 浏览器可以使用匿名用户名和任意密码登录。

在 Red Hat Linux 中，你可以使用 Mozilla Web 浏览器作为 FTP 客户端。你需要知道的全部是如何编写 URL，以便 Web 浏览器能够识别你想要使用 FTP 下载文件。FTP URL 的语法如下：

```
ftp://hostname/pathname
```

第一部分（ftp://）表示你想要进行 FTP 传输。hostname 部分应为 FTP 服务器的名称（名称通常以 ftp 开头——例如 ftp.netspace.com）。pathname 是你想要下载的文件的完整目录路径和文件名。

```
ftp://localhost
```

然后按 Enter。Mozilla 显示 Red Hat Linux 系统上匿名 FTP 目录的内容。图 4-2 显示了 Mozilla 中匿名 FTP 目录的典型外观。你可以单击文件夹查看其内容并下载任何文件。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_419_0.png)

图 4-2：
你可以使用 Mozilla 从匿名 FTP 服务器下载文件

![](img/a7eec43a54473e95dc5ea333fecf1bd7_419_1.png)

当你使用 `ftp://localhost` URL 时，如果你没有运行 FTP 服务器或已设置防火墙不允许任何 FTP 连接，则系统不会给出响应。在你的系统上，以 root 身份登录并在终端窗口中输入 `service vsftpd start` 来启动 FTP 服务器。

如果你输入其他匿名 FTP 服务器的主机名，采用相同的方法访问匿名 FTP 站点也是可行的。例如，尝试输入以下 URL：

```
ftp://ftp.netscape.com
```

你应该会得到 `ftp.netscape.com` 服务器的目录。

## 使用命令行 FTP 客户端

了解如何从命令行使用 FTP 是很有用的——以防万一。例如，你的 GUI 桌面可能无法工作，而你需要做的是下载一些文件来修复问题。如果你知道如何使用命令行 FTP 客户端，你就可以下载文件并解决问题。这并不难。

学习命令行 FTP 客户端的最佳方法是实际尝试一下。该命令称为 ftp，你可以在 Red Hat Linux 系统上尝试 ftp 命令。你甚至不需要任何 Internet 连接，因为你可以使用 ftp 命令连接到自己的系统——我会向你展示如何操作。

在下面的示例 FTP 会话中，我使用命令行 FTP 客户端使用我的用户名（naba）登录并浏览系统上的目录。当你尝试类似操作时，请将名称替换为你的用户名并提供你的密码。以下是显示命令的列表（我的注释以斜体显示）：

```
ftp localhost
Connected to localhost (127.0.0.1).
220 (vsFTPd 1.2.0)
Name (localhost:naba): (I press Enter.)
331 Please specify the password.
Password: (I type my password.)
230 Login successful. Have fun.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> help (I type help to see a list of FTP commands.)
Commands may be abbreviated. Commands are:
! debug mdir sendport site
$ dir mget put size
account disconnect mkdir pwd status
append exit mls quit struct
ascii form mode quote system
bell get modtime recv sunique
binary glob mput rget tenex
bye hash newer rstatus tick
case help nmap rhelp trace
cd idle nlist rename type
cdup image ntrans reset user
chmod lcd open prompt restart umask
close ls passive rmdir runique verbose
cr macdef mdelete proxy send
delete mdelete proxy send
ftp> help mget (I can get help on a specific command.)
mget get multiple files
ftp> cd /var/ftp (This changes directory to /var/ftp.)
250 Directory successfully changed.
ftp> ls (This command lists the contents of the directory.)
227 Entering Passive Mode (127,0,0,1,248,180)
150 Here comes the directory listing.
drwxr-xr-x 2 0 0 4096 Jun 26 05:10 pub
226 Directory send OK.
ftp> bye (This command ends the session.)
221 Goodbye.
```

如列表所示，你可以通过输入命令 ftp hostname 启动命令行 FTP 客户端，其中 hostname 是你想要访问的系统的名称。当 FTP 客户端与远程系统上的 FTP 服务器建立连接时，FTP 服务器会提示你输入用户名和密码。提供信息后，FTP 客户端会显示 ftp> 提示符，你可以开始输入命令执行特定任务。如果你记不起某个特定的 FTP 命令，输入 help 即可查看列表。你可以通过输入 help command 获取特定命令的额外帮助，其中 command 是你想要了解的内容。

许多 FTP 命令与用于浏览文件系统的 Linux 命令相似。例如，cd 更改目录，pwd 打印当前工作目录的名称，ls 列出当前目录的内容。另两个常见命令是 get 和 put——get 用于从远程系统下载文件到你的系统，put 则上传（发送）文件从你的系统到远程主机。

表 4-1 描述了一些常用的 FTP 命令。你不必输入完整的 FTP 命令。对于较长的命令，只需输入前几个字符——足以唯一标识该命令即可。例如，要删除文件，可以输入 dele，要将文件传输模式更改为二进制，可以输入 bin。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_421_0.png)

从互联网下载文件时，你几乎总是希望以二进制模式传输文件，因为软件通常以二进制形式归档和压缩（其文件不是纯文本文件）。因此，始终使用 binary 命令将模式设置为二进制。然后使用 get 命令下载文件。

表 4-1 常用 FTP 命令

| 命令 | 描述 |
|---|---|
| ! | 在本地系统上执行 shell 命令。例如，! ls 列出远程系统上当前目录的内容。 |
| ? | 显示命令列表（与 help 相同）。 |
| append | 将本地文件追加到远程文件。 |
| ascii | 将文件传输类型设置为 ASCII（或纯文本）。这是默认的文件传输类型。 |
| binary | 将文件传输类型设置为二进制。 |
| bye | 结束与远程 FTP 服务器的 FTP 会话并退出 FTP 客户端。 |
| cd | 更改远程系统上的目录。例如，cd /pub/Linux 将远程目录更改为 /pub/Linux。 |
