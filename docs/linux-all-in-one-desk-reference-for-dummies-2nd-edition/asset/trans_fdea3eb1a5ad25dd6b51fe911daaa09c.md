

首次启动 KDE 时，系统会运行 KBear 向导（KBear Wizard），以便你配置 KBear。此配置步骤主要涉及 KBear 窗口的布局，因此你可以直接接受默认设置。

当主 KBear 窗口出现时，它会以类似 Windows 资源管理器的视图显示你的主目录。要连接到 FTP 服务器，请选择“FTP > 快速连接”（FTP>Quick Connect）。随后会弹出一个对话框（见图 4-2），提示你输入 FTP 服务器的主机名以及用户名和密码。

+ 图 4-2：输入远程 FTP 服务器的信息并点击“连接”。

![](img/792720823146d68f19fd50c99ebfce4b_389_0.png)

输入所需信息后，点击“连接”（Connect）。KBear 将建立与远程 FTP 服务器的连接。在图 4-3 所示的 KBear 主窗口中，你可以并排看到本地目录和远程目录。

现在，你可以通过将一个系统的文件夹中的文件拖动到另一个系统的文件夹中来传输文件，从而使得 FTP 传输就像普通的拖放文件复制一样简单。

使用完 KBear 后，请选择“FTP > 退出”（FTP>Quit）或点击工具栏最左侧的“电源”（Power Off）按钮。

## 使用 Web 浏览器作为 FTP 客户端

任何 Web 浏览器都可以充当 FTP 客户端，但此类程序最适合用于匿名 FTP 下载，因为 Web 浏览器可以使用用户名 anonymous（匿名）和任意密码进行登录。

### 使用图形化 FTP 客户端

![](img/792720823146d68f19fd50c99ebfce4b_390_0.png)

图 4-3：KDeer 窗口并排显示本地目录和远程 FTP 服务器的目录。

例如，你可以使用 Firefox Web 浏览器作为 FTP 客户端。你只需要知道如何编写 URL，以便让 Web 浏览器知道你想使用 FTP 下载文件。FTP URL 的语法如下：

```
ftp://hostname/pathname
```

第一部分（ ftp:// ）表示你想要进行 FTP 传输。*hostname* 部分是 FTP 服务器的名称（名称通常以 ftp 开头——例如，ftp.netscape.com）。*pathname* 是你想要下载的文件所在的全目录路径和文件名。

如果你只提供 FTP 服务器的主机名，Web 浏览器将显示匿名 FTP 目录的内容。如果你想在你的 Linux 系统上访问匿名 FTP，请启动 Firefox（点击 GNOME 面板上的 Web 浏览器图标），在“位置”（Location）文本框中输入 FTP URL，然后按 Enter。例如，在我的系统上，我输入 ftp://localhost/pub/ 来访问 pub 目录。

图 4-4 展示了 Firefox 中匿名 FTP 目录的典型外观。你可以点击文件夹查看其内容并下载任何文件。虽然我展示了如何使用 Firefox 的 FTP 功能访问本地系统，但 FTP 的目的（当然是）从其他系统下载文件到你的系统。

图 4-4：你可以使用 Web 浏览器从匿名 FTP 服务器下载文件。

![](img/792720823146d68f19fd50c99ebfce4b_391_0.png)

**警告！**

当你使用 ftp://localhost/ URL 时，如果你没有运行 FTP 服务器，或者你设置了防火墙不允许 FTP 连接，系统将不会给出响应。

![](img/792720823146d68f19fd50c99ebfce4b_391_1.png)

在 Debian 和 Fedora Core 中，以 root 身份登录并在终端窗口中输入 /etc/init.d/vsftpd start 以启动 FTP 服务器。在 SUSE 中，xinetd 超级服务器控制 FTP 服务器 vsftpd。/etc/xinetd.d/vsftpd 配置文件指定了如何启动 vsftpd。有关 xinetd 配置文件的更多信息，请参阅第七卷第一章。

如果你输入其他某个匿名 FTP 服务器的主机名，访问匿名 FTP 站点的相同方法也适用。例如，尝试输入以下 URL：

```
ftp://ftp.netscape.com/
```

你将看到 ftp.netscape.com 服务器的目录。

## 使用命令行 FTP 客户端

了解如何从命令行使用 FTP 是个好主意——以防万一。例如，如果你的 GUI 桌面无法正常工作，你可能需要下载一些文件来修复问题。如果你知道如何使用命令行 FTP 客户端，你就可以下载文件并解决问题。这并不太难，而且所有 Linux 发行版都提供了命令行 FTP 客户端。

弄清楚命令行 FTP 客户端的最佳方法是动手尝试。该命令名为 ftp，你可以在 Linux 系统上运行 ftp 命令。你甚至不需要 Internet 连接，因为你可以使用 ftp 命令连接到自己的系统——我会向你展示如何操作。

请注意，ftp 命令的确切输出可能会有所不同，因为某些发行版（如 Debian）使用 gFTP 的文本模式版本作为命令行 FTP 客户端。

在下面的示例 FTP 会话中，我使用命令行 FTP 客户端以我的用户名（naba）登录，并浏览我的一个 Linux 系统上的目录。当你尝试类似的操作时，请用你的用户名替换该名称并提供你的密码。以下是展示与典型命令行 FTP 客户端交互的列表（我的评论以斜体显示，我输入的文字以粗体显示）：

```
ftp localhost
Connected to localhost.localdomain.
220 (vsFTPd 2.0.3)
Name (localhost:naba):       (我按 Enter。)
331 Please specify the password.
Password:                    (我输入我的密码。)
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> **help**              (我输入 help 以查看 FTP
命令列表。)
Commands may be abbreviated. Commands are:

!       debug         mdir        qc        send
$       dir           mgmt        sendport  site
account disconnect    mkdir       put       size
append  exit          mls         pwd       status
ascii   form          mode        quit      struct
bell    get           mtime       quote     system
binary  glob          mput        recv      sunixic
bye     hash          newer       recuper   tenex
case    help          nmap        restatus  tick
cd      idle          nlist       rhelg     trace
cdup    image         mtrans      rename    type
chmod   lcd           open        reset     user
close   ls            prompt      restart   umask
cr      macdef        passive     rmdir     verbose
delete  mdelete       proxy       runique   ?
ftp> **help mget**       (我可以在特定命令上获取帮助。)
mget          get multiple files
ftp> **cd /var**        (这将目录更改为 /var。)
250 Directory successfully changed.
ftp> **ls**          (此命令列出
目录的内容。)
227 Entering Passive Mode (127,0,0,1,38,142)
150 Here comes the directory listing.
... lines deleted...
226 Directory send OK.
ftp> **bye**           (此命令结束会话。)
221 Goodbye.
```

如上所示，通过输入命令 **ftp hostname** 即可启动命令行 FTP 客户端，其中 *hostname* 是你想要访问的系统的名称。当 FTP 客户端与远程系统的 FTP 服务器建立连接后，FTP 服务器会提示你输入用户名和密码。在你提供信息后，FTP 客户端会显示 `ftp>` 提示符，你可以开始输入命令以执行特定任务。如果你记不起某个特定的 FTP 命令，请输入 **help** 以查看命令列表。你可以通过输入 **help command** 来获取特定命令的额外帮助，其中 *command* 是你需要帮助的特定命令。

许多 FTP 命令与用于导航文件系统的 Linux 命令相似。例如，**cd** 更改目录，**pwd** 打印当前工作目录的名称，**ls** 列出当前目录的内容。另外两个常用命令是 **get** 和 **put**：**get** 用于从远程系统下载文件到你的系统，**put** 用于从你的系统上传（发送）文件到远程主机。

表 4-1 描述了一些常用的 FTP 命令。你不必输入完整的 FTP 命令。对于长命令，你只需输入前几个字符——足以唯一识别该命令即可。例如，要删除一个文件，你可以输入 **dele**；要将文件传输模式更改为二进制模式，你可以输入 **bin**。

![](img/792720823146d68f19fd50c99ebfce4b_393_0.png)

从 Internet 下载文件时，你几乎总是希望以二进制模式传输文件，因为软件通常以二进制形式归档和压缩。（它们不是纯文本文件。）因此，始终使用 **binary** 命令将模式设置为二进制。然后使用 **get** 命令下载文件。

![](img/792720823146d68f19fd50c99ebfce4b_393_1.png)

在传输多个名称相似的文件（例如 **image1.jpg**、**image2.jpg** 等）时，输入 **prompt** 以关闭提示。（否则，每次文件传输后，FTP 客户端都会询问你是否要传输下一个文件。）然后输入 **mget** 后跟带有通配符的文件名。例如，要下载所有以 **image** 开头且以 .jpg 扩展名结尾的文件，请输入 **mget image*.jpg**。

| 命令 | 描述 |
| :--- | :--- |
| ! | 在本地系统上执行 shell 命令。例如，<code>! ls</code> 列出本地系统当前目录的内容。 |
| ? | 显示命令列表（等同于 **help**） |
| append | 将本地文件追加到远程文件 |
| ascii | 将文件传输类型设置为 ASCII（或纯文本）。此命令是默认的文件传输类型。 |

