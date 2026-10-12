
# 第 22 章
# 使用 FTP 提供远程文件服务

文件传输协议（FTP）曾被视为通过网络在计算机之间传输文件的主要方法。尽管现在许多图形化 FTP 客户端都补充了原始的基于文本的界面命令，但 FTP 今天仍被广泛使用。随着计算机的发展，FTP 也随之演进，Fedora Core 提供了许多使用图形界面通过 FTP 传输文件的方式。

本章概述了 Fedora 包含的可用 FTP 软件，并简要介绍了初始设置、配置以及使用特定于 FTP 的客户端的细节。Fedora 还包含一个名为 vsftpd（非常安全的 FTP 守护进程）的 FTP 服务器软件包，以及一系列你可以用来提供和传输文件的 FTP 协议相关程序。

以下各节概述了如何使用 FTP 客户端，以及 how to install and configure the vsftpd FTP server（如何安装和配置 vsftpd FTP 服务器）。

## 本章内容

- 使用 FTP 客户端
- FTP 服务器
- 安装 FTP 软件
- FTP 用户
- wu-ftpd 的 xinetd 配置
- 配置非常安全的 FTP 服务器
- 配置 Wu-FTPd 服务器
- 使用 ftpaccess 文件中的命令配置 wu-ftpd
- 配置 FTP 服务器文件转换操作
- 使用 ftphosts 文件中的命令允许或拒绝 FTP 服务器连接
- 服务器管理
- 参考资料

## 使用 FTP 客户端

基本的 FTP 协议允许用户连接到服务器，读取目录和文件名，以及下载和上传数据。如果设置了正确的访问权限，用户还可以创建新文件夹并为其设置访问权限。

然而，使用 FTP 会带来安全风险：用户名和密码未经加密就在局域网或互联网上传输。为了防止用户承担将身份验证详细信息暴露给窃听者的风险，许多站点仅启用匿名 FTP 登录和文件检索。许多 Linux 用户已转向更安全的替代方案，例如 OpenSSH 套件中提供的 sshd 和 sftp 或 scp。以下各节讨论了不同种类的较新和传统 FTP 接口及其使用情况。由于它们是更大的 OpenSSH 集合的一部分，sftp 和 scp 命令将在第 25 章“使用 SSH 和 Telnet 进行远程访问”中介绍。

### FTP 客户端界面

Fedora 提供了支持图形化或基于文本的 FTP 界面的 FTP 客户端。无论选择哪种类型，如果学习如何在命令行下使用 FTP 客户端，都能提升你对 FTP 的理解和使用。

使用基于文本的界面有助于理解图形化 FTP 会话中每个操作的作用。这种理解在某些情况下非常有用，例如，当图形客户端未自动检测正在传输的文件类型时。在这种情况下，二进制文件会被作为 ASCII 文件传输，因此变得无法使用。反之，作为二进制传输的 ASCII 文件会在每行末尾打印 `^M` 控制字符。这种错误通常发生在从旧版 Microsoft Windows 操作系统向 Linux 传输文件时，因为 Windows FTP 客户端默认使用 ASCII 而非二进制传输。

以下各节描述了如何使用基于文本的 FTP 客户端界面。在此说明之后，你将学习如何使用 Fedora 可用的众多图形化 FTP 客户端。

### 使用基于文本的 FTP 客户端界面

典型的 FTP 会话中可能会使用以下部分常用命令：

- **ascii**——为 FTP 会话设置 ASCII 文件传输类型。在发送或接收文本文件进行文件传输之前使用此命令。
- **bin**——为 FTP 会话设置二进制文件类型传输。在发送或接收二进制文件（如图形图像或压缩归档文件）进行文件传输之前使用此命令。
- **bye**——使用此命令关闭 FTP 连接并退出 ftp 命令。
- **close**——在 FTP 会话期间关闭与远程服务器的连接。使用此命令代替 quit 或 bye 返回到 ftp 命令提示符。
- **get**——启动从 FTP 服务器到用户本地计算机的单文件传输。使用此命令获取单个文件（例如 `get cartoon.jpg`）。
- **hash**——设置文件传输期间使用井号（#）。使用此命令以视觉方式指示传输进度。
- **mget**——启动从 FTP 服务器到用户本地计算机的多文件传输。使用此命令通过单个命令下载（接收）多个文件（例如 `mget *.jpg`）。
- **mput**——启动从用户本地计算机到 FTP 服务器的多文件传输。使用此命令通过单个命令上传（发送）多个文件（例如 `mput *.jpg`）。
- **open**——使用 IP 地址或主机名打开与远程服务器的连接。在 ftp 命令提示符下工作时使用此命令（例如 open ftp.redhat.com）。
- **prompt**——是一个交互式命令，当发出 mput 或 mget 命令时，询问用户是否要获取特定文件。如果用户发起 `mget *` 且提示开启，FTP 客户端将提示用户传输 `*` 通配符匹配的每个文件。当目录中有几个文件需要传输，而其中有一两个文件不需要时，这特别有用。默认情况下，提示功能是开启的。
- **put**——启动从用户本地计算机到 FTP 服务器的单文件传输。使用此命令上传（发送）单个文件（例如 put inventory.doc）。
- **send**——与 put 命令相同。
- **quit**——与 bye 命令相同。

> 虽然本章的这一节讨论了标准 ftp 客户端的使用，但 Linux 还有其他基于文本的 FTP 客户端。Nc-FTP 包含在 Fedora Core CD-ROM 中，或可从 www.ncftp.com 获取，它为用户提供额外的功能，例如一次获取多个目录的能力（无需执行递归 mget）以及在本地机器上重构目录结构。该产品的网站列出了此客户端提供给用户的所有功能——除了示例中描述的标准操作集之外。

这些只是 FTP 会话中可用命令的一部分。通过键入 **help**，用户可以查看有效命令的完整列表。键入 help command-name 会显示该命令作用的简要描述。列表 22.1 显示了 **help** 的输出。

### 列表 22.1 FTP 会话中 help 列出的命令

命令可以缩写。命令如下：

| | | | | |
| :--- | :--- | :--- | :--- | :--- |
| l | cr | mdir | proxy | send |
| $ | delete | mget | sendport | site |
| account | debug | mkdir | put | size |
| append | dir | mls | pwd | status |
| ascii | disconnect | mode | quit | struct |
| bell | form | mtime | quote | system |
| binary | get | mput | recv | sunique |
| bye | glob | newer | reget | tenex |
| case | hash | nmap | rstatus | trace |
| ccc | help | nlist | rhelp | type |
| cd | idle | ntrans | rename | user |
| cdup | image | open | reset | umask |
| chmod | lcd | passive | restart | verbose |
| clear | ls | private | rmdir | ? |
| close | macdef | prompt | runique | |
| cprotect | mdelete | protect | safe | |

### 使用 ftp 命令的典型 FTP 会话

连接到远程 FTP 服务器可能需要用户名和密码，但许多服务器也提供匿名访问。配置正确的远程 FTP 服务器会迅速响应 FTP 请求，并显示共享目录和文件。本节展示了一个在 Internet 许多站点中常见的典型服务器（在此情况下运行 wu-ftpd 服务器）的示例 FTP 会话。

你通过使用 **ftp** 命令加上远程计算机的 IP 地址或主机名来连接到远程 FTP 服务器，如下所示：

```
$ **ftp pheniox**

Connected to pheniox.

220 pheniox FTP server (Version wu-2.6.1-18) ready.

Name (pheniox:tdc): **anonymous**

331 Guest login ok, send your complete e-mail address as password.

Password:

230 Guest login ok, access restrictions apply.

Remote system type is Unix.

Using binary mode to transfer files.

ftp>
```

在此示例中，*ftp* 用于连接，然后使用匿名访问登录。这是在 Name 提示符下输入单词 **anonymous** 来实现的。按下回车键后，会显示密码提示符。使用匿名访问时，输入你的电子邮件地址被视为一种“礼貌形式”。输入的地址没有验证，但许多 FTP 服务器配置为仅接受有效的电子邮件地址格式（即，*user@somewhere.com*），如果在提示符下输入了任何文本。

> 许多 FTP 服务器在匿名访问时，如果在密码提示符下简单按下回车键，将接受该操作。

现在连接已建立并经过服务器认证，你可以设置 FTP 会话以按你的意愿运行。如前一节所述，*ftp* 命令有许多不同的内置命令，你可以在 *ftp>* 提示符下键入问号来查看这些命令。这些命令可以影响会话显示，设置文件传输类型，或获取有关远程服务器的信息。

