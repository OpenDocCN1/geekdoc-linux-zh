
``` 
[me@linuxbox ~]$ ftp fileserver
Connected to fileserver.localdomain.
220 (vsFTPd 2.0.1)
Name (fileserver.me): anonymous
331 Please specify the password.
Password:
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> cd pub/cd_images/Ubuntu-8.04
250 Directory successfully changed.
ftp> ls
200 PORT command successful. Consider using PASV.
150 Here comes the directory listing.
-rw-rw-r-- 1 500 500 733079552 Apr 25 03:53 ubuntu-8.04-desktop-i386.iso
226 Directory send OK.
ftp> lcd Desktop
Local directory now /home/me/Desktop
ftp> get ubuntu-8.04-desktop-i386.iso
local: ubuntu-8.04-desktop-i386.iso remote: ubuntu-8.04-desktop-i386.iso
200 PORT command successful. Consider using PASV.
150 Opening BINARY mode data connection for ubuntu-8.04-desktop-i386.iso (733079552 bytes).
226 File send OK.
733079552 bytes received in 68.56 secs (10441.5 kB/s)
``` 

``` 
ftp> bye
``` 

以下是本次会话中输入的命令的解释：

| Command | Meaning |
|---|---|
| `ftp fileserver` | 调用 `ftp` 程序并使其连接到 FTP 服务器 `fileserver`。 |
| `anonymous` | 登录名。登录提示后会出现密码提示。某些服务器会接受空白密码，其他服务器则需要以电子邮件地址形式输入密码。在这种情况下，可以尝试类似 "user@example.com" 的内容。 |
| `cd pub/cd_images/Ubuntu-8.04` | 切换到远程系统上包含所需文件的目录。请注意，在大多数匿名 FTP 服务器上，公共下载的文件都位于 `pub` 目录的某个子目录下。 |
| `ls` | 列出远程系统的目录。 |
| `lcd Desktop` | 将本地系统的目录更改为 `~/Desktop`。在示例中，`ftp` 程序是在工作目录为 `~` 时被调用的。此命令将工作目录更改为 `~/Desktop`。 |
| `get ubuntu-8.04-desktop-i386.iso` | 指示远程系统将文件 `ubuntu-8.04-desktop-i386.iso` 传输到本地系统。由于本地系统的工作目录已更改为 `~/Desktop`，因此文件将被下载到那里。 |
| `bye` | 注销远程服务器并结束 `ftp` 程序会话。命令 `quit` 和 `exit` 也可以使用。 |

在`ftp>`提示符下输入`help`将显示支持的命令列表。在获得足够权限的服务器上使用`ftp`，可以执行许多普通的文件管理任务。它很笨拙，但确实有效。

### `lftp` – 一个更好的`ftp`

`ftp`并不是唯一的命令行 FTP 客户端。事实上，有很多。其中一个更好（也更受欢迎）的客户端是 Alexander Lukyanov 编写的`lftp`。它与传统的`ftp`程序类似，但具有许多额外的便利功能，包括多协议支持（包括 HTTP）、失败下载自动重试、后台进程、路径名制表符补全等。

### `wget`

另一个流行的用于文件下载的命令行程序是`wget`。它可用于从 Web 和 FTP 站点下载内容。可以下载单个文件、多个文件，甚至整个站点。要下载 linuxcommand.org 的首页，我们可以这样做：

``` 
[me@linuxbox ~]$ wget http://linuxcommand.org/index.php
--11:02:51--  http://linuxcommand.org/index.php
=> `index.php'
Resolving linuxcommand.org... 66.35.250.210
Connecting to linuxcommand.org|66.35.250.210|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: unspecified [text/html]

[ <=> ] 3,120      ---.-K/s

11:02:51 (161.75 MB/s) - `index.php' saved [3120]
``` 

该程序的众多选项允许`wget`递归下载、在后台下载文件（允许你在下载继续的同时注销），以及完成部分下载的文件的下载。这些功能在其优于平均水平的 man 手册中有很好的记录。

### 与远程主机的安全通信

多年来类 Unix 操作系统一直具有通过网络远程管理的能力。在互联网普及的早期，有几个流行的程序用于登录远程主机。这些是`rlogin`和`telnet`程序。然而，这些程序与`ftp`程序存在同样的致命缺陷；它们以明文传输所有通信（包括登录名和密码）。这使得它们在互联网时代完全不适合使用。

### `ssh`

为了解决这个问题，开发了一种名为 SSH（Secure Shell）的新协议。SSH 解决了与远程主机安全通信的两个基本问题。首先，它验证远程主机确实是它声称的那台主机（从而防止所谓的“中间人”攻击），其次，它加密本地主机和远程主机之间的所有通信。

SSH 由两部分组成。SSH 服务器在远程主机上运行，监听 22 端口的传入连接，而 SSH 客户端则在本地系统上用于与远程服务器通信。

大多数 Linux 发行版都附带了来自 BSD 项目的 OpenSSH 实现。一些发行版默认包含客户端和服务器包（例如 Red Hat），而其他发行版（如 Ubuntu）仅提供客户端。要使系统能够接收远程连接，它必须安装、配置并运行 OpenSSH-server 包，并且（如果系统正在运行或位于防火墙后面）必须允许 TCP 端口 22 的传入网络连接。

> 提示：如果您没有可连接的远程系统但想尝试这些示例，请确保您的系统上已安装`OpenSSH-server`包，并将`localhost`用作远程主机的名称。这样，您的机器将与自身建立网络连接。

用于连接到远程 SSH 服务器的 SSH 客户端程序恰当地称为`ssh`。要连接到名为 remote-sys 的远程主机，我们将使用`ssh`客户端程序如下：

``` 
[me@linuxbox ~]$ ssh remote-sys
The authenticity of host 'remote-sys (192.168.1.4)' can't be established.
RSA key fingerprint is
41:ed:7a:df:23:19:bf:3c:a5:17:bc:61:b3:7f:d9:bb.
Are you sure you want to continue connecting (yes/no)?
``` 

首次尝试连接时，会显示一条消息，提示无法验证远程主机的真实性。这是因为客户端程序以前从未见过该远程主机。要接受远程主机的凭据，请在提示时输入`yes`。连接建立后，系统会提示用户输入其密码：

``` 
Warning: Permanently added 'remote-sys,192.168.1.4' (RSA) to the list
of known hosts.
me@remote-sys's password:
``` 

输入密码成功后，我们会收到来自远程系统的 shell 提示符：

``` 
Last login: Sat Aug 30 13:00:48 2008
[me@remote-sys ~]$
``` 

远程 shell 会话一直持续到用户在远程 shell 提示符下输入`exit`命令，从而关闭远程连接。此时，本地 shell 会话恢复，本地 shell 提示符重新出现。

也可以使用不同的用户名连接到远程系统。例如，如果本地用户“me”在远程系统上有一个名为“bob”的账户，用户 me 就可以按如下方式登录远程系统上的 bob 账户：

``` 
[me@linuxbox ~]$ ssh bob@remote-sys
bob@remote-sys's password:
Last login: Sat Aug 30 13:03:21 2008
[bob@remote-sys ~]$
``` 
