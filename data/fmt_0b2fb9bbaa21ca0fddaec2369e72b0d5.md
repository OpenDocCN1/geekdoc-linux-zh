
- `restart { all|printer }`——尝试重启打印守护进程。有时 `lpd` 进程会崩溃或卡住，这将尝试重启一个新的守护进程。
- `status { all|printer }`——获取打印机状态并列出队列是否启动或打印是否启用。
- `topq printer [job..]`——打印队列顶端列出的作业。

`lpc` 的 `man` 页有更多关于可用命令的内容但这些将帮助你开始队列管理。

在最坏的情况下，如果 `lpc` 命令不起，你可以使用 `/etc/rc.d/init.d/lpd.init stop` 命令完全停止 `lpd` 程序。`/etc/rc.d/init.d/lpd.init start` 命令将启动 `lpd`。

有关打印的更多信息或帮助，请查看 `Printing HOWTO`。

## 7.7 Ghostscript

`Ghostscript` 被 Red Hat 用于转换 postscript。虽然它很复杂，但它非常强大。它可以将 postscript 转换为其他格式，如 PDF。虽然它很复杂，但它非常强大。它可以将 postscript 转换为其他格式，如 PDF。虽然它很复杂，但它非常强大。它可以将 postscript 转换为其他格式，如 PDF。虽然它很复杂，但它非常强大。它可以将 postscript 转换为其他格式，如 PDF。虽然它很复杂，但它非常强大。它可以将 postscript 转换为其他格式，如 PDF。虽然它很复杂，但它非常强大。它可以将 postscript 转换为其他格式，如 PDF。虽然它很复杂，但它非常强大。它可以将 postscript 转换为其他格式，如 PDF。

## 7.8 总结

- `Samba` 用于在 Windows 网络上显示 Linux 打印机。
- `Ghostscript` 是一个强大的打印工具。它可以将 postscript 转换为其他格式，如 PDF。

## 8.1 设置 MS 网络

从 Linux 打印到 Windows 机器，步骤稍有不同。Red Hat 允许你（通过 `printtool`）添加一个通过服务器消息块 (`SMB`) 连接的打印机，`printtool` 会处理其余工作。Windows 机器会获取打印作业并将其发送到打印机。Windows NT 也可以处理 `LPD` 协议，因此你可能想使用它。

为了设置 `Samba`，你需要配置 `/etc/printcap` 文件和 BSD 风格打印。这几乎包含了 Linux 为 Windows 98 或 Windows NT 机器提供打印机服务所需的所有配置。

## 8.2 安装 Samba

软件安装完成后，你应该能够浏览网络并看到所有其他机器，至少是与其处于同一子网的机器。如果你无法实现，请将软件安装到这一步。如果出现问题，通常会得到一个关于问题及其解决方法的、有些晦涩的解释。

在工作组中，通常没有中央服务器。用户名和密码会根据需要通过服务器进行身份验证。

### 什么是域？

Windows NT 域有一个中央密码服务器，在用户登录 Windows 机器时对其其进行身份验证。它不是在 Windows 登录界面上检查本地密码，而是将密码发送到 `PDC`（主域控制器），由其授予访问该域内所有服务器上服务的权限。

如果你在网络上有一个 `PDC` 并选择让 `Samba` 对此进行验证，你就可以将网络配置为域。否则，选择工作组。

### 安装 TCP/IP 栈

Windows 98 和 Windows NT 在安装时都已自带 `TCP/IP` 栈。当 Windows 请求用户名和密码时，请确保提供在你正在验证的任何系统中可用的用户名。

我们假设你已经如何设置 `TCP/IP` 网络。如果不知道，请查看网络章节获取有关如何操作的信息。一旦在所有 Windows 机器上加载了 `TCP/IP` 栈，尝试让他们互相 `ping`，或者 `ping` Linux 机器。Linux 机器也应该能够 `ping` 其他子网的机器。

## 8.2 安装 Samba

现在 Windows 机器已设置完毕，让我们转向 Linux 机器。如果你在 Red Hat 安装屏幕上选择了 `DOS/Windows` 连接，则已安装 `Samba`，并且可以通过 Red Hat 发行版的 `Samba` 访问。如果没有安装，可以从 `contrib.redhat.com` 或 `www.samba.org` 安装更新的 RPM 包。

除非你的桥器转发 `TCP/IP` 数据包，否则你将无法看到子网以外的内容。路由器通常不会转发 `SMB` 数据包，因为它只处理 `TCP/IP`。但由于 `Samba` 寄基于 `TCP/IP`，你仍然可以连接到其他子网的机器。

# 第 8 章 • Samba

你可以检查示例配置文件 `/etc/smb.conf` 并针对你的网络对其进行调整。以下是 `smb.conf` 文件的示例：

```
[global]
printing = bsd
printcap name = /etc/printcap
# 上述列出了打印方法。Linux 使用 BSD 打印，因此我们使用
# BSD 打印和 /etc/printcap。
load printers = yes
guest account = nobody
# 如果用户可以在没有认证的情况下连接，上述就是
# 连接的名称。
log file = /var/log/samba.log.%m
admin users=markk
# 对所有文件具有完全访问权限的用户
read prediction = yes
dead time = 15
workgroup=WORKGROUP
mangled map=(*.html,*.htm)
lock directory = /var/log/samba
share modes = yes
os level = 33
domain master = yes
```

```
[homes]
comment = 目录
browseable = no
read only = no
create mode = 0750
read size = 8192
max xmit = 8192
# 上述两个选项尝试以 8kB 块进行读写。
```

```
[printers]
comment = 所有打印机
browseable = no
# 此条目会扩展到每个可用打印机，我们不希望
# 在浏览列表中看到实际的条目。
printable = yes
public = yes
# 我们希望任何人都能打印，即使没有认证。
writable = no
# 无法在打印机上存储文件，对吧？
create mode = 0700
```

```
[pcsoft]
comment = PC 软件
# 注释其在浏览列表中显示
path = /vol/repository
# 用于共享的 Linux 目录
public = no
# 用户可以在没有认证的情况下连接吗？不能。
writable = yes
printable = no
create mode = 0666
# 上述设置了 Linux 侧的文件权限。
# 它被设置为所有者、组和世界可读可写。
```

```
[accounting]
path = /home/bob/bob
valid users = fred bob
# 只有 fred 和 bob 可以访问此共享。
public = no
only guest = no
browseable = no
writable = yes
create mask = 0777
```

就像 Windows 的 `system.ini` 文件被分为以括号中单词开头的部分一样；`smb.conf` 文件也是如此。`[global]`、`[printers]` 和 `[homes]` 是仅三个保留的节头。所有其他内容都被认为是提供给 `SMB` 客户端的共享名称。

`[global]` 部分选项适用于整个程序。例如，`mangled map` 选项设置所有以 `.htm` 结尾的文件应被写入 Linux 服务器为 `.html`。这使得在 Windows 中编写文件并将其发送到 Web 服务器变得更容易。

- 其他值得注意的选项包括：
- `log file`——当 `samba` 启动时，它将写入日志文件。在上述情况下，日志文件名为 `samba-log` 加上机器名。
- `dead time`——在没有活动 `dead time` 分钟后，`smb` 连接将断开。这不仅有助于节省 Linux 服务器的资源。
- `admin users`——对所有文件具有完全访问权限的用户。
- `workgroup`——工作组名称。
- `guest account`——如果用户可以在没有认证的情况下连接，上述就是连接的名称。
- `mangled map`——设置所有以 `.htm` 结尾的文件应被写入 Linux 服务器为 `.html`。

# Linux SMB 连接

现在你已经通过 `Samba` 让 Windows 机器与 Linux 之间实现了通信，那么如何从 Linux 访问 `SMB` 共享呢？很简单：使用 `Samba` 客户端和其他 Linux 下的 `SMB` 工具即可。

## smbfs
