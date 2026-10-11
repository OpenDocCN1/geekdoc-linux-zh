
![](img/71f80d7808bf5b5ad1239cc29be7bab_251_0.png)

图 3-1：刚建立与 FTP 服务器连接的 `gFTP` 窗口。

```
PWO 257 / is current directory.
listing from server (LC_TIME=en_UTF-8)
PASV 222 Entering Passive Mode.
220 Opening ASCII connection for -
226 Transfer complete
```

### 使用图形化 FTP 客户端

`gFTP` 窗口有一个菜单栏，其中有执行各种任务的菜单。菜单栏下方是一个带有许多按钮和文本字段的工具栏。在这里你可以输入远程主机的名称或 IP 地址，以及登录远程主机所需的用户名和密码。图 3-1 显示了在你填写这些信息并点击显示有两台电脑图标的按钮（工具栏最左侧的一个）与远程主机建立连接后的 `gFTP` 窗口。

使用 `gFTP` 上传文件，请遵循以下步骤：

1. 在 `Host`（主机）字段中填写远程系统的主机名或 IP 地址。如果你以前用过，可以在点击 `Host` 字段旁边的向下箭头时从下拉列表中选择它。
2. 在 `User`（用户）字段中提供用户名，在 `Pass`（密码）字段中提供密码，然后点击显示两台电脑图标的按钮（工具栏最左侧的）与远程主机建立连接。
3. `gFTP` 窗口显示远程源的目录。你可以通过拖拽文件到远程目录来上传文件。
4. `gFTP` 窗口显示本地目录。你可以通过将文件从远程目录拖到本地目录来下载文件。
5. 点击右侧的向下箭头。
6. 完成传输后，从 `gFTP` 退出。

这种类型的*匿名 FTP* 非常适合向任何想要文件的人分发文件。例如，硬件供应商可能会使用匿名 FTP 为任何需要的人提供更新的设备。这种 FTP 客户端不仅如此，还可以使用 SSH（安全 Shell）协议传输文件。

img/71f80d7808bf5b5ad1239cc29be7bab_252_0.png)

## 234 使用图形化 FTP 客户端

### 介绍 FileZilla

`FileZilla` 是另一个适用于 Windows 和 Linux 的图形客户端。它看起来与 `gFTP` 非常相似（如图 3-2 所示）。img/71f80d7808bf5b5ad1239cc29be7bab_253_0.png)

图 3-2：`FileZilla` 显示本地目录。

你可以在 `https://filezilla-project.org` 找到 `FileZilla`。

img/71f80d7808bf5b5ad1239cc29be7bab_254_0.png)

图 3-3：`FileZilla` 显示远程 FTP 服务器的目录。

当 `FileZilla` 窗口出现时，它显示你的主目录，就像 Windows 资源管理器一样。要连接到远程主机，在 `Host` 字段中输入主机名或 IP 地址，以及登录远程主机所需的用户名和密码。图 3-3 显示了在你填写这些信息并与远程主机建立连接后的 `FileZilla` 窗口。你现在可以使用 `FileZilla` 上传文件，只需将文件从一个系统拖到另一个系统。你也可以通过将文件从远程目录拖到本地目录来下载文件。

完成后，选择 `FileZilla` 退出。

### 使用网络浏览器作为 FTP 客户端

任何网络浏览器都可以作为 FTP 客户端，但此类程序最适用于匿名下载，此时网络浏览器可以使用匿名用户名和任何密码登录。img/71f80d7808bf5b5ad1239cc29be7bab_255_0.png)

图 3-4：Firefox 中 FTP 目录的典型外观。

例如，你可以使用 Firefox 浏览器作为 FTP 客户端。你还需要知道如何编写 URL，以便网络浏览器知道你想使用 FTP 下载文件。FTP URL 的语法为：

```
ftp://hostname/pathname
```

第一部分 (`ftp/`) 表示你想进行 FTP 传输。主机名是 FTP 服务器的一部分（`ftp` 之后的名称），例如 `ftp.wiley.com`。路径是你想要下载的文件完整路径和文件名。

如果你只提供 FTP 服务器的主机名，网络浏览器将显示匿名 FTP 目录的内容。如果你想在 Linux 系统上访问匿名 FTP，启动 Firefox（点击 GNOME 面板上的网络图标），在位置（Location）文本框中输入 FTP URL 并按回车。

## 236 使用命令行 FTP 客户端

访问 `ftp://localhost/pub/` 以进入 `pub` 目录。（如果你没有运行 FTP 服务器，或者设置了防火墙以允许 FTP 连接，你的系统将不会给你任何响应。）

![](img/71f80d7808bf5b5ad1239cc29be7bab2_255_0.png)

图 3-4：你可以使用网络浏览器从服务器下载文件。

在 Debian 和 Fedora 中，以 root 身份登录并在终端窗口中输入 `/etc/init/vsftpd start` 来启动 FTP 服务器。在 SUSE 中，由 `xinetd` 服务器控制 FTP 服务器 `vsftpd`。`/etc/xinetd.d/vsftpd` 配置文件指定了 `vsftpd` 如何启动。（有关 `xinetd` 配置文件的更多信息，请参阅第七卷第 1 章）。

![](img/71f80d7808bf5b5ad1239cc29be7bab2_255_1.png)

如果你输入其他匿名 FTP 服务器的主机名，同样可以使用访问匿名 FTP站点的方法。例如，尝试以下 URL：

`ftp://ftp.netscape.com/`

你将获得 `ftp.netscape.com` 服务器的目录。

## 使用命令行 FTP 客户端

从命令行使用 FTP 是一个很好的主意。例如，如果你的 GUI 桌面没有运行，你可能需要下载一些文件来解决问题；如果你知道如何使用命令行 FTP 客户端，就可以做到。命令行 FTP 客户端在所有 Linux 发行版中均可用，使用它并不困难。

![](img/71f80d7808bf5b5ad1239cc29be7bab2_255_2.png)

www.it-ebooks.info

## 237 使用命令行 FTP 客户端

了解命令行 FTP 客户端最好的方法就是尝试使用它。命令是 `ftp`，你可以从你的 Linux 系统尝试 `ftp` 命令。你甚至不需要连接互联网，因为你可以使用 `ftp` 命令连接到自己的系统。

请注意，`ftp` 命令的输出可能不同，因为某些发行版（如 Debian）使用 `gFTP` 的文本模式作为命令行客户端。

在下面的示例 FTP 会话中，使用了命令行 FTP 客户端登录并浏览 Linux 系统上的目录。这里是使用典型命令行 FTP 客户端的的列表：
