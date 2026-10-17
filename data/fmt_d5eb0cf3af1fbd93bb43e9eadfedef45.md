
在继续之前，我们应该更改旧 Windows NT 服务器的名称并重新加入域。任何名称都可以（例如 `F000`），因为其域成员身份将是短暂的。一旦服务器重新加入域，我们就可以使用域管理员账户（例如 `GLASS\Administrator`）登录。

![](img/e6dc042fe420c610acdd193e834a4772_278_0.png)

在这里，我们把本地 `c:\users` 目录下的所有内容复制到 `\BEVELED\USERS`。

```
C:\users>scopy \beveled\users /s
C:\users\foo2 -> \beveled\users\foo2
C:\users\foo2\AUTOEXEC.BAT -> \beveled\users\foo2\AUTOEXEC.BAT
C:\users\foo2\testing -> \beveled\users\foo2\testing
C:\users\user1 -> \beveled\users\user1
C:\users\user1\09fig9a.bmp -> \beveled\users\user1\09fig9a.bmp
File(s) copied: 5
```

在 Windows NT 4.0 服务器资源工具包的补充 4 中，该工具应该被标准的 `xcopy.exe` 命令取代，该命令作为 Windows NT 4.0 操作系统的一部分包含在。个人而言，在使用 `xcopy.exe` 安全文件/目录信息方面遇到过困难。

## 图 14.6

Windows NT 4.0 资源管理器显示的 `C:\USERS\user1` 原始权限。

![](img/e6dc042fe420c610acdd193e834a4772_279_0.png)

将目录复制到使用 POSIX ACL 的 Samba 服务器后，Windows ACL 被转换为：

```
# file: user1
# owner: GLASS\Administrator
# group: GLASS\Domain Users
user::rwx
user:GLASS\user1:rwx
group::-
group:GLASS\Domain Admins:rwx
mask::rwx
other::-
default:user::rwx
default:user:GLASS\user1:rwx
```

# 替换 Windows NT 文件打印服务器——全面替换

```
default:group::::-
default:group:GLASS\Domain Admins:rwx
default:mask::rwx
default:other::::-
```

## 图 14.7

显示了 Linux/Samba 服务器上使用 POSIX ACL 存储的新 `\BEVELLED\USERS` 的权限。

![](img/e6dc042fe420c610acdd193e834a4772_280_0.png)

14.7 显示了 ACL 在 Windows NT 安全对话框中的外观。这引出了几个可能会引起困惑的点。

- 就像我们在不感知 ACL 的文件系统上一样，Samba 使用“获取所有权”（o）位报告为无权限（即 `--`），它看起来像是 0 位。这仅仅是报告权限的约定，并不会赋予指定用户任何额外的访问权限。
- `rwx` 权限集被报告为等同于完全控制（ALL）访问权限。

## 关于打印机的简要说明

在将所有文件复制到 Samba 服务器后，是时候处理将 `[hp4]` 打印机从旧 NT 服务器移动到我们的 Samba 主机的细节了。遗憾的是，没有简单的方法可以将打印队列从一个 Windows NT 移动到另一个。这意味着没有简单的方法可以将打印队列从 Windows NT 主机移动到 Samba 服务器。

我们唯一的选择是在 Samba 机器上重新创建打印机并手动重置权限。这意味着我们还需要手动安装必要的驱动程序。所有这些在第 9 章中都介绍过。

## 第 3 步：测试服务器

我们已经验证了服务器的部分。但正如任何经验丰富的网络管理员都会告诉你的样，测试和生产环境之间存在巨大差异。

- 就像我们在不感知 ACL 的文件系统上一样，Samba 使用“获取所有权”（o）位报告为无权限（即 `--`），它看起来像是 0 位。这仅仅是报告权限的约定，并不会赋予指定用户任何额外的访问权限。
- `rwx` 权限集被报告为等同于完全控制（ALL）访问权限。
- 登录域，用户应该能够在没有任何干预的情况下挂载主目录。
- 新服务器应该出现在网络中。
- 用户应该能够从 `[docs]` 共享打开文档并打印到 `[hp4]` 打印机。登录脚本窗口如图 14.8 所示，在以 `user1` 登录后显示——目前为止一切顺利。

## 图 14.8

以 `user1` 登录时运行的登录脚本。

![](img/e6dc042fe420c610acdd193e834a4772_281_0.png)

接下来我们浏览网络以确保新服务器显示符合预期。我们的测试结果如图 14.9 所示。

## 图 14.9

网络中我们的 Samba 服务器。

![](img/e6dc042fe420c610acdd193e834a4772_281_1.png)

最后，我们尝试用 `wordpad.exe` 打开 `\BEVELED\DOCS` 中的文本文件并打印（见图 14.10）。

# 替换 Windows NT 文件打印服务器——全面替换

## 图 14.10

将 `\BEVELED\DOCS` 中的文本打印到 `\BEVELED\HP4`。

![](img/e6dc042fe420c610acdd193e834a4772_282_0.png)

## 在 Samba 服务器上管理共享

当 Samba 服务器部署在由 Windows 客户端、服务器和管理员组成的环境中时，传统的以 Unix 为中心的 Samba 主机管理方式（如文本编辑器）可能会由于 Unix 工具与标准 Windows 管理工具之间的差异而引起某些担忧。Unix 管理员开发的工具对 Samba 的需求更灵活，但也有必要支持原生的 NT 工具（如服务器管理器或 Microsoft 管理控制台 `MMC`），以便与其他服务器集成。

允许 NT 管理员创建、修改和删除文件共享的工具可以每天使用。我们已经在第 9 章涵盖的 Windows NT 添加打印机向导中看到了这种先例。

Samba 提供了三个全局 `smb.conf` 参数来通过 MS-RPC 函数修改 `smb.conf`。这些是：

- `add share command`
- `change share command`
- `delete share command`

每个参数都接受程序或脚本名称，该程序应修改 `smb.conf` 以反映请求的更改。为了执行任何这些命令，`smbd` 要求请求更改的用户以 `root` 账户连接。在这种情况下，作为“域管理员”组的成员是不够的。一种常见的

执行此操作是为了在使用管理工具连接服务器之前，先连接到 `\server\ipc$` 共享。

```
C:\WINNT\ net use \beveled\ipc$ /user:root
```

请记住，作为成员服务器，`smbd` 将首先要求一个域控制器（DC）对用户进行验证。如果验证失败，`smbd` 将尝试在本地 `smbpasswd` 文件中查找该用户。第 7 小时“安全值与密码”涵盖了在使用加密密码时如何将用户添加到 Samba 的 `smbpasswd` 文件中。如果你需要复习如何将 `root` 添加到 `smbpasswd` 文件，请参考该部分。

`add share` 命令和 `change share` 命令脚本各会传递以下参数：

- 当前 `smb.conf` 的绝对路径
- 所涉及的共享名称
- 磁盘上现有目录的绝对路径，该目录将作为共享的根目录
- 共享的注释

`delete share` 命令只需要两个参数：

- 当前 `smb.conf` 的绝对路径
- 所涉及的共享名称

Samba 2.2.2 包含一个编写好的 Perl 脚本，用于说明一个最小化共享脚本将如何工作。该脚本 `modify_samba_config.pl` 存储在 Samba 源码包 `examples/misc/` 目录下。我们将将其添加到 `smb.conf` 中：

```
# 为响应服务器管理器/MMC 提供支持
add share command = /usr/local/samba/lib/modify_samba_config.pl
delete share command = /usr/local/samba/lib/modify_samba_config.pl
change share command = /usr/local/samba/lib/modify_samba_config.pl
```

在测试此配置之前，我们将通过向 `smbd` 发送挂起信号 `-SIGHUP <pid>` 来指示它如何重新读取配置文件。
