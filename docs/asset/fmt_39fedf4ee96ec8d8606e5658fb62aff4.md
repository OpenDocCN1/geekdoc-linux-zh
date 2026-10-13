
```
cd /mnt/cdrom/RPMS
rm -ivh gftp*
```

要启动 gFTP，从 GNOME 或 KDE 桌面菜单选择 Internet->gFTP。gFTP 窗口将会出现（如图 4-1 所示）。

> 图 4-1：在打开与远程 FTP 服务器连接之前的 gFTP 窗口。

![](img/d9230b719dc0efd80851f363d8c6f571_410_0.png)

# 使用图形化 FTP 客户端

gFTPC 有一个菜单栏，带有执行各种任务的菜单。菜单栏下方是一个带有许多按钮和文本字段的工具栏。在这里你可以输入远程主机的名称或 IP 地址、用户名以及登录远程主机所需的密码。图 4-1 显示了填入这些信息后的 gFTPC 窗口。

使用 gFTPC 上传或下载文件，请遵循以下步骤：

- 1. 在 `Host` 字段中填写远程系统的主机名或 IP 地址。

如果你以前用过该主机，可以在点击 `Host` 字段旁边的向下箭头时出现的下拉列表中选择。

- 2. 在 `User` 字段提供用户名，在 `Pass` 字段中提供密码，然后点击显示两台电脑图标的按钮（位于 `Host` 字段左侧）。

此操作会导致 gFTPC 连接到你的主机并使用你提供的用户名和密码登录。gFTPC 窗口的下部分显示两个系统之间交换的 FTP 协议消息。

- 3. 注意任何错误信息的指示。

远程系统的目录列表出现在 gFTPC 窗口的右半。左半显示当前的本地目录。

- 4. 要从当前系统向远程系统上传一个或多个文件，在左侧选择文件，然后点击右箭头按钮。

- 5. 从远程系统下载文件，选择列表上的文件名，然后点击左箭头按钮。

- 6. 当你完成文件传输时，从菜单选择 `FTPC: Quit`。

通过这些步骤，使用 GUI FTP 客户端（如 gFTPC）传输文件是一项简单任务。

信不信由，gFTPC 并不用于 FTP 传输。它还可以使用 HTTP 协议传输文件，并使用 Secure Shell (`SSH`) 协议进行安全文件传输。

![](img/d9230b719dc0efd80851f363d8c6f571_411_0.png)

## 使用 Web 浏览器作为 FTP 客户端

任何 Web 浏览器都可以作为 FTP 客户端，但此类程序最适用于匿名 FTP 下载，此时 Web 浏览器可以使用匿名用户名和任何密码登录。

### 使用图形化 FTP 客户端

在 Fedora Core 中，你可以使用 Mozilla Web 浏览器作为 FTP 客户端。你只需要知道如何编写 URL，以便 Web 浏览器能识别出你想使用 FTP 下载文件。FTP URL 的语法如下：

```
ftp://hostname/pathname
```

第一部分 (`ftp://`) 表示你想要进行 FTP 传输。`hostname` 是 FTP 服务器的一部分（名称通常以 ftp 开头——例如，`ftp.netscape.com`）。`pathname` 是你想要下载的完整目录路径和文件名。

如果你提供了 FTP 服务器的主机名，Mozilla 浏览器会显示匿名 FTP 目录的内容。如果你想在你的 Fedora Core 系统上寻找匿名 FTP，请启动 Mozilla（点击 GNOME 面板上的 Mozilla 图标），然后在 `Location` 框中输入以下行：

```
ftp://localhost
```

然后按回车。Mozilla 会显示你 Fedora Core 系统上匿名 FTP 目录的内容。图 4-2 显示了 Mozilla 中匿名 FTP 目录的典型外观。你可以点击文件夹查看其内容并下载任何文件。

| 匿名/ 索引 |
| --- |
| 文件 编辑 查看 签签 收藏 窗口 帮助 |
| 上一个 后一个 刷新 ftp://localhost/ 搜索 打印 |
| 首页 签签 Read Me 在网络 支持 商店 产品 培训 |
| ftp://localhost/ 索引 |
| 向上到级目录 |
| 01/12/2004 06:00:00 |

图 4-2:
你可以使用 Mozilla 从匿名 FTP 服务器下载文件。

![](img/d9230b719dc0efd80851f363d8c6f571_412_0.png)

当你使用 `ftp://localhost` URL 时，如果你没有运行 FTP 服务器，或者设置了防火墙不允许任何 FTP 连接，你将得不到系统的响应。在你的系统上，以 root 身份登录，并在终端窗口中输入 `vsftpd start` 来启动 FTP 服务器。

## 使用命令行 FTP 客户端

如果你输入其他匿名 FTP 服务器的主机名，访问匿名 FTP 站点的方法同样适用。例如，输入以下 URL：

```
ftp://ftp.netscape.com
```

你将获得 `ftp.netscape.com` 服务器的目录。

### 使用命令行 FTP 客户端

了解如何从命令行使用 FTP 是一个好主意——以防万一。例如，你的 GUI 桌面可能无法工作，为了解决问题，你可能需要下载文件。如果你知道如何使用命令行 FTP 客户端，你就可以下载文件并处理问题。这并不难。

学习命令行 FTP 客户端最好的方法是尝试。该命令名为 `ftp`，你可以从 Fedora Core 系统中尝试 `ftp` 命令。你甚至不需要任何互联网连接，可以使用 `ftp` 连接到你的主机——我为你演示。

在示例 FTP 会话中，使用命令行 FTP 客户端使用用户名 (`n`) 登录并浏览系统目录。这里显示了命令（命令为斜体）：

```
ftp localhost
Connected to localhost (127.0.0.1).
Name (localhost):n (我按回车)。
331 指定密码。
Password:(我输入密码)。
230 登录成功。
远程系统类型为 UNIX。
使用二进制模式传输文件。
ftp help (我输入 help 查看 FTP 命令列表)。
命令可以缩写。命令如下：
```
debug mdir sendport
$ dir mget put
disconnect mkdir struct
append exit quit struct
ascii form quote system
modtime recv unique
```
```

```
binary mput
ascii mget
type get
cd /var/ftp (这切换到 /var/ftp)。
ls
目录列表
250 目录切换成功。
mget filename (我获取特定文件)。
222 进入被动模式
150 这里是目录列表。
226 目录发送完毕。
bye (此命令结束会话)。
221 再见。
```

表 4-1 描述了一些常用的 FTP 命令。你不需要输入整个 FTP 命令。对于长命令，你必须输入前几个字符——足以唯一标识该命令。例如，要删除文件，你可以使用 `delete`，要将文件传输改为二进制，你可以输入 `bin`。

从互联网下载文件时，你总是希望以二进制模式传输文件，因为软件通常以二进制形式归档和压缩（文件不是纯文本文件）。因此，始终使用 `binary` 命令将模式设置为二进制。然后使用 `get` 命令下载文件。

### 使用命令行客户端

| 表 4-1 常用 FTP 命令 |
| 命令 | 描述 |
| :--- | :--- |
| `!` | 在本地系统上执行 shell 命令。例如，`!ls` 列出远程系统当前目录的内容。 |
| `?` | 显示命令列表（同于 help）。 |
| `append` | 将本地文件追加到远程文件。 |
| `ascii` | 将文件类型设置为 ASCII（或纯文本）。此命令是默认的文件传输类型。 |
| `binary` | 将文件类型设置为二进制。 |
| `bye` | 结束与远程服务器的 FTP 会话并返回 FTP 客户端。 |
| `cd` | 更改远程系统的目录。例如，`cd /pub/Linux` 将目录更改为 `/pub/Linux`。 |
| `chmod` | 更改远程文件的权限设置。例如，`chmod 664 index.html` 更改远程系统 `index.html` 文件的权限设置。 |
| `close` | 结束与 FTP 服务器的 FTP 会话并返回提示符。 |
| `delete` | 删除远程文件。例如，`delete bigimage.jpg` 删除远程系统上的该文件。 |
| `dir` | 列出远程系统当前目录的内容。 |
| `disconnect` | 结束 FTP 会话并返回 FTP 客户端的提示符。（这与 `close` 相同）。 |
| `get` | 下载文件。例如，`get junk.tar.gz junk.tgz` 从远程系统下载 `junk.tar.gz` 文件并保存为本地系统上的 `junk.tgz` 文件。 |
| `hash` | 开启或关闭显示文件传输进度的哈希标记 (#)。当开启此功能时，每从远程系统传输 1024 字节，屏幕上就会打印一个哈希。（它是进度条的命令行版本。） |
| `help` | 显示命令列表。 |
| `image` | 同 `binary`。 |
