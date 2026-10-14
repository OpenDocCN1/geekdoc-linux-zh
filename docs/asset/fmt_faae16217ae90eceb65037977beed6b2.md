
![](img/cbac72550c7126a22162e94d91a0c360_540_0.png)

# 网络与互联网服务

## 第二部分

`\` 表示当前工作目录。通过此命令行，你可以发布表 16.1 所示的命令来传输和处理文件。

# 表 16.1 smClient 命令

| 命令 | 参数 | 说明 |
| :--- | :--- | :--- |
| ? or help | [command] | 提供命令的帮助信息，如果未指定命令，则提供通用帮助。 |
| ! | [shell command] | 执行指定的 shell 命令或让用户进入 shell 提示符。 |
| cd | [directory] | 切换到服务器上的指定目录（而不是本地机器）。如果没有指定目录，`smclient` 会报告当前工作目录。 |
| lcd | [directory] | 切换到本地机器上的指定目录。如果没有指定目录，`smclient` 将报告当前工作目录。 |
| del | [files] | 如果你有权限，将删除服务器上的指定文件。文件可以包含字符。 |
| dir or ls | [files] | 列出指定的文件。你也可以使用 `ls` 命令获取文件列表。 |
| exit or quit | none | 退出 smclient 程序。 |
| get | [remotefile] [local name] | 获取指定的远程文件并将其保存到本地服务器。如果指定了 *local name*，则复制的文件将以此文件名保存，而不是远程服务器上的文件名。 |
| mget | [files] | 将所有指定的文件（包括通配符）复制到本地。如果在在此命令之前输入了 `recursion`，也将复制所有目录的内容。 |
| md or mkdir | [directory] | 在远程机器上创建指定的目录。 |
| rd or rmdir | [directory] | 在远程机器上删除指定的目录。 |
| put | [localfile] [remotename] | 将指定的文件从本地机器复制到服务器。 |
| mput | [files] | 将本地机器上的所有指定文件复制到服务器。如果在在此命令之前输入了 `recursion`，也将复制所有目录的内容。 |
| print | [file] | 打印远程机器上的指定文件。 |
| queue | none | 显示远程机器上所有的打印任务。 |

# 在 Linux 客户端挂载共享

为了让生活更简单，`smstatus` 允许挂载 Samba 共享。如果 Samba 服务器尚未识别 Windows，请刷新屏幕或重启 Windows。在出现问题的情况下，通常怀疑的对象是 Windows 尚未识别 Samba，用户和密码问题。在 Samba 服务器尚未识别 Windows 的情况下，请在 `[global]` 中临时设置 `username level` 和 `password level` 为一个较大的值，如 100。然后设置 `encrypt passwords = yes` 和 `smb passwd file = /etc/smpasswd`。在 `[global]`。

为了，请执行以下命令：

```
smclient //192.168.100.1/homes -U [
```

# 在 Windows 客户端挂载共享

![](img/cbac72550c7126a22162e94d91a0c360_542_0.png)

# 使用 SWAT 进行 Samba 配置

SWAT 是一种基于 Web 的工具，允许从可以访问服务器的浏览器进行密码保护的 Samba 管理。SWAT 随 Samba 2 新推出，且 SuSE 6.2 Samba Samba 2.0.5a。

> 注意
> 使用 SWAT 会 你的你的 `smb.conf` 文件。它将消除所有注释，消除 `include=` 和 `copy=` 选项，消除许多设置为默认值的选项，并将选项更改为更常见的同义词（在某些情况下为反同义词，同时反转值）。SWAT 还会消除 `[GLOBAL]` 行。这是因为出现在文件顶部的括号斜杠会被 Samba 视为 [GLOBAL] 的一部分。

在使用 SWAT 配置之前始终备份 `smb.conf`。使用 SWAT 配置的 `smb.conf` 文件短得多，更具可读性。注释和自文档化默认配置的丢失可能会降低其可读性。如果你为了可读性和自文档化定制了 `smb.conf`，你可能想避免使用 SWAT。

SWAT 是一种通过减少错误来提高安全的便利工具。然而它会极大改变 `smb.conf`，如果不谨慎使用，可能会导致安全漏洞。

# 在你的服务器上激活 SWAT

1. 验证 `/etc/services` 包含以下行。该行不应被注释。

```
swat      901/tcp
```

2. 取消 `/etc/inetd.conf` 中以下行的注释：

```
swat stream  tcp nowait.400 root /usr/sbin/swat swat
```

3. 找到 `inetd` 的 PID。

执行以下命令：

```
kill -f PID
```

找到 `inetd` 进程 ID（PID）的最简单方法是输入 `ps -ef | grep inetd`。进程 ID 将位于左起第二列。

该步骤应能在典型的 SuSE 服务器上成功启用 SWAT。下一步是通过 SWAT 访问 Samba 配置。

# 使用 SWAT 从你的浏览器中配置 smb.conf

## 安全警告

在完成 SWAT 操作后，你必须关闭工作站上的所有浏览器。所有打开的浏览器都会“记住”密码，这会导致任何能够物理访问你工作站（或服务器终端）的人都能访问 Samba 配置，包括密码管理。

此外，如果是在远程工作站的浏览器上使用 SWAT，密码将以明文形式传输并可能被嗅探。

为了获得最佳安全性，请仅在服务器终端上使用 SWAT，并在完成后关闭所有浏览器。

从你喜喜欢的浏览器（包括 Netscape Navigator、Microsoft Internet Explorer 或 Lynx），导航到服务器 IP 地址的 901 端口：

```bash
#Lynx http://192.168.100.1:901
```
