
24. 移除启动盘后，将其取出，并在显示器选择屏幕（如图 C-23 所示）中选择你的显示器品牌和型号。如果自动检测到品牌和型号，它们会被选中，你只需点击`Next`继续。如果没有，请对同一制造商的显示器进行尝试，不要偏离太远；在 Linux 中错误的设置可能会物理损坏你的显示器。

# 附录 C 如何安装 Red Hat Linux 7.2 和 Apache Web 服务器

![](img/b5f7722b7c2983a215c7726aaada19f9_519_0.png)

图 C-25 完成屏幕

## 安装 APACHE WEB 服务器

为了按照第 9 章所讨论的 CGI 脚本开发和测试 Web 页面，你必须访问 `www.apache.org` 并安装最新版本的 Apache Web Server 软件。

Red Hat 包管理器文件（扩展名为 `.rpm`）是你的 Apache Web Server 软件安装的重要部分，用于管理你的 Apache 安装。Apache Web Server 软件的更新速度比 Red Hat 包管理器文件（`.rpm`）快。如果你尝试使用过时的 Red Hat 包管理器文件（`.rpm`），可能会出现崩溃和库依赖错误等不可预知的问题。如果你主要关注的是稳定性和一致性，最好等到你能够从 `www.apache.org` 或 Red Hat 网站获取当前的文件。

安装 Apache Web Server 软件：

- 1. 确保你已以 root 身份登录到工作站。
- 2. 将 Red Hat Linux 7.2 CD-ROM 1 插入 CD-ROM 驱动器。
- 3. 输入 `mount /mnt/cdrom` 并按 Enter 挂载 CD-ROM 驱动器。
- 4. 输入 `cd /mnt/cdrom/RedHat/RPMS` 并按 Enter。
- 5. 输入 `ls *.rpm` 并按 Enter。该命令的输出应该显示 `file-1.1.3-1.i386.rpm`，包含了 Apache 运行所需的库文件（类似于 Windows 中的 `.dll` 文件）。

![](img/b5f7722b7c2983a215c7726aaada19f9_519_1.png)

- 6. 输入 `rpm -ivh mm-1.1.3-1i386.rpm` 并按 Enter 安装包 `mm-1.1.3-1i386.rpm`。该命令只需要 `-i` 选项和文件名，但我们添加 `v` 和 `h` 以详细显示安装进度和其他信息。

`verbose`（详细）一词意味着提供比默认消息更多的信息。在这种情况下，它意味着哈号 `#` 标记安装进度，并且该包的可执行文件或主文件名会显示在屏幕上。
- 7. 现在输入 `ls apache*.rpm` 并按 Enter。命令的输出应该是两个文件名，格式为 `apache-X.X-X.i386.rpm` 和 `apacheconf-X.X-X.noarch.rpm`（其中 Xs 代表主版本、次版本和补丁版本的数字；注意，在你的 CD-ROM 上，`noarch.rpm` 可能是 `i386.rpm`）。文件名类似于：`apache-1.3-20.i386.rpm` 和 `apacheconf-0.8.1-1.noarch.rpm`。
- 8. 输入 `rpm -ivh apache-X.X-X.noarch.rpm`（Xs 是你在第 7 步命令结果看到的数字），并按 Enter。例如，如果你在输入第 7 步命令时看到 `apache-1.3-20-16.noarch.rpm`，则输入 `rpm -ivh apache-1.3-20-16.noarch.rpm` 并按 Enter。
- 9. 输入 `rpm -ivh apacheconf-X.X-X.noarch.rpm`（Xs 是你在第 7 步命令结果看到的数字）并按 Enter。例如，如果你在输入第 7 步命令时看到 `apacheconf-0.8.1-1.noarch.rpm`，则输入 `rpm -ivh apacheconf-0.8.1-1.noarch.rpm` 并按 Enter。
- 10. Apache 默认未设置为自动启动。要在现在不重启的情况下启动它，输入 `/etc/rc.d/init.d/httpd start` 并按 Enter。
- 11. 若要让 Apache 在每次机器重启时自动启动，输入 `ntsys` 并按 Enter。这会加载 `ntys` 程序，如图 C-26 所示。`ntys` 是一种基于菜单的简化方法，用于编辑复杂的系统初始化脚本。
- 12. 向滚动可用守护进程和服务的列表，直到找到 `httpd` 选择，并使用空格键在括号 `[*]` 中放置星号。这意味着系统每次在此运行级别下启动时，都会启动该服务。
- 13. 按 Tab 键将焦点移动到 OK 按钮，然后按 Enter 保存更改并退出 `ntsys` 程序。

# 附录 C 如何安装 Red Hat Linux 7.2 和 Apache Web 服务器

![](img/b5f7722b7c2983a215c7726aaada19f9_521_0.png)

图 C-26 服务屏幕

> 在步骤 11-13 中，你将 Apache 设置为仅在特定的运行级别下启动。如果你将来希望 Apache 在不同的运行级别下启动，你可能需要在该运行级别下使用 `ntsys` 程序。你将需要完全按照上述步骤 11-13 的操作重复你的动作。
>
> 你可以指定运行级别，并使用 `ntsys` 命令编辑。例如，在运行级别 3 下，你可以输入 `ntsys` 来查看信息。你也可以输入 `ntsys 5` 来更改运行级别。

## 附录 D

# UNIX 变体

UNIX 变体仅仅是不同计算机上的发行版本。根据 UNIX 社区管理员的说法，有许多 UNIX 变体。本附录并不尝试列出所有变体，而是关注一些最流行的。

UNIX 衍生出许多变体的原因之一是其操作系统内核和 TCP/IP（传输控制协议/互联网协议）在 20 世纪 80 年代广泛使用。导致 UNIX 演变为许多变体的第三个原因是其源代码是公开的，使得供应商更容易适配 UNIX 系统。

## 流行的 UNIX 版本

大多数 UNIX 版本遵循一种（或组合）两种标准：伯克利发行版（BSD）标准和 System V 4（SVR4）标准。

BSD 标准源于加利福尼亚大学伯克利分校教授和学生的努力。该小组开发了 BSD 3 版本，然后是 BSD 4 版本。在 20 世纪 90 年代，他们的工作演变成了商业。你在本文中学到的 UNIX 的两个流行功能——`vi` 编辑器和 C Shell——源于 UNIX。

System V 的根源在于 AT&T 实验室的工作。从 20 世纪 70 年代到 80 年代末，实验室开发了 System V。最终，这个版本的 UNIX 由 AT&T 的子公司 UNIX Laboratories 接管。在 20 世纪 90 年代初，UNIX Laboratories 与 Novell 合作将 UNIX 版本移植到 Intel 处理器上。UNIX 不仅通过他们的工作到了流行的 PC，还引发了名为 UNIX Desktop 的图形用户界面。不久后，90 年代，Novell 决定减少其 UNIX 业务，并将其出售给名为 Santa Cruz Operation (SCO) 的公司，该公司现在提供名为 UnixWare 的 System V 商业产品。

今天，许多计算机和操作系统供应商提供商业 UNIX 发行版。此外，独立小组提供免费 UNIX 系统。表 D-1 列出了一些商业系统，表 D-2 列出了一些免费系统。

# 表 D-1 流行的商业 UNIX 变体

| 版本 | 制造商 | 来源 | 网络信息 |
| --- | --- | --- | --- |
| AIX | IBM | SVR4 和 BSD 的结合 | www.ibm.org 或 www-1.ibm.com/servers/aix |
| Digital Equipment UNIX（以前称为 Unix） | Compaq（本文编写时正在被惠普收购） | BSD | www.compa.com 或 www.tru64unix.compa.com |
| Hewlett Packard UNIX (HP-UX) | 惠普 | SVR4 | www.hp.com |
| Irix | Silicon Graphics | SVR4 | www.sgi.com |
| Mac OS X | Apple | BSD | www.apple.com |
| Red Hat | Red Hat | SVR4 | www.redhat.com |
| OSF1 | Compaq（本文编写时正在被惠普收购） | SVR4 | www.compa.com 或 www.tru64unix.compa.com |

## 流行的 UNIX 版本

## 表 D-1 常见的商业 UNIX 变体（续）

| 版本 | 制造商 | 起源 | 网上信息 |
|---|---|---|---|
