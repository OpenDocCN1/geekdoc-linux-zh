
如果你无法下载 RPM 版本，或者想自己编译程序，请下载 `samba-tar.gz` 文件。使用以下命令解压文件：

```
tar xfvz samba.tar.gz
```

切换到包含解压文件的目录（通常为 `/usr/src`）并输入：

```
./configure
```

按下回车并等待命令提示符返回。然后输入：

```
make
```

按下回车并等待命令提示符返回。最后，输入 `install`。如果一切顺利，Samba 将已安装。现在你需要配置它，以便 Red Hat Linux 作为 Samba 服务器运行，而 Windows 电脑作为 Samba 客户端。

# 配置 Samba 服务器

从第 2 版本开始，Samba 包含一个名为 SWAT 的工具（Samba Web Administration）。该工具使得设置 Samba 变得非常简单。主配置文件是 `/etc/smb.conf`。SWAT 允许你使用浏览器作为 `/etc/smb.conf` 的界面，并对该文件进行必要的修改。当你使用 SWAT 进行配置时，将了解到更多关于 `smb.conf` 的信息。安装期间的示例 `smb.conf` 文件可以参考，因为它会覆盖原始文件。

`smb.conf` 文件分为若干章节，我在后续讨论中以括号形式显示这些名称。接下来显示的是我网络中某计算机的 `smb.conf` 文件。参考此文件查看章节结构。

```
# 使用 SWAT 创建的 Samba 配置

# 来自 localhost (127.0.0.1)

# 日期: 2000/05/25 10:29:40

# 全局参数
```

```[global]
workgroup = ONE

netbios name = TERRY

server string = Samba Server

security = SHARE

log file = /var/log/samba/log

max size = 50

socket options = TCP_NODELAY SO_RCVBUF=8192 SO_SNDBUF=8192

dns proxy = No

wins support = Yes

hosts allow = 192.168.1.

hosts deny = all

[homes]
comment = 用户目录

read only = No

[printers]
comment = 所有打印机

path = /var/pool/samba

guest ok = Yes

print ok = Yes

browse = Yes

[nancy]
path = /oldwin

valid users = nancy

read only = No

guest ok = no

browse = Yes
```

## [global]

`smb.conf` 文件的第一个章节是 `[global]` 章节。每个章节包含格式如下的选项和值：

`option = value`

你有许多选项和值可供选择，这里列出了最常用的。要查看完整的选项列表，请参阅 `smb.conf` 手页。

- `workgroup = ONE` 是 Windows 计算机网络属性框“标识”选项卡中显示的工作组名称。
- `netbios name = TERRY` 是 Samba 服务器被 Windows 计算机识别的名称。
- `server string = Samba Server` 是 Samba 服务器的名称。

`security = SHARE` 是应用于服务器访问的安全级别。其他可能的选项包括：`user`（默认设置）、`domain`（域）和 `server`（服务器）。使用 `share` 可以更方便地创建不需要身份验证的匿名共享，当 Windows 计算机的 `netbios` 名称与 Linux 计算机上的其他名称不同时，这非常有用。如果密码文件位于网络中的另一台服务器上，则使用 `server`。如果客户端通过 `smbpasswd` 添加到 Windows NT 域，并且登录请求由 Windows NT 主域或备份域控制器处理，则使用 `domain`。

- `log file = /var/log/samba/log` 是日志文件的位置。
- `max log size = 50` 是文件可以增长到的最大大小（单位：KB）。
- `socket options = TCP_NODELAY SO_RCVBUF=8192 SO_SNDBUF=8192` 允许对服务器进行调以提高性能。`TCP_NODELAY` 是默认值，`BUF` 值是发送和接收缓冲区。
- `dns proxy = No` 表示 `netbios` 名称不会被视为 DNS 名称，且不会进行 DNS 查找。
- `wins support = Yes` 用于告诉 Samba 服务器充当 WINS 服务器。
- `hosts allow = 192.168.1.1` 意味着接受来自此网络的请求。
- `hosts deny = all` 意味着所有主机的请求都将被拒绝。

## [homes]

`smb.conf` 文件的下一个部分 `[homes]` 用于允许服务器让用户快速访问其主目录。请参考 `smb.conf` 手页以获取有关 `[homes]` 部分如何工作的完整描述。

- `comment = Home Directories` 是一行注释。
- `read only = No` 指定用户可以向其目录写入内容。

## [printers]

此节设置打印选项。

- `path = /var/spool/samba` 是打印池池目录的位置。
- `guest ok = Yes` 允许访客访问打印机。
- `print ok = Yes` 允许客户端将打印作业发送到指定目录。必须设置此选项，否则打印无法工作。
- `browseable = Yes` 意味着打印机出现在浏览列表中。

在尝试为 Windows 客户端设置打印机之前，请确保你的打印机在 Linux 网络中已正确配置。你需要在 `smb.conf` 文件中输入要使用的打印机的打印池路径位置。

## [nancy]

此 `smb.conf` 文件的最后一部分称为 `[nancy]`。这是我妻子使用的电脑，所以我为她命名了此共享名称。

- `path = /oldwin` 是 `nancy` 可访问的目录路径。
- `valid users = nancy` 指定了可以使用该共享的用户。
- `read only = No` 允许对目录进行写操作访问。
- `guest ok = no` 防止访客访问。
- `browseable = yes` 意味着共享在浏览列表中可见。

你刚刚分析的 `smb.conf` 文件是使用 SWAT 程序创建的，如文件开头的注释行所示。你也可以通过输入之前显示的选项值来从头创建此文件，或者通过修改随程序安装的 `smb.conf` 文件来创建。记住，你查看的是一个针对小型网络的简单文件。关于选项和值的完整细节，请始终参考 `smb.conf` 手页。接下来你将使用 SWAT 来配置 `smb.conf`。

## 使用 SWAT

在可以使用 SWAT 之前，你需要更改两个文件来启用它。第一个文件是 `/etc/services`。该文件是互联网服务及其端口号和协议的列表。你需要在 `/etc/services` 中添加以下行：

```
Swat 901/tcp
```

接下来，你需要在 `/etc/inetd.conf` 中添加一行。`inetd` 守护进程在系统启动时运行并监听特定端口上的连接。`inetd.conf` 文件列出了当 `inetd` 检测到其中一个端口上的请求时应该运行的程序。你需要添加以下行：

```
Swat stream tcp nowait.400 root /usr/sbin/swat swat
```

## 第 9 章：连接到微软网络

如果你对添加的行有更多细节感兴趣，请查看 `inet` 手页。最后，你需要重启 `inet` 守护进程以便其读取你对 `inet.conf` 所做的更改。执行此操作，请在命令行提示符输入：

```
killall inet
```
