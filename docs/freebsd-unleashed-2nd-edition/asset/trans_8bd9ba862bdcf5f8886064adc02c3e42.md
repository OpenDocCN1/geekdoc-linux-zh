

![](img/48eec858cce7dfb89da36a4d40b7daf3_151_0.png)

**图 6.9** 使用 1 命令调用 xmixer 时的 xgmixer。功能保持不变，但由于此版本使用 GTK 工具包而非 Athena 工具包，外观有所不同。

## 网络应用程序

FreeBSD 上有许多可用的网络应用程序。本节将重点介绍 Web 浏览器、电子邮件、FTP 等。

### 配置 Netscape

Netscape Communicator Web 浏览器可用于 FreeBSD。FreeBSD 上可用的最新版本是 4.8。如果您想运行 Netscape 7，则需要运行 FreeBSD 中的 Linux 版 Netscape。此外，如果您想使用大多数插件（如 Flash 和 Shockwave），也需要运行 Linux 版本。这些插件仅适用于 Linux 版本的 Netscape。在 FreeBSD 中运行 Linux 版 Netscape 允许您使用这些插件。

所有 Netscape 浏览器（包括 Linux 版本）均可作为 ports 目录中的 www 条目提供。这允许您像安装普通的 FreeBSD 应用程序一样安装和运行 Linux 版本。

安装 Netscape 后，可以使用命令 `netscape`（适用于 Netscape 4.8）或命令 `netscape7`（适用于 Netscape 7）来启动它。本节将介绍 Netscape 4.8，但 Netscape 7 与之类似。

大多数用户可能之前使用过 Netscape，FreeBSD 中的配置与 Windows 中的配置相同。要更改 Netscape 选项，请单击菜单栏中的 Edit（编辑），然后单击 Preferences（首选项）。这将打开如图 6.10 所示的配置对话框。

要配置各种 Netscape 设置，请单击所需选项类别旁边的加号 (+) 以展开它。然后，单击您想要配置的项目，在窗口右侧打开其配置对话框。

### Lynx Web 浏览器

Lynx 是一个以文本模式运行且没有图形功能的 Web 浏览器。虽然它仍可使用，但由于它不支持图像、框架或 Java，使用 Lynx 浏览 Web 变得越来越困难。由于许多网站使用图像作为链接且未使用 ALT 标签，这会导致 Lynx 中的导航问题，这些问题很难或不可能绕过。图 6.11 显示了加载了 FreeBSD Web 网站的 Lynx。

![](img/48eec858cce7dfb89da36a4d40b7daf3_152_0.png)

**图 6.10** Netscape 的配置对话框。它与在 Windows 中配置 Netscape 类似。

![](img/48eec858cce7dfb89da36a4d40b7daf3_152_1.png)

**图 6.11** Lynx 中的 FreeBSD Web 网站。

Lynx 仍然可以在许多网站上工作，尽管导航并不总是很容易。使用箭头键在浏览器窗口中的链接之间移动。空格键将前进到下一页。输入 **G** 可以切换到不同的 Web 网站。输入 **G** 后，系统将提示您输入 URL。**Q** 在询问您是否确定要退出后退出 Lynx。

有关 Lynx 的更多信息（包括自定义选项），请通过输入 `man lynx` 查看 Lynx 手册页。

## FTP

FTP（*File Transfer Protocol*，文件传输协议）是一种在系统之间传输文件的方法。虽然它不再经常直接使用（通常，通过点击网站链接从 FTP 下载文件），但如果您需要将文件传输到另一台服务器，知道这一点仍然很有用。

要开始 FTP 会话，请在 shell 提示符或 X-terminal 中输入 **ftp**，后接您想要连接的服务器名称。例如，要连接到 FreeBSD FTP 服务器，您应输入以下内容：

```
ftp ftp.freebsd.org
```

完成此操作后，假设连接成功，您最终会看到类似以下内容：

```
Connected to ftp.beastie.tdk.net.
220 ftp.beastie.tdk.net FTP server (Version DG-4.1.73 983302105) ready.
Name (ftp.freebsd.org:murban):
```

在 **Name**（名称）提示符下，您需要输入 FTP 服务器的登录名。如果您的登录名与您当前所在系统的登录名相同，您可以直接按 Enter 键而不输入名称，系统将使用您的本地登录名。

如果您没有该系统的登录名，可以使用名称 **anonymous**（匿名）登录到公共 FTP 服务器。例如，这就是您登录到 FreeBSD FTP 服务器的方式。一旦您输入 anonymous 作为用户名并按下 Enter 键，远程主机将响应类似以下内容：

```
331 Guest login ok, send your e-mail address as password.
Password:
```

只需按说明操作，将您的电子邮件地址作为密码输入。请注意，密码不会回显到您的屏幕上。

登录成功后，您可能会收到欢迎消息，最后看到类似以下内容：

```
Remote system type is UNIX.
Using binary mode to transfer files.
ftp>
```

在提示符下，您可以使用许多与本地 shell 中使用的相同的 shell 命令在 FTP 服务器中导航。有关如何操作 shell 命令的详细信息，请参阅第 7 章。表 6.9 提供了一些在 FTP 会话中最常用命令的列表。

**表 6.9** 常用 FTP 命令

| 命令 | 操作 |
| :--- | :--- |
| ls | 列出远程主机的目录内容。 |
| cd | 更改远程主机的目录。 |
| pwd | 显示您在远程主机上所在的当前目录。 |
| lcd | 更改本地主机的目录。 |
| binary | 以二进制模式传输文件（除了纯文本外，应使用此模式）。 |
| ascii | 以 ASCII 模式传输文件（此模式应*仅*用于纯文本）。请注意，在大多数情况下，纯文本也可以以二进制模式传输，且不会有问题。 |
| put *filename* | 将 *filename* 复制到远程主机。除非指定了路径，否则假设 *filename* 位于当前目录中。如果未指定目标文件，文件将放置在远程主机的当前目录中，并具有与本地文件相同的名称。（此命令仅在您有权限写入远程机器目录时有效。） |
| mput *file1 file2* | 将列表中的多个文件复制到远程主机。文件将放置在远程主机的当前目录中。（此命令仅在您有权限写入远程机器目录时有效。） |
| get *filename* | 将文件从远程主机复制到本地系统。如果未指定路径，则假设文件位于远程主机的当前目录中。如果未指定目标文件，文件将使用相同的文件名复制到本地系统。 |
| mget *file1 file2* | 从远程主机获取列表中的多个文件。文件将放置在本地系统的当前目录中。 |
| mkdir *dirname* | 在远程机器上创建一个名为 *dirname* 的目录（假设您有权限这样做）。 |
| rmdir *dirname* 或 rm *dirname* | 删除远程机器上名为 *dirname* 的目录（假设您有权限这样做）。 |
| del *filename* | 从远程机器中删除文件 *filename*（假设您有权限这样做）。 |
| bye 或 quit | 关闭与远程主机的连接并退出 FTP 程序，返回 shell 提示符。 |

您还可以在 `ftp>` 提示符下输入 **help** 以获取可用命令的列表。输入 **help** 后接列表中的一个命令，即可获取该命令功能的简短描述。以下是一个示例：

```
ftp> help
Commands may be abbreviated. Commands are:

!  disconnect  mdelete    preserve   runique
$  edit       mkdir      progress   send
   account    exit       get        prompt     sendport
   append     form       mkdir      proxy      site
   ascii      ftp        mls        put        size
   bell       get        mode       pwd        status
   binary     gate       mdtimes    quit       struct
   bye        glob       more       quote      sunique
   case       hash       mput       recv       system
   cd         help       msand      reget      tenex
   cdup       idle       newer      rename     trace
   chmod      image      nlist      reset      type
   close      lcd        nmap       restart    umask
   cr         less       ntrans     restrict   user
   debug      lpwd       open       rhelp      verbose
   delete     ls         page       rmdir      ?
   dir        macdef     passive    rstatus
```

```
ftp> help mdir
mdir list contents of multiple remote directories
ftp>
```

有关使用 FTP 的更多信息，请在 shell 提示符下输入 `man ftp` 阅读 FTP 的手册页。您可能还想阅读第 7 章中关于文件操作命令的部分，因为 FTP 中使用的命令与之相似。

以下展示了一个示例 FTP 会话的可能样子：

```
bash$ ftp ftp.freebsd.org
Connected to ftp.beastie.tdk.net.
220 ftp.beastie.tdk.net FTP server (Version DG-4.1.73 983302105) ready.
Name (ftp.freebsd.org:murban): anonymous
331 Guest login ok, send your e-mail address as password.
Password:
230 Guest login ok, access restrictions apply.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> ls
227 Entering Passive Mode (62,243,72,50,88,26)
150 Opening ASCII mode data connection for 'file list'.
total 2
```

