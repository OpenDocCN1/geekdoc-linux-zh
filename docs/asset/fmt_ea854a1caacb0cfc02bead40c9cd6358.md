
FileZilla 是适用于 Windows 和 Linux 的另一个 GUI FTP 客户端。它与 gFTP 相似，但其开发仍在继续（而 gFTP 的开发已停止）。这两个程序在外观和操作上相似。你可以在 `https://filezilla-project.org` 找到 FileZilla（如图 2-2 所示）。它适用于所有发行版以及 GNOME 和 KDE。

图 2-2：

从此站点下载 FileZilla。

![](img/322157d1fa7d965f05bcd68ed0ffc36b_236_1.png)

当主 FileZilla 窗口出现时，它以类似于 Windows 资源管理器的方式显示你的主文件夹。要连接到 FTP 服务器，输入远程主机的名称或 IP 地址，以及登录远程主机所需的用户名和密码。图 2-3 显示了你在填写这些信息并与远程主机建立连接后 FileZilla 窗口的外观。

![](img/322157d1fa7d965f05bcd68ed0ffc36b_237_0.png)

图 2-3：

FileZilla 窗口显示本地目录和远程 FTP 服务器的目录。

现在你可以使用 FileZilla 上传或下载文件，就像使用 gFTP 一样。

FTP 传输变得就像普通的拖放文件复制：通过将文件从一个系统的文件夹拖动并放到另一个系统的文件夹上来传输文件。

完成后，选择 `File→Quit`。

### 将网络浏览器用作 FTP 客户端

任何网络浏览器都可以充当 FTP 客户端，但此类程序最适合匿名 FTP 下载，在这种情况下，网络浏览器可以使用匿名用户名和任何密码登录。

例如，你可以使用 Firefox 网络浏览器作为 FTP 客户端。你需要知道的全部就是如何编写 URL，以便网络浏览器能够识别你想要使用 FTP 下载文件。FTP URL 的语法是

```
ftp://hostname/pathname
```

第一部分（`ftp://`）表示你想要进行 FTP 传输。`hostname` 部分是 FTP 服务器的名称（通常以 `ftp` 开头，如 `ftp.wiley.com`）。`pathname` 是你想要下载的文件的完整目录路径和文件名。

如果你仅提供 FTP 服务器的主机名，网络浏览器会显示匿名 FTP 目录的内容。如果你想在 Linux 系统上访问匿名 FTP，启动 Firefox（在 GNOME 面板上点击网络浏览器图标），在位置文本框中输入 FTP URL，然后按 Enter。

图 2-4 显示了 Firefox 中典型的 FTP 目录。你可以点击文件夹查看其内容并下载任何文件。你可以使用 Firefox 的 FTP 功能访问本地系统。例如，输入 `ftp://localhost/pub/` 来访问 `pub` 目录。（如果你没有运行 FTP 服务器或已设置防火墙不允许 FTP 连接，则系统不会响应。）

![](img/322157d1fa7d965f05bcd68ed0ffc36b_238_0.png)

图 2-4：

你可以使用网络浏览器从 FTP 服务器下载文件。

![](img/322157d1fa7d965f05bcd68ed0ffc36b_238_1.png)

在 Debian 和 Fedora 中，以 root 身份登录并在终端窗口中输入 `/etc/init.d/vsftpd start` 来启动 FTP 服务器。在 SUSE 中，`xinetd` 超级服务器控制 FTP 服务器 `vsftpd`。`/etc/xinetd.d/vsftpd` 配置文件指定了 `vsftpd` 的启动方式。（有关 `xinetd` 配置文件的更多信息，请参阅第 5 书第 1 章。）

如果你输入其他匿名 FTP 服务器的主机名，访问匿名 FTP 站点的相同方法也适用。尝试输入 URL `ftp://ftp.wiley.com/`。你将获得 `ftp.wiley.com` 服务器的目录。

## 使用命令行 FTP 客户端

![](img/322157d1fa7d965f05bcd68ed0ffc36b_239_0.png)

从命令行使用 FTP 是一个好主意。例如，如果你的 GUI 桌面无法工作，你可能需要下载一些文件来修复问题；如果你知道如何使用命令行 FTP 客户端就可以做到。命令行 FTP 客户端在所有 Linux 发行版中都可用，使用起来并不困难。

了解命令行 FTP 客户端的最佳方式就是尝试它。命令是 `ftp`，你可以在 Linux 系统中尝试 `ftp` 命令。甚至不需要互联网连接，因为你可以使用 `ftp` 命令连接到自己的系统。

![](img/322157d1fa7d965f05bcd68ed0ffc36b_239_1.png)

注意：你从 `ftp` 命令获得的输出可能与本书中显示的不同，因为某些发行版（如 Debian）使用 gFTP 的文本模式版本作为命令行 FTP 客户端。

在下面的示例 FTP 会话中，命令行 FTP 客户端用于登录并浏览 Linux 系统上的目录。以下是列表，展示了与典型命令行 FTP 客户端的交互：

```
ftp localhost
Connected to localhost.localdomain.
220 (vsFTPd 2.0.3)
Name (localhost:jdoe): (press Enter.)
331 Please specify the password.
Password: (enter the password for the user.)
230 Login successful.
Remote system type is Unix.
Using binary mode to transfer files.
ftp> help
Commands may be abbreviated. Commands are:
!       debug      mdir      qc        send
$       dir        mget      sendport  site
account disconnect mkdir     put       size
append  exit       mls       pwd       status
ascii   form       mode      quit      struct
bell    get        modtime   quote     system
binary  glob  mput  recv  sunique
bye     hash  newer reget tenex
case    help  nmap  rstatus tick
cd      idle  nlist rhelp  trace
cdup    image ntrans rename type
chmod   lcd   open  reset  user
close   ls    prompt restart umask
cr      macdef passive rmdir verbose
delete  mdelete proxy runique ?
ftp> help mget (to get help on a specific command.)
mget get multiple files
ftp> cd /var (This changes directory to /var.)
250 Directory successfully changed.
ftp> ls (This command lists the contents of the directory.)
227 Entering Passive Mode (127,0,0,1,38,142)
150 Here comes the directory listing.
. . . lines deleted . . .
226 Directory send OK.
ftp> bye (This command ends the session.)
```

如列表所示，你可以通过输入命令 `ftp hostname` 启动命令行 FTP 客户端，其中 `hostname` 是你想要访问的系统的名称。当 FTP 客户端与远程系统上的 FTP 服务器建立连接时，FTP 服务器会提示你输入用户名和密码。提供信息后，FTP 客户端会显示 `ftp>` 提示符，你可以开始输入命令执行特定任务。如果记不起某个特定的 FTP 命令，输入 `help` 查看命令列表。你可以通过输入 `help command` 获取特定命令的额外帮助，其中 `command` 是你想要帮助的命令。

许多 FTP 命令与用于导航文件系统的 Linux 命令类似。例如，命令 `cd` 更改目录；`pwd` 打印当前工作目录的名称；`ls` 列出当前目录的内容。另两个常用命令是 `get`，它从远程系统下载文件到你的系统，以及 `put`，它将文件从你的系统上传（发送）到远程主机。

表 2-1 描述了一些常用的 FTP 命令。你不必输入完整的 FTP 命令。对于较长的命令，只需输入前几个字符——足以唯一标识该命令即可。例如，要删除文件，可以输入 `dele`；要将文件传输模式更改为二进制，可以输入 `bin`。

## 表 2-1 常用 FTP 命令
