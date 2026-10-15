
`/usr` 目录包含软件应用程序、库和其他类型的共享数据，供系统上的任何人使用。许多 Linux 系统管理员会为 `/usr` 分配独立分区。`/usr` 下的许多子目录包含手册页（`/usr/share/man`）、软件包共享文件（`/usr/share/name_of_package`，例如 `/usr/share/emacs`）、额外的应用程序或软件包文档（`/usr/share/doc`），以及一个完整的本地构建和安装软件的子目录树 `/usr/local`。

## /tmp 目录中的临时文件存储

顾名思义，`/tmp` 目录用于临时文件存储；当你使用 Linux 时，各种程序会在此目录中创建文件。

## 访问 /var 目录中的可变数据文件

`/var` 目录包含各种系统服务用于假脱机和日志记录的子目录。这些可变数据文件中有很多是临时的，例如打印假脱机队列；而另一些，如系统日志和内核日志，在使用中会被重命名和轮转。传入的电子邮件通常定向到 `/var/spool/mail` 下的文件。

Linux 还将 `/var` 用于其他重要系统服务。这些服务包括 `/var/ftp` 下的顶层文件传输协议（FTP）目录（见第 18 章“使用 FTP 进行远程文件服务”），以及 Apache Web 服务器在系统上的初始主页目录 `/var/www/html`。（关于使用 Apache 的更多信息，请参见第 17 章“Apache Web 服务器管理”。）

## 登录并使用 Linux

你可以通过多种方式访问和使用 Linux 系统。一种是在控制台前，使用连接到 PC 的显示器、键盘和鼠标。另一种是通过串行控制台，既可以通过调制解调器拨号，也可以通过运行终端仿真器并借助空调制解调器电缆连接到 Linux PC 的方式。你还可以通过有线或无线网络，使用 `telnet` 或 `ssh` 命令连接到系统。本节的信息将向你展示如何使用物理和远程文本登录来访问和使用 Linux 系统。

### 注意

本章重点介绍基于文本的登录和 Linux 的使用。图形登录和使用图形桌面将在第 3 章“使用 Gnome”中介绍。

### 基于文本的控制台登录

如果你坐在 PC 前，登录一个未启动到图形登录界面的 Linux 系统，你会看到类似如下的提示符：

```
Ubuntu 8.04 (hardy) ubuntu tty1
login:
```

你的提示符可能会因所用 Ubuntu 版本的不同而有所不同。无论如何，在此提示符下输入你的用户名并按回车键。当提示输入密码时，输入密码并按下回车键。

### 注意

注意，你的密码不会回显出来，这是一个好主意。为什么说这是好主意？嗯，这样可以防止别人从你身后偷看你的屏幕输入。不难猜到，一个五个字母的密码可能对应着用户配偶的名字！

### 注销

使用 `exit` 或 `logout` 命令退出你的会话。输入命令并按回车键。然后你会返回登录提示符。如果你使用虚拟控制台，请记得在离开 PC 前退出每个控制台。（否则，别人可以轻易坐下来使用你的帐户。）

### 从远程计算机登录和注销

虽然你可以在自己的计算机上愉快地登录，这被称为本地登录，但你也可以通过网络连接从远程计算机登录到你的计算机。基于 Linux 的操作系统提供了许多远程访问命令，你可以使用它们登录到本地局域网 (LAN)、广域网 (WAN) 或互联网上的其他计算机。请注意，你不仅必须在远程计算机上拥有一个账户，而且远程计算机必须配置为支持远程登录——否则，你将无法登录。

> NOTE
>
> 请参阅第 14 章“Networking”，了解如何使用 Linux 设置网络接口以支持远程网络登录，并参阅第 11 章，了解如何启动远程访问服务（如 `sshd`）。

登录远程 Linux 计算机最好且最安全的方式（不考虑未来漏洞）是使用 `ssh` 或 Secure Shell 客户端。你在远程计算机上的登录和会话在工作时都会被加密。`ssh` 客户端具有许多不同的命令行选项，但可以用远程计算机的名称或 IP 地址简单地使用，如下所示：

```
[andrew@hardy-dev ~]$ ssh 192.168.0.41
The authenticity of host '192.168.0.41 (192.168.0.41)' can't be established.
RSA key fingerprint is e1:db:6c:da:3f:fc:56:1b:52:f9:94:e0:d1:d1:31:50.
Are you sure you want to continue connecting (yes/no)?

yes
```

第一次使用 `ssh` 连接到远程计算机时，Linux 会显示远程计算机的加密身份密钥并要求你验证连接。在你输入 `yes` 并按 Enter 后，会警告你远程计算机的身份（密钥）已输入到你的主目录下 `.ssh` 目录中的 `known_hosts` 文件中。你还会被提示输入密码：

```
Warning: Permanently added '192.168.0.41' (RSA) \
to the list of known hosts.
andrew@192.168.0.41's password:
andrew-$
```

输入密码后，你就可以在远程计算机上工作了。同样，你在与远程计算机通信时键盘上输入的所有内容都会被加密。使用 `exit` 或 `logout` 命令退出会话并返回到计算机上的 shell。

```
GTK_RC_FILES=/etc/gtk/gtkrc:/home/andrew/.gtkrc-1.2-gnome2

WINDOWID=58623199

USER=andrew

...
USERNAME=andrew

PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games

DESKTOP_SESSION=default

GDM_XSERVER_LOCATION=local

PWD=/usr/local

LANG=en_GB.UTF-8

GNOME_KEYRING_PID=5714

GDM_LANG=en_GB.UTF-8

SHLVL=1

HOME=/home/andrew

LOGNAME=andrew

XDG_DATA_DIRS=/usr/local/share/:/usr/share/:/usr/share/gdm/

...
LESSOPEN="| /usr/bin/lesspipe %s"

WINDOWPATH=7

DISPLAY=:0.0

LESSCLOSE="/usr/bin/lesspipe %s %s"

COLORTERM=gnome-terminal

XAUTHORITY=/home/andrew/.Xauthority

_=/usr/bin/env
```

`OLDPWD=/usr/share/locale`

这个简短的列表显示了一些常见的变量。这些变量由包含在 `/etc`、`/etc/skel` 或用户 `/home` 目录中的配置或资源文件设置。例如，你可以在 `/etc/profile`、`/etc/bashrc`、`.bashrc` 或安装在你的主目录中的 `.bash_profile` 文件中找到 `bash` 的默认设置。阅读 `bash` 的 `man` 手册，了解有关使用这些配置文件的信息。

最重要的环境变量之一是 `$PATH`，它定义了可执行文件的位置。例如，如果作为普通用户，你尝试使用不在你的 `$PATH` 中的命令（例如虚构的 `command` 命令），你会看到类似这样的内容：

```
$ command
-bash: command: command not found
```

> **NOTE**
>
> 如果你尝试执行的命令确实存在，但尚未安装在你的系统上，那么 Ubuntu 会提示你安装它，甚至会给出正确的命令。

然而，你可能知道 `command` 确实已安装在你的系统上，并且你可以使用 `whereis` 命令来验证，如下所示：

```
$ whereis command
command: /sbin/command
```

你也可以通过输入其完整路径名或完整目录规范来运行该命令，如下所示：

```
$ /sbin/command
```

正如这个例子所示，`command` 命令确实已安装。发生的情况是，默认情况下，`/sbin` 目录不在你的 `$PATH` 中。其原因之一是 `/sbin` 目录下的命令通常仅 intended 由 `root` 运行。你可以通过编辑主目录中的 `.bash_profile` 文件将 `/sbin` 添加到你的 `$PATH`（如果你默认使用 `bash` shell，就像大多数 Linux 用户一样）。查找以下行：

```
PATH=$PATH:$HOME/bin
```

然后你可以使用 `vi` 编辑器（本章中讨论）编辑此文件，如下所示添加 `/sbin` 目录：

```
PATH=$PATH:/sbin:$HOME/bin
```

一些基于控制台的文本编辑器有

- `emacs`—全面的 GNU `emacs` 编辑环境，它远不止一个编辑器；请参阅本章后面“使用 `emacs`”一节
