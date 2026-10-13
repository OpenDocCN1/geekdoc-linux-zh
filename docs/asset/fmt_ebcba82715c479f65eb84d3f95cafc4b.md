
| `help` | 显示命令列表。 |

| `image` | 与 `binary` 相同。 |

| `lcd` | 更改本地系统上的当前目录。例如，`lcd /var/ftp/pub` 将当前目录更改为 `/var/ftp/pub`。 |

| `ls` | 列出当前远程目录的内容。 |

| `mdelete` | 删除远程系统上的多个文件。例如，`mdelete *.jpg` 删除当前目录下所有以 `.jpg` 结尾的远程文件。 |

# 第 III 部分：Linux 互联网络

## 表 17-1（续表）

| 命令 | 描述 |
| --- | --- |
| `mdir` | 列出多个远程文件并将列表保存到指定的本地文件中。例如，`mdir /usr/share/doc/w* wlist` 将列表保存到名为 `wlist` 的本地文件中。 |
| `mget` | 下载多个文件。例如，`mget *.jpg` 下载所有以 .jpg 结尾的文件。如果开启了提示（`prompt`），FTP 客户端在下载每个文件之前会请求确认。 |
| `mkdir` | 在远程系统上创建目录。 |
| `mls` | 与 `mdir` 相同。 |
| `mput` | 上传多个文件。例如，`mput *.jpg` 将所有以 .jpg 结尾的文件发送到远程系统。 |
| `open` | 打开到 FTP 服务器的连接。例如，`open ftp.netscape.com` 连接到该服务器。 |
| `prompt` | 开启或关闭提示。当提示开启时，FTP 客户端会请求确认。 |
| `put` | 将文件发送到远程系统。例如，`put index.html` 将 `index.html` 发送到远程系统。 |
| `pwd` | 显示当前目录的完整路径。 |
| `quit` | 与 `bye` 相同。 |
| `recv` | 与 `get` 相同。 |
| `rename` | 重命名远程系统上的文件。例如，`rename old.html new.html` 将文件重命名为 `new.html`。 |
| `restart` | 通过指定的偏移重启文件传输。 |
| `rdir` | 删除远程系统上的目录。例如，`rdir` 删除当前目录下的 `images` 目录。 |
| `safe` | 将数据传输的保护级别设置为安全，以便使用加密校验和来保护数据完整性。 |
| `size` | 显示远程文件的大小。例如，`size bigfile.tar.gz` 显示文件的大小。 |
| `status` | 显示 FTP 客户端的当前状态。 |
| `user` | 向 FTP 服务器发送用户信息。例如，`user naba` 发送用户名 `naba`；随后服务器会提示密码。 |

# 使用图形化客户端

GNOME 自带 `gFTP`，这是一个图形化 FTP 客户端。要启动 `gFTP`，从 GNOME 桌面应用程序 Internet > `gFTP` 选择。这将启动 `gFTP` 程序并显示其窗口。

`gFTP` 窗口（见图 17-1）有一个用于执行各种任务的菜单栏。菜单栏下方是包含许多按钮和文本字段的工具栏。在这里你可以输入远程主机名称、用户名和登录所需的密码。提供主机用户信息后，点击 Host 字段左侧的计算机图标按钮。这将 `gFTP` 连接到该主机并使用你提供的用户名和密码登录。

图 17-1 显示了连接到远程站点并在远程目录间移动以准备下载文件后的 `gFTP` 窗口。

![](img/3b3329dddbc9c0857ad4f2ef1c0db305_541_0.png)

图 17-1：连接到远程 FTP 服务器后的 `gFTP` 窗口。

`gFTP` 窗口的中间分为两部分。左侧显示当前本地目录的内容；右侧显示远程目录的内容。一旦建立连接，传输文件非常简单。只需在列表中选择所需文件，点击左侧箭头按钮下载或点击右侧箭头按钮上传。

使用 `gFTP` 的最大好处是你可以通过选择右侧窗口中的目录并点击左箭头来下载整个目录。

要断开连接，再次点击计算机按钮。然后你可以通过从菜单中选择 Quit 来退出 `gFTP` 应用程序。

# 508 第三部分：Linux 网络互

`gFTP` 不仅用于 FTP 传输。它还可以使用 HTTP 协议传输文件，并使用安全 Shell (`SSH`) 协议进行安全文件传输。

## 使用 Web浏览器作为 FTP 客户端

任何 Web 浏览器都可以作为 FTP 客户端，但它们最适用于匿名 FTP 下载，在这种情况下，浏览器可以使用匿名用户名和密码登录。

在 Linux 中，你使用 Firefox 浏览器作为 FTP 客户端。只需提供告诉 Web 浏览器使用 FTP 下载文件的 URL 即可。FTP URL 的语法如下：

```
ftp://username:password@hostname/pathname
```

第一部分 (`ftp/`) 表示你正在进行 FTP 传输。`hostname` 部分是 FTP 服务器的名称（例如 `localhost`，或者 `ftp.beta.redhat.com`）。`pathname` 是你想要下载的文件的完整目录路径和文件名。`username:password` 是登录 FTP 服务器所需的用户名和密码。你可以留空这些部分以以匿名用户的身份登录。

> 当你在 URL 中提供用户名和密码时，由于该密码将以明文形式存在，任何查看该 URL 的人都可以读取。

如果 URL 仅包含 FTP 服务器的主机名，Web 浏览器将显示匿名 FTP 目录的内容。如果你想在你的 Linux 系统上尝试，请启动 Firefox（点击 GNOME 面板上的 浏览器图标），并在位置框中输入以下内容：

```
ftp://localhost
```

按下回车。Firefox 将显示你 Linux 系统上匿名 FTP 目录的内容。你可以点击文件夹查看其内容并下载任何文件。

当你使用 `ftp://localhost` 时，如果你没有运行 FTP 服务器，或者设置了防火墙不允许任何 FTP 连接，你将不会收到系统的响应。

如果你输入其他 FTP 服务器的主机名，访问匿名 FTP 站点的相同方法也同样有效。例如，输入以下 URL：

```
ftp://download.fedora.redhat.com
```

你理应可以获得 `download.fedora.redhat.com` 服务器的目录。

## 配置 FTP 服务器

Linux 自带由 Chris Evans 编写的极其安全的 FTP 守护 (`vsftpd`)。`vsftpd` 的可执行文件为 `/usr/sbin/vsftpd`，它使用了 `/etc` 和 `/etc/vsftpd` 目录下的多个配置文件。

# 第 17 章：FTP 服务器

`vsftpd` 服务器配置为独立运行，并有一个初始化脚本（或称为 initscript）——`etc/init.d/vsftpd` 用于启动和停止服务器。如本章前面的介绍，你可以使用命令启动服务器：

```
service vsftpd start
```

你可以以 root 身份使用以下命令，使 `vsftpd` 在系统启动时启动：

```
chkconfig --level 35 vsftpd on
```

在启动 `vsftpd` 服务器后，默认设置已足够开始使用该服务器。然而，你应该了解这些配置文件，以防你需要对它们进行自定义。

## 学习 vsftpd 配置文件

`vsftpd` 服务器消耗了位于 `/etc` 目录下的多个配置文件。这些目录控制着 FTP 服务器的许多方面，例如它是否独立模式运行、谁可以下载文件，以及是否允许匿名 FTP。

- `vsftpd` 的关键配置文件如下：

- `/etc/vsftpd/vsftpd.conf`：控制 `vsftpd` 服务器如何工作。（例如，它是否应该允许匿名登录、是否允许文件上传、是否以独立模式运行等？）

- `/etc/vsftpd/ftusers`：列出无法访问 FTP 服务器的用户名。

- `/etc/vsftpd/user_list`：列出被拒绝访问的用户名（甚至不会提示输入密码）。然而，如果 `/etc/vsftpd/vsftpd.conf` 中的 `userlist_deny` 选项设置为 `NO`，则这些用户被允许访问 FTP 服务器。

你通常可以让大多数配置文件保持默认设置。然而，以防你可能更改某些内容以使 `vsftpd` 满足你的需求，接下来的章节将简要解释这些配置文件。

## 理解 /etc/vsftpd/vsftpd.conf 文件

为了了解你可以在 `/etc/vsftpd/vsftpd.conf` 文件中设置什么，以及这些行如何影响 `vsftpd` 服务器的运行，请查看默认安装的 `/etc/vsftpd/vsftpd.conf` 文件。该文件中的注释告诉了每个选项的作用。

默认情况下，`vsftpd` 几乎不允许任何操作。通过这些选项，你可以放宽使用 FTP 的限制。设置应该放宽到什么程度取决于你。请注意，大多数选项被设置为 `YES`。这是因为大多数默认设置都是 `NO`。若要反转某个选项的意图，只需在该行开头放置一个 `#` 将该选项注释掉。

# 第三部分：Linux 网络互

你可以在 `/etc/vsftpd/vsftpd.conf` 中设置以下选项：
