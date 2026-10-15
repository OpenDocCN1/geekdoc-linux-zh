
Printer name `queue3` is valid.

```
[printers]
```
共享使用任何普通打印机服务可用的参数。我们可以通过更改现有打印机共享的名称，使打印 `cap` 文件中的所有打印机都对用户可用：

```
[printers]

printing = bsd

comment = My printer

path = /var/spool/print

print command = /usr/bin/lpr -p %q -d %s

error command = /usr/bin/lrm -p %q -d %s

success command = /usr/bin/lpok -p %q -d %s

fail command = /usr/bin/lrm -p %q -d %s
```

当用户尝试连接到 `\\server\queue2` 时，Samba 会创建一个 `[printers]` 服务的副本并重命名为找到的打印机名称：

```
[queue2]

printing = bsd

comment = My printer

path = /var/spool/print

print command = /usr/bin/lpr -p %q -d %s

error command = /usr/bin/lrm -p %q -d %s

success command = /usr/bin/lpok -p %q -d %s

fail command = /usr/bin/lrm -p %q -d %s
```

通过这种方式，打印变量（如 `%p`）会被扩展。服务器的打印系统负责处理发送作业到打印机的细节。这种行为由 `load printers` 参数控制，在某些环境下有充分禁用它的理由。如果 `printcap` 文件包含大量打印机（约 200 个），每个 `smbd` 进程的内存占用将会增加。这对于你的服务器是否是一个问题可以通过 `top` 和 `ps` 等工具轻松判断。

如果定义了 `[printers]` 服务，`smbd` 会在启动时为所有已知打印机创建共享，而不是按需创建。如图 9.13 所示。

图 9.13
在主机共享列表中包含所有已知打印机

![](img/e6dc042fe420c610acdd193e834a4772_170_png)

# 打印机共享的安全

许多管理员倾向于让任何想要向队列提交作业的用户访问打印机。从历史上看，LPD 等打印系统没有按用户执行访问控制的方法。然而，Windows NT 一直对打印机和文件提供细粒度的访问控制。Samba 提供了在上一节配置文件共享时所需的访问参数灵活性；Samba 打印机可以对网络上的所有用户可用，无论客户端是否经过身份验证。然而，如果打印机对于谁能发送作业有更严格的控制（例如负责公司工资的打印机），Samba 提供了两个级别的安全检查。

第一级控制应用于客户端首次尝试连接打印机时。Samba 执行与上一节表 8.6 所示的限制访问参数。打印机和文件共享相同的有效用户列表。

第二级访问检查在客户端尝试以某种方式操作打印队列时（例如提交作业或从队列中删除作业）进行。Samba 2.2 包含了为打印机分配 Windows NT 风格 ACL 的功能，并将这些设置存储在本地数据库中。这与第 8 节中描述的文件共享 ACL 方法相同。图 9.14 显示了名为 `hp-print` 的 Samba 打印机的安全对话框。

图 9.14
从 Windows NT 4.0 客户端查看 `hp-print` 的 ACL

![](img/e6dc042fe420c610acdd193e834a4772_171_0.png)

## Samba—打印服务器

有关文件和打印机上的 Windows NT ACL 的更多信息，请参阅 Windows NT Resource Kit 或其他涵盖 Windows/2000 安全性的书籍。

## 排除打印共享故障

当打印服务运行不顺利预期时，我们将通过一些基础步骤排除故障来结束本节。最令人沮丧的问题之一是 Windows 用户打印了一个文件但它直接消失了。打印机本身没有生成任何内容。当发生这种情况时，第一步是验证用户是否可以从服务器的所有地方打印到打印机。如果目标打印机名为 `queue` 且用户无法从其 Windows 客户端打印，请先使用 `su` 命令以该用户的身份登录服务器。

```
root# /bin/su -y
```

```
$ /usr/bin/lpr -Pqueue1 /etc/hosts
```

如果打印失败，请遵循您的服务器操作系统和打印机的文档来确定原因。如果成功打印了测试页，请继续验证两个步骤。

接下来，我们将确保 Windows 客户端缓存的打印作业具有正确的格式。这是通过在溢流目录（spool directory）中捕获文件而不实际将其发送到打印机来实现的。实现此点的最简单方法是临时更改共享的打印命令

```
print command = echo % >> /tmp/%S.log
```

这会维护一个溢流作业名称的日志，可以使用文本编辑器检查实际文件。请记住，除非接到指示，否则打印命令不会删除溢流作业。我们的调试（debug）打印命令允许我们在不对 Windows 客户端进行任何更改的情况下捕获这些作业。

如果您发现 Windows 未能将作业传输到服务器，请验证客户端未将打印机标记为离线，这会导致其显示为灰色图标（图 9.15）。如果是如此，最好清除 Windows 系统上的本地打印队列，将打印机标记为在线，并重启客户端。如果操作系统继续自动将打印机标记为离线，请按照第 13 小节“故障排除技术”中概述的技巧进行，以确保 Windows 客户端和 Samba 服务器之间能够正常通信。

第 9 小节

## 图 9.15

![](img/e6dc042fe420c610acdd193e834a4772_173_0.png)

Windows 98 客户端上禁用的网络打印机。

假设客户端将文件缓存到 Samba 服务器，请尝试使用与原始打印命令相同的语法以用户身份打印该文件（但不要删除文件）。如果打印机将连接映射到游客账户（例如，`guest only = yes`），请确保指定的游客账户有效并可以向打印机发送文件。查找以下项目：

- 客户端安装的打印驱动程序与分配给队列的机型号不匹配
- 打印机的硬件限制（例如内存不足），会导致其无法处理文件

尽管无法列出管理打印机时可能出现的每种困难，但本节涵盖的步骤将帮助您诊断 80–90% 的常见问题。

### 总结

Samba 2.2 对 Samba 支持 Windows 客户端共享打印机（特别是 Windows NT/2000 客户端）进行了重大升级。向用户导出打印机的基本步骤为：

- 在 `smb.conf` 中定义打印共享。
- 在 Samba 主机上为客户端安装必要的打印机驱动程序。
- 在 Windows 主机上安装打印机。

通过使用特殊的 `[printers]` 共享，可以一次完成系统中所有已知打印机的第 1 步。

Samba 2.2 还引入使用原生 Windows NT 打印机管理工具（如添加打印机向导）在系统中添加和删除打印机的功能。在第 14 小节“替换 Windows NT 文件和打印服务器——全面”中，我们将讨论更多的 `smb.conf` hook，允许使用其他原生 NT 工具管理 Samba。

## Samba—打印服务器 159

### 问答

- Q 我的用户正在向 PostScript 打印机打印，但打印的是 PostScript 代码而不是实际页面。我该如何修复？
- A 许多 Unix 系统都有 PostScript 打印机过滤器，可以将文本文件转换为 PostScript（例如 `enscript`）。该过滤器足够智能，可以让 PostScript 不变以便正确打印。然而，Windows 打印机驱动程序会在文件开头放置 `Ctrl-D (^D)`。这会混淆通常在寻找 `!` 的过滤器，导致打印作业中的 PostScript 被转换成 PostScript，您会得到一大页的垃圾内容。您可以通过在打印共享中添加参数 `postscript = yes` 来修复此。

- Q 我有一台 System V 机器。我如何告诉 Samba 我服务器上所有的打印队列，以便客户端可以浏览它们？
- A 在这里，您应该确保 `smbd` 使用 `printcap name = l1stat`。这是 Solaris 等系统的默认值。然而，如果在 `smb.conf` 中手动将 `printcap name` 设置为其他值，`smbd` 将无法自动确定可用打印机的完整列表。

- Q 我的客户端在尝试向我的 Samba 服务器打印时遇到“磁盘已满”的错误信息，但空间充足。问题在哪里？
- A 如果拒绝写入权限，`smbd` 将无法将溢流文件写入打印机 `path` 参数定义的目录中。如果溢流目录所在的磁盘已，也会发生这种情况。

# 用于 MS-DOS 的 Microsoft 网络客户端版本 3.0
