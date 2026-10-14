

## 表 16-1 *(continued)*

| 命令 | 含义 |
|---|---|
| `lcd Desktop` | 将本地系统的目录更改为 `~/Desktop`。在示例中，`ftp` 程序是在工作目录为 `~` 时被调用的。此命令将工作目录更改为 `~/Desktop`。 |
| `get ubuntu-8.04-desktop-i386.iso` | 指示远程系统将文件 `ubuntu-8.04-desktop-i386.iso` 传输到本地系统。由于本地系统的工作目录已更改为 `~/Desktop`，文件将下载到那里。 |
| `bye` | 注销远程服务器并结束 `ftp` 程序会话。命令 `quit` 和 `exit` 也可使用。 |

在 ftp> 提示符下输入 help 将显示支持的命令列表。在获得足够权限的服务器上使用 ftp，可以执行许多普通的文件管理任务。它很笨拙，但确实有效。

## lftp—更好的 ftp

ftp 并不是唯一的命令行 FTP 客户端。事实上，有很多。其中之一更好的（也是更受欢迎的）是 Alexander Lukyanov 的 lftp。它与传统的 ftp 程序工作方式类似，但具有许多额外的便利功能，包括多协议支持（包括 HTTP）、失败下载自动重试、后台进程、路径名制表符补全等。

## wget—非交互式网络下载器

另一个流行的命令行文件下载程序是 wget。它可用于从 Web 和 FTP 站点下载内容。可以下载单个文件、多个文件，甚至整个站点。要下载 http://www.linuxcommand.org/ 的第一页，我们可以这样做：

```
me@linuxbox:~$ wget http://linuxcommand.org/index.php
--11:02:51--  http://linuxcommand.org/index.php
           => `index.php'
Resolving linuxcommand.org... 66.35.250.210
Connecting to linuxcommand.org|66.35.250.210|:80... connected.
```

```
HTTP request sent, awaiting response... 200 OK
Length: unspecified [text/html]

  [ <=> ] 3,120    --.-K/s

11:02:51 (161.75 MB/s) - `index.php' saved [3120]
```

该程序的众多选项允许 wget 递归下载、在后台下载文件（允许你注销但继续下载），以及完成部分下载的文件的下载。这些功能在其优于平均水平的 man 手册中有详细记录。

## 与远程主机安全通信

多年来类 Unix 操作系统一直具有通过网络远程管理的能力。在互联网广泛采用的早期，有几个流行的程序用于登录远程主机：rlogin 和 telnet 程序。然而，这些程序与 ftp 程序存在同样的致命缺陷；它们以明文传输所有通信（包括登录名和密码）。这使得它们在互联网时代完全不适合使用。

## ssh—安全地登录远程计算机

为了解决这个问题，开发了一种名为 SSH（Secure Shell）的新协议。SSH 解决了与远程主机安全通信的两个基本问题。首先，它验证远程主机确实是它声称的那台主机（从而防止中间人攻击），其次，它加密本地主机和远程主机之间的所有通信。

SSH 由两部分组成。SSH 服务器在远程主机上运行，在端口 22 上监听传入连接，而 SSH 客户端则在本地系统上使用以与远程服务器通信。

大多数 Linux 发行版都附带了来自 BSD 项目的 OpenSSH 实现。一些发行版默认包含客户端和服务器包（例如 Red Hat），而其他发行版（如 Ubuntu）仅提供客户端。要使系统能够接收远程连接，它必须安装、配置并运行 OpenSSH-server 包，并且（如果系统正在运行或位于防火墙后面）必须允许 TCP 端口 22 的传入网络连接。

> 注意：如果您没有可连接的远程系统但想尝试这些示例，请确保您的系统上已安装 OpenSSH-server 包，并使用 localhost 作为远程主机的名称。这样，您的机器将与自身建立网络连接。

