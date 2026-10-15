
**图 4.36** 你只需输入“`sales`”即可创建虚假的“节点”，例如 `Sales`。然后输入反斜杠（\）和你想给共享命名的名称。这与底层的共享名称没有任何关系。

“链接名称”字段，你在此输入 `SalesWin1` 并让用户看到。在“指向目标的路径)”字段中，如图 4.36 所示输入 `\windcl.ad.corp.com\WinShare1`。

### 图 4.37 DFS 管理器帮助你构建 DFS，以便你为共享内容提供统一的视图（如其他窗口所示）。

![](img/1bd448c8019d74f469e5d7e3f033d752_284_0.png)

最棒的部分是，底层 NTFS 权限（Windows）和 POSIX 权限（Linux）会将那些不应该访问的人排除在外。这是统一权限并让他们轻松找到对他们重要的内容的极佳方法。

关于 Windows DFS 的更多信息，请查看以下内容：

- www.microsoft.com/windows2000/techinfo/howitworks/fileprint/dffsnew.asp
- www.microsoft.com/windows2000/techinfo/planning/fileprint/dfsssteps.asp
- www.microsoft.com/windowsserver2003/technologies/fileprint/file/dfs/default.mspx

再次，DFS 还有许多其他功能（例如复制服务），我们在这里没有进行探讨。有关 Samba 提供的 DFS 服务的更多信息，请查看：http://us2.samba.org/samba/docs/man/Samba-HOWTO-Collection/SambaHA.html

## 结语

让 Linux 和 Windows 共享文件确实是一项挑战。正如我们所探索的，Linux 阵营正在努力让 Linux 与 Windows 的兼容性更高。理想情况下，所有文件服务（特别是针对 Samba）将实现内核化（Kernelization）。这样，使用 Active Directory 域账户登录 Linux 机器的用户将与整个域内现有的 Windows 文件服务器实现 100% 的无缝集成，只需登录一次。

# 第 4 章 · Windows 与 Linux 之间的文件共享

截至今天，这还没有实现。目前，Linux 和 Windows 之间的文件共享确实可行，但在 Linux 客户端上实现真正单点登录的潜力很大程度上尚未实现。冗余的密码提示随处可见，且目前的“密钥环”（keyring）功能只是治标不治本。Kerberos 化是未来的趋势。

我并不是说我们应该放弃希望。关于 Kerberos 和互操作性，有许多额外的资源可以查阅。而且，当构建 Fedora 桌面时，GNOME 桌面的最新开发版本已经支持了它。

![](img/1bd448c8019d74f469e5d7e3f033d752_285_0.png)

我们已经在过去的几个章节中已经了 Kerberos。在书的现在，我们将结束对 Kerberos 的介绍。以下是关于 Kerberos 互操作性潜力的一些建议阅读方向，我们之前没能深入探讨。

**Windows 2000 Kerberos 认证** 该文档介绍了 Kerberos 如何在 Windows 2000（以及一般的 Active Directory）上实现。这些材料对于 Windows 2003 同样适用。可以在 www.microsoft.com/windows2000/techinfo/howitworks/security/kerberos.asp 找到该文档。

**Windows 2000 Kerberos 互操作性和 Kerberos 5 逐步指南** (krb5 1.0) 这些文档真正向你展示了如何与现有的 Kerberos 域执行跨域兼容。请从 www.microsoft.com/windows2000/techinfo/howitworks/security/kerbint.asp 开始，继续阅读到 www.microsoft.com/windows2000/techinfo/planning/security/kerbsteps.asp。

**使用 Kerberos 和 LDAP 进行集中化用户管理** 如果你计划使用 LDAP 作为账户仓库，并想对如何对其 Kerberos 化获得第二意见，可以在 www.samag.com/documents/s=9494/sam0502a.htm 看到这篇文章。

# 第 5 章 · Windows 与 Linux 之间的打印机共享

啊，打印机。它们是企业中不可避免的恶。它们消耗纸张、碳粉、时间和耐心。而且通常我们的企业都有很多打印机。也许如果我们少一点会更好？或者，如果不减少数量，我们至少可以在现有的打印机上进行更多的打印。

这就是本章的主题。即你可以利用现有的 Linux 或 Windows 打印机投资并进行共享。

然后有趣的事情就开始了。

与之前的章节一样，我们将首先通过让 Windows 客户端连接 Windows 服务器上的打印机，让 Linux 客户端连接 Linux 服务器上的打印机，来确保设置好并正常运行。在图 5.1 中，你可以看到我们的预期设计。也就是说，我们希望让 Windows-2003 服务器托管一台打印机，同时也让我们的 Linux 服务器托管一台打印机。然后，我们希望 Windows 和 Linux 客户端能够向我们想要的任何打印机打印。

## 利用 Windows 打印机

多年来，设置 Windows 打印机变得越来越简单。在我们的示例中，我们将物理上将打印机连接到 Windows 服务器上。此外，你可能还有其他选项，例如通过 HP Jetdirect 或类似的打印服务器设备实现“网络化”的打印机。我们无法涵盖所有的潜在选项——打印机制造商太多了，每个人都有自己的做法。然而，我们将尝试向你展示在查阅打印机及其配套网络设备说明书时，如何为这些情况做好准备。

## 设置打印机

多年来，设置 Windows 打印机变得越来越简单。在我们的示例中，我们将物理上将打印机连接到 Windows 服务器上。此外，你可能还有其他选项，例如通过 HP Jetdirect 或类似的打印服务器设备实现“网络化”的打印机。我们无法涵盖所有的潜在选项——打印机制造商太多了，每个人都有自己的做法。然而，我们将尝试向你展示在查阅打印机及其网络设备说明书时，如何为这些情况做好准备。

### 图 5.1 预期设计。也就是说，我们希望让 Windows-2003 服务器托管一台打印机，同时也让我们的 Linux 服务器托管一台打印机。然后，我们希望 Windows 和 Linux 客户端能够向我们想要的任何打印机打印。

## 加载 Windows 驱动程序

多年来，设置 Windows 打印机变得越来越简单。在我们的示例中，我们将物理上将打印机连接到 Windows 服务器上。此外，你可能还有其他选项，例如通过 HP Jetdirect 或类似的打印服务器设备实现“网络化”的打印机。我们无法涵盖所有的潜在选项——打印机制造商太多了，每个人都有自己的做法。然而，我们将尝试向你展示在查阅打印机及其网络设备说明书时，如何为这些情况做好准备。

## Windows 域打印 (IPP)

Windows 和 Linux 共享一种现代向客户端提供打印服务的方式。这是一种被称为 IPP（互联网打印协议）的标准，它在 RFC 2910 的互联网打印协议中有记录。其理念是如果你知道一个网络地址（例如 `http://<something>`），你就可以向打印机打印。RFC 2910 规定打印流量将通过端口 631 传输（而不是 http 的标准端口 80）。

Windows 中所有涉及 http 的内容意味着需要配置 Windows IIS。在安装时，我们建议您在 Windows 服务器上安装 IIS，因此您到这里时应该已经做好了准备。如果你还没有加载 IIS，现在就必须加载它了。再次强调，IIS 是可选的，但非常有用，我们将对其进行设置，以便我们的 Windows 和 Linux 客户端能够知道打印机的 Web 地址并能够正常运行。

然而，诀窍在于：Windows 并不称其为 IPP，它们有自己的名称：Windows 打印网络打印（Windows Internet Printing）。此外，微软的 Windows 打印网络打印并不使用标准的 631 端口——它使用普通的 80 端口。根据微软的说法，这是因为原始的 RFC 没有指定端口，而微软正是据此编写的。现在 RFC 指定了 631 端口，但微软已经决定使用 80 端口。这并不是问题，但如果微软能让 Windows 打印网络打印完全支持 RFC 标准，那就更好了。他们并没有这样做。因此，在我们的旅程中，我们将告诉 Linux 客户端如何通过 80 端口使用 Windows 打印网络，这样 Windows 服务器就能接收到流量、运行并开始打印。

让我们现在配置它。

## 安装 IIS 和 Internet 打印（如果之前未执行）
