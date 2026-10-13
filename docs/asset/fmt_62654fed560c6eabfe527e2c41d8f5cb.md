
进入`/etc/vsftpd.ftusers`列不允许登录 FTP 服务器的用户。这些用户通常是服务器上具有较高权限的用户；允许这些用户登录会对你的系统带来安全漏洞。你可以通过任何文本编辑器编辑此文件来向列表中添加名称。

列表 14-2: `/etc/vsftpd.ftusers` 文件

```
[root@main ~]# cat /etc/vsftpd.ftusers
# 不允许通过 ftp 登录的用户
bin
daemon
adm
lp
sync
shutdown
halt
mail
news
uucp
operator
games
nobody
```

# 第四部分：配置您的企业级 Linux 网络服务

## 配置 `/etc/vsftpd.user_list` 文件

根据您在`/etc/vsftpd/vsftpd.conf`文件设置的指令，`/etc/vsftpd.user_list`文件中的列表可用于阻止或允许列表中列出的用户访问。列表 14-3 显示了文件内容。请注意文件开头注释行中的指令。列表中的第一行是在命令行提示符处输入的命令，列表的其余部分是该命令的输出。

列表 14-3：`/etc/vsftpd.user_list` 文件

```
[root@root]# cat /etc/vsftpd.user_list
# vsftpdlist
# 如果 userlist_deny=NO，则只允许文件中的用户访问
# 如果 userlist_deny=YES (默认)，则永远不允许文件中的用户访问，
# 甚至不会提示输入密码。
# 注意，默认的 vsftpd pam 配置也会检查 /etc/vsftpd.ftpusers
root
bin
daemon
adm
l
sync
halt
mail
news
uuccp
operator
games
nbody
```

## 启动 FTP 服务器

在按照您的喜好配置 FTP 服务器后，您需要启动它。通过输入以下命令启动服务器：

```
[root@root]# service vsftpd start
Starting vsftpd for vsftpd:	[ OK ]
```

此命令启动当前会话的 FTP 服务器，但没有设置服务器在系统启动时自动启动。要确保 FTP 服务器在系统启动时启动，请输入以下命令：

```
chkconfig -level 35 vsftpd on
```

此命令告诉系统在处于运行级别（runlevel）3 或 5 时，始终启动`vsftpd`服务器。

# 第 14 章：配置和管理 FTP 服务器

## 测试 FTP 服务器

始终测试您的工作，以确保您正确配置了服务器。您可以通过尝试登录在本地测试服务器。列表 14-4 显示了整个登录过程。列表中的第一行是在命令行提示符处输入的命令，列表的其余部分是该命令的输出。

列表 14-4：登录过程

```
[root@main ~] ftp localhost
Connected to localhost.localdomain.
220 Welcome to the TAC Technology server!
220 Anonymous logins are allowed by using
220 ftp or anonymous as the username and
220 a valid email address as the password.
220 Please be advised that all activity on this site is logged.
220 We hope you enjoy your visit with us!
530 Please login with USER and PASS.
530 Please login with USER and PASS.
KERBEROS_V4 rejected as an authentication type
Name(localhost): terry
Please specify the password.
Password:
Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp>
```

如果您能成功在本地登录服务器，说明您的配置是正确的。为了完成测试，您应该以普通用户身份远程登录——如果您配置了匿名登录，则以匿名用户身份登录。

## 登录 FTP 服务器

可以使用图形化客户端或命令行客户端登录 FTP 服务器。在本节中，我将向您展示如何使用图形化客户端和命令行客户端。

### 使用 gFTP 访问 FTP

企业 Linux 包含一个图形化 FTP 程序 —— `gFTP`，可以从 GNOME 或 KDE 桌面访问。可以通过选择“应用程序 > 更多 > gFTP 窗口”来启动 `gFTP`，如图 14-2 所示。通过 `gFTP` 登录 FTP 服务器，请按照以下步骤操作：

1. 在 Host（主机）字段中，填写您想要连接的的主机名或 IP 地址。
2. 在 Port（端口）字段中，输入远程服务器的端口号。端口 21 是 `ftp` 通常使用的端口。
3. 在 User（用户）字段中，输入用户的用户名。
4. 在 Pass（密码）字段中，输入用户的相应密码。如果您连接的是之前连接过的主机，可以点击 Host、User 和 Pass 字段旁边的箭头，并从相应的下拉列表中选择。（img/64d26e5c3406fc66f2dd833f0d7cc3af_247_0.png） 14-2：`gFTP` 程序是一个图形化客户端：(img/64d26e5c3406fc66f2dd833f0d7cc3af_247_1.png)
5. 点击 Host 字段左侧的 Host 按钮。（按钮上有两台电脑。）`gFTP` 连接到远程服务器并登录您输入的用户。
6. 登录后，您将看到一个类似于图 14-3 所示的窗口。窗口左侧是本地系统的目录列表。窗口右侧是远程系统的目录列表。两个目录列表之间的箭头可用于在系统之间传输文件。
   - 要从本地系统传输文件到远程系统，请从本地目录列表中选择您想要传输的文件并点击向右的箭头。
   - 要从远程系统传输文件到本地系统，从远程目录列表中选择您想要传输的文件，然后点击向左的箭头。

### 使用命令行客户端访问 FTP 服务器

您可以使用命令行客户端登录 FTP 服务器。在本节中，我将向您展示如何使用命令行客户端。

# 第 15 章

## 提供网页服务

本章内容

- 安装和启动 Web 服务器
- 配置和管理你的 Web 服务器

每当你访问 Internet 上的网站时，你都会看到该网站提供的内容。而你没有看到的是让查看网站成为可能的幕后活动。这些幕后活动都由一个 Web 服务器控制，而 Apache Web 服务器是目前美国使用最广泛的 Web 服务器。正如你通过阅读本章所看到的，它的设置和维护相对容易。如果你正在安装 Enterprise Linux 的 AS 或 ES 版本，你可以在本章中找到关于 Apache 服务器所需的全部知识。如果你运行的是 Enterprise Linux 的 WS 或桌面版本，你将不会运行 Web 服务器——因此你可以跳过本章。

设置和运行 Web 服务器可能是一项非常复杂的任务；事实上，有许多书籍专门讨论这个主题。然而，本章将使你能够设置一个基础的 Web 服务器。你可以参考 `www.apache.org` 上的 Apache 网站获取更详细的文档。

## 安装和启动 Web 服务器

Apache Web 服务器软件通常在系统安装期间自动安装，因此你不必手动安装它。不过，我建议在尝试启动它之前检查它是否存在。你可以通过输入以下命令来检查 Web 服务器：

```
rpm -q httpd
```

如果已安装 Apache 软件，系统会响应已安装软件的名称和版本号。如果没有安装 Web 服务器，你的查询将导致系统响应服务器未安装。

你可以按照以下步骤安装 Web 服务器：

1. 选择“应用程序”：“系统设置”::“添加/删除应用程序”。

如果你没有以 `root` 用户身份登录，系统会提示你输入 `root` 密码。

会弹出“软件包管理”对话框，如图 15-1 所示。

图 15-1：使用软件包管理对话框向你的系统添加包。

2. 滚动到“部分”部分并勾选“Web 服务器”复选框。
