
```
scp file username@yourserver:/home/username/
```

- 从你的（远程）服务器拷贝到另一个（远程）服务器，使用以下语法：

```
scp username@yourserver:/home/username/file .
```

- 从（远程）服务器拷贝到另一个（远程）服务器，使用以下语法：

```
scp username@yourserver:/home/username/file username2@yourserver2:/home/username2/
```

在上述命令中，`file` 是要传输到服务器 `yourserver` 上用户为 `username` 的目录 `/home/username/` 的文件，末尾的点 `.` 表示当前本地目录。

让我们来学习 `sftp`。

# sftp

Secure File Transfer Program (安全文件传输程序) 是传统 FTP 的替代方案。它在 SSH 上执行所有功能。`sftp` 的语法为：

```
sftp user@host:file file
```

在这里，`user` 是本地 PC，`host` 是远程 PC，`file` 是文件名。

在学习了安全服务之后，让我们学习安全性较低的服务。

# 第 3 章 安全性较低的服务

有一些不安全的的服务是不应该使用的，因为它们的所有流量都以明文形式在网络上传输。在接下来的章节中，让我们讨论其中一些安全性较低的服务：

- Telnet：它是一种允许你访问远程主机虚拟终端的协议。它是一个基于文本的控制台应用程序。
- FTP：它是运行在端口 20 和 21 上的标准协议。你可以输入 `help` 命令来列出 FTP 中可用命令。两个重要的命令是 `put` 和 `get`，分别提供将文件从你的机器移动到远程机器以及从远程服务器拉取到你机器的功能。如果有多个文件，请使用 `mput` 和 `mget`。
- rsync：这个文件传输程序类似于 RCP。它发送加密流量。服务器在端口 873 上监听。
- ssh：它是一种用于在远程主机上执行命令的加密协议。
- login：它是一个将你的终端连接到远程机器终端的登录程序。它是不安全的协议，并以明文发送所有信息。
- finger：它允许远程系统上的用户搜索另一个系统上的用户信息。它显示用户的登录名、真实姓名、空闲时间、位置和电话号码。`finger` 守护进程监听端口 79。
- talk and expect：它们是实时聊天协议，分别运行在端口 517 和 518 上。输入 `talk username` 向其他人发送请求。

让我们用一台 Linux 机器作为服务器。

# 作为服务器的 Linux 机器

以下是 Linux 上可用的相同安全协议：

- HTTP：Apache 是 Linux 上最常见的 Web 服务器，通过系统的 rc 脚本启动。你可以轻松地配置 Apache 及其位于 `/etc/httpd/conf/` 的配置文件。Apache 监听端口号 80，并可以监听许多不同的网络端口。
- sshd：安全守护进程 `sshd` 通过系统的 rc 脚本启动。它的全局系统配置文件存在 `/etc/sshd_config` 中，用户的配置文件放置在 `$HOME/`。它监听端口 22。
- ftp：FTP 守护进程使用端口 20 和 21 启动 FTP 请求。其配置文件 `ftppass`、`ftpversions`、`ftgroups` 和 `ftpdusers` 位于。
- DNS：域名服务 `DNS` 将主机名映射到 IP 地址。它使用端口 53。

# 配置 inetd

`inetd` 守护进程是一个超级服务器，它监听传入的连接并启动相应的服务。`inetd` 的配置文件通常位于 `/etc/inetd.conf`。

要在 `inetd` 中启用某项服务，你必须在配置文件找到该服务并取消行的注释。一旦配置完成，必须重启 `inetd` 服务才能更改生效。

# 微软网络与网络服务介绍 81

你可以使用以下命令连接到支持 `ssh` 的服务器：

```
ssh -p port username@yourserver
```

将 `port` 替换为默认端口 22，将 `username` 替换为你的主机或 IP 地址，并将 `yourserver` 替换为你想要连接的服务器的主机或 IP 地址。

如果服务器支持 SSH 连接，你可以访问默认端口 22。第一次使用 SSH 时，它会询问你是否确认要继续，并要求你提供密码。成功连接后，你可以发送和接收数据。

让我们来学习 `scp`。

# scp

Secure Copy (安全复制) 是 SSH 软件包的一部分。`scp` 命令允许你通过 `ssh` 连接复制文件。它是 RCP 和 FTP 的替代方案。`scp` 命令有三种用法方式：

- 从（远程）服务器拷贝文件到你的计算机，请使用以下语法：

```
scp file username@yourserver:/home/username/
```

- 从你的（远程）服务器拷贝到另一个（远程）服务器，使用以下语法：

```
scp username@yourserver:/home/username/file .
```

- 从（远程）服务器拷贝到另一个（远程）服务器，使用以下语法：

```
scp username@yourserver:/home/username/file username2@yourserver2:/home/username2/
```

在上述命令中，`file` 是要传输到服务器 `yourserver` 上用户为 `username` 的目录 `/home/username/` 的文件，末尾的点 `.` 表示当前本地目录。

让我们来学习 `sftp`。

# sftp

Secure File Transfer Program (安全文件传输程序) 是传统 FTP 的替代方案。它在 SSH 上执行所有功能。`sftp` 的语法为：

```
sftp user@host:file file
```

在这里，`user` 是本地 PC，`host` 是远程 PC，`file` 是文件名。

在学习了安全服务之后，让我们学习安全性较低的服务。

# 第 3 章 安全性较低的服务

有一些不安全的的服务是不应该使用的，因为它们的所有流量都以明文形式在网络上传输。在接下来的章节中，让我们讨论其中一些安全性较低的服务：

- Telnet：它是一种允许你访问远程主机虚拟终端的协议。它是一个基于文本的控制台应用程序。
- FTP：它是运行在端口 20 和 21 上的标准协议。你可以输入 `help` 命令来列出 FTP 中可用命令。两个重要的命令是 `put` 和 `get`，分别提供将文件从你的机器移动到远程机器以及从远程服务器拉取到你机器的功能。如果有多个文件，请使用 `mput` 和 `mget`。
- rsync：这个文件传输程序类似于 RCP。它发送加密流量。服务器在端口 873 上监听。
- ssh：它是一种用于在远程主机上执行命令的加密协议。
- login：它是一个将你的终端连接到远程机器终端的登录程序。它是不安全的协议，并以明文发送所有信息。
- finger：它允许远程系统上的用户搜索另一个系统上的用户信息。它显示用户的登录名、真实姓名、空闲时间、位置和电话号码。`finger` 守护进程监听端口 79。
- talk and expect：它们是实时聊天协议，分别运行在端口 517 和 518 上。输入 `talk username` 向其他人发送请求。

让我们用一台 Linux 机器作为服务器。

# 作为服务器的 Linux 机器

以下是 Linux 上可用的相同安全协议：

- HTTP：Apache 是 Linux 上最常见的 Web 服务器，通过系统的 rc 脚本启动。你可以轻松地配置 Apache 及其位于 `/etc/httpd/conf/` 的配置文件。Apache 监听端口号 80，并可以监听许多不同的网络端口。
- sshd：安全守护进程 `sshd` 通过系统的 rc 脚本启动。它的全局系统配置文件存在 `/etc/sshd_config` 中，用户的配置文件放置在 `$HOME/`。它监听端口 22。
- ftp：FTP 守护进程使用端口 20 和 21 启动 FTP 请求。其配置文件 `ftppass`、`ftpversions`、`ftgroups` 和 `ftpdusers` 位于。
- DNS：域名服务 `DNS` 将主机名映射到 IP 地址。它使用端口 53。

# 配置 inetd

`inetd` 守护进程是一个超级服务器，它监听传入的连接并启动相应的服务。`inetd` 的配置文件通常位于 `/etc/inetd.conf`。

要在 `inetd` 中启用某项服务，你必须在配置文件找到该服务并取消行的注释。一旦配置完成，必须重启 `inetd` 服务才能更改生效。

# 微软网络与网络服务介绍 81

你可以使用以下命令连接到支持 `ssh` 的服务器：

```
ssh -p port username@yourserver
```
