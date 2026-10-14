
# 第二部分：面向桌面用户的 Ubuntu

## 第 25 章：连接到其他系统

本节剩余部分讨论如何使用`ssh`连接到实际运行`ssh`守护进程的远程系统。有关如何在 Ubuntu 系统上启用`ssh`守护进程的信息，请参见下一节。作为当前用户使用`ssh`连接到远程系统只需输入`ssh hostname`命令，其中`hostname`是要连接的主机名称或 IP 地址。

当你第一次尝试连接到一个以前从未连接过的远程系统时，你将看到如下所示的消息。

```
$ ssh laptop
The authenticity of host 'laptop (192.168.6.90)' can't be established.
RSA key fingerprint is 07:6e:3a:50:4b:4d:e6:d8:f1:b0:c6:b2:da:02:a3:da.
Are you sure you want to continue connecting (yes/no)?
```

要继续连接到此系统，请输入`yes`并按回车键。`ssh`实用会将远程系统的 RSA 密钥添加到其已知主机列表中（以防止未来有其他机器伪装远程机器），并提示你输入密码，或者在下面的示例中：

```
Warning: Permanently added 'laptop' (RSA) to the list of known hosts.
wwh@laptop's password:
```

### 注意事项

如果你好奇，RSA 代表 Rivest、Shamir 和 Adleman，他们是 OpenSSH 实现的`ssh`所使用的公钥加密技术的开发者。有关公钥基础设施 (PKI) 和相关加密技术的更多信息，请参见维基百科上的 PKI 信息网站：http://en.wikipedia.org/wiki/Public_key_infrastructure。

在提示处，输入远程系统的密码并按回车键。假设你输入了正确的密码，你将看到来自远程系统的成功登录消息，系统提示符将显示（如下所示）：

```
Linux ubuntu32 2.6.24-19-386 #1 SMP Fri Jul 11 16:43:33 UTC 2008
```

Ubuntu 系统中包含的程序是免费软件；每个程序的具体分发条款在`/usr/share/doc/*/copyright`的各个单独文件中描述。

```
Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted
by applicable law.
Last login: Wed May 1 20:15:16 2008
wwh@ubuntu32:-
```

一旦你建立了与远程机器的`ssh`连接，你就可以执行对该机器物理连接上可以做的任何操作，包括如果你正确使用`DISPLAY`环境变量，启动显示在你本地系统上的图形化应用程序，这在第 5 章“使用 GNOME 桌面”中的“什么是桌面？Linux 的图形环境”中讨论过。当你在远程系统工作时，可以通过按 Ctrl+D 或输入`exit`命令注销。

这一切的前提是你在你想要连接的所有系统上具有相同的登录用户名，或者你总是想以自己的身份进行连接。幸运的是，`ssh`命令提供了一种简单的方法与其他用户身份连接到另一个系统，可以使用如`ssh@host`的命令，其中`user`是你想要登录的用户名，`host`是你想以该用户连接的主机名。例如，命令`ssh joeuser@laptop`将使用`ssh`以用户`joeser`的身份连接到远程主机。

假设你知道该用户的密码，你就可以以指定用户的身份登录并执行该用户被授权的任何操作。

`ssh`命令还有许多其他选项，你可能永远都不需要使用其中几个。有关`ssh`命令的完整信息，如果需要，可以查看通过`man ssh`命令提供的在线参考信息。

## 为你的系统启用入站 SSH 连接

如本章前面所述，如果你想使用任何需要 SSH 协议的命令远程连接到你的系统，则你的系统上必须运行`ssh`守护进程。Ubuntu 系统可用的标准版本 SSH 服务器是 OpenSSH 服务器 (www.openssh.org)，这是一个开源 SSH 服务器，由同样支持 OpenBSD 项目 (www.openbsd.org) 的人员积极维护，OpenBSD 是一个开源 UNIX 类分发版，以其对系统安全的关注而闻名。标准的 Ubuntu 安装中，默认不安装 OpenSSH 服务器（但 Ubuntu 中的所有内容）都可以使用第 19 章中描述的任何包管理工具轻松添加。

要安装 OpenSSH 服务器，请使用你喜欢的安装包来安装`openssh-server`包。我倾向于在 Ubuntu 系统上使用图形化的 Synaptic 包管理器，但如果你喜欢，也可以使用命令行包管理器。

作为安装 OpenSSH 服务器的一部分，Ubuntu 会向系统启动过程添加脚本，以便在启动系统时自动启动。旧版本的 Ubuntu 提供了一个图形化的系统管理服务，要在 Ubuntu 10.04 系统中查看此，你必须安装此类软件包，例如 Boot-Up Manager 应用程序（通过安装`bum`包）或我最喜欢的`sysv-rc-conf`（来自同名包），它提供了一个简单的接口用于在系统启动和各种运行级别下激活或禁用服务。图 25-1 显示了在 GNOME 终端窗口中激活 SSH 到运行级别 2 及以上以后的`sysv-rc-conf`。

如果你想通过 SSH 启用对系统的远程登录，只需再次运行`sysv-rc-conf`，向下滚动到图 25-1 中的 SSH 条目，并勾选如 2 等主要运行级别的复选框。

### 提示

VNC 服务器是 OpenSSH 的一个非常有吸引力的替代方案，它可以让你轻松地查看系统上安装的服务以及它们所在的系统运行级别。

### 图 25-2

在 Ubuntu 系统上配置 vino VNC 服务器

![](img/1a233c34336fbf5a85d6eb785e401709_950_0.png)

在配置 vino 服务器时，请务必在图 25-2 所示对话框的“安全”部分中设置远程桌面密码。要执行此操作，请勾选“要求用户输入此密码”复选框并输入密码。你可以选择性勾选“确认每次对此机器的访问”复选框，当有人尝试使用 VNC 客户端连接它时，你的桌面上将显示如图 25-3 所示的对话框。

### 图 25-3

Ubuntu 桌面上的远程连接请求

![](img/1a233c34336fbf5a85d6eb785e401709_950_1.png)

通常，我不建议启用此选项。首先，是因为这在很大程度上违背了最初支持远程 VNC 连接的初衷；其次，是因为对你的 VNC 服务器的访问应该应该密码保护，因此只有你给了密码的人才能通过 VNC 访问你的桌面。

一旦你使用“远程桌面首选项”对话框启用了远程访问，GNOME 桌面就会启动`vino-server`进程，并在每次在此 Ubuntu 系统上启动 GNOME 登录会话时自动启动。

### 传统 VNC 服务器的工作原理

通常，VNC 服务器由系统守护进程作为`inetd`或`xinetd`启动，或者通过名为`vncserver`的 shell 或 Perl 脚本启动，它们导出自己的显示器，而不是当前登录用户的桌面。这些机制为你的 VNC 服务器环境提供了额外的灵活性。由`inetd`或`xinetd`响应连接请求启动的 VNC 服务器可以启动多个提供不同桌面尺寸和分辨率的服务器，如果你的系统有一个 21 英寸显示器，并且你想从笔记本电脑连接而无需来回滚动，这将非常方便。如果你使用`vncserver`脚本启动 VNC 服务器，你还可以利用用户特定的启动脚本来识别管理器以及你的 VNC 服务器应该启动的任何应用程序。VNC 服务器脚本通常是文件`~/.xstartup`。如果当你第一次启动 VNC 服务器时该目录和启动文件不存在，则会创建该目录并从默认窗口启动文件`/etc/X11/xinit/xinitrc`克隆启动脚本。

导出独立于任何物理显示器的图形化控制台并使用启动脚本，使得传统的 VNC 服务器能够遵循通常使用的、复杂的 X Window 启动文件链：`~/.xinitrc`、某些系统上的`~/.Clients`、`/etc/X11/xinit/xinitrc`、`/etc/X11/XSession`等。这些启动文件可以通过环境变量设置启动各种桌面环境和窗口管理器，并在此找不到其他窗口管理器时，提供启动`twm`窗口管理器作为最后手段的方案。

遵循这种更传统模型并适用于 Ubuntu 系统的 VNC 服务器包括`vnc4server`和`tightvncserver`软件包，你可以使用你的包管理工具安装它们。但是，如果你在 Ubuntu 系统上安装了其中一个，你应该卸载 vino VNC 服务器。

### 用于其他系统的 VNC 客户端和服务器软件
