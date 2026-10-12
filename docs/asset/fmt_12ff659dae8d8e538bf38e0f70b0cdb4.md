
同样，`ps` 和 `ss` 命令显示 HTTPtunnel 客户端已启动并正在运行。

现在，所有发送到我们 Kali Linux 机器 TCP 端口 8080 的流量都将被重定向到我们的 HTTPtunnel（在那里它被 HTTP 封装，穿过防火墙发送到被入侵的 Linux 服务器并解封装），然后再次重定向到 Windows 服务器的远程桌面服务。

我们可以通过启动 Wireshark 嗅探流量并验证其确实被 HTTP 封装，然后在对我们 Kali Linux 机器的监听端口 8080 发起远程桌面连接之前来验证这是否正常工作：

![](img/ec25e59d75726b7041242a56d3376832_613_0.png)

*图 305：通过 HTTP 隧道在 Windows Server 2016 机器上进行 RDP 登录*

太好了！远程桌面连接成功了。

检查 Wireshark 中的流量，我们确认它确实被 HTTP 封装，并且可以绕过深度包内容检测设备。

![](img/ec25e59d75726b7041242a56d3376832_614_0.png)

*图 306：在 Wireshark 中检查 HTTP 封装的流量*

+   $ ^{596} $ (Sebastian Weber, 2010), http://http-tunnel.sourceforge.net/
+   $ ^{597} $ (Stunnel, 2019), https://www.stunnel.org/
+   $ ^{598} $ (Sebastian Weber, 2010), http://http-tunnel.sourceforge.net/

## 21. Active Directory 攻击

Microsoft Active Directory 域服务,<sup>600</sup>通常简称为 Active Directory (AD)，是一种允许系统管理员大规模更新和管理操作系统、应用程序、用户以及数据访问的服务。由于 Active Directory 可以是一个高度复杂且细粒度的管理层，它带来了巨大的攻击面，因此值得特别关注。

在本模块中，我们将介绍 Active Directory，并演示枚举、认证和横向移动技术。

### 21.1 Active Directory 理论

在我们进入枚举和利用之前，让我们先简要概述一下基本的 Active Directory 概念和术语，以此奠定基础。

Active Directory 由几个组件组成。最重要的组件是域控制器 (DC),<sup>601</sup>它是一个安装了 Active Directory 域服务角色的 Windows 2000-R2 服务器。域控制器是 Active Directory 的枢纽和核心，因为它存储了关于特定 Active Directory 实例如何配置的所有信息。它还执行各种各样的规则，这些规则规定了给定 Windows 域内的对象之间如何交互，以及终端用户可以使用哪些服务工具。Active Directory 的强大功能及其复杂性，建立在网络管理员可用的控制具有惊人的细粒度这一基础上。

> "Windows 服务器操作系统有三个不同的版本。第一个是原始的“桌面体验”版本。随着 Windows Server 2008 R2 引入的 Server Core,<sup>602</sup>是一种没有专用图形界面的最小化服务器安装。最近的版本是 Server Nano,<sup>603</sup>它是在 Windows Server 2016 中引入的，甚至比 Server Core 更加精简。标准的“桌面体验”版本和 Server Core 版本都可以作为域控制器运行。Nano 版本不可以。"

当配置 Active Directory 实例时，会创建一个域，名称类似于 corp.com，其中 corp 是组织的名称。在这个域内，我们可以添加各种类型的对象，包括计算机对象和用户对象。

系统管理员可以（并且几乎总是）借助组织单位 (OU) 来组织这些对象。<sup>604</sup>OU 类似于文件系统中的文件夹，它们是用于存储和分组其他对象的容器。计算机对象代表实际的服务器和工作站，这些设备是*加入域的*（属于该域的一部分），而用户对象代表组织中的员工。所有 AD 对象都包含属性，这些属性根据对象类型而异。例如，用户对象可能包含姓名、姓氏、用户名和密码等属性。

通常，内部网络上的客户端计算机连接到域控制器以及各种其他内部成员服务器，例如数据库服务器、文件存储服务器等。此外，许多组织通过连接到互联网的网络服务器提供内容，这些服务器有时也是内部域的成员。

> 需要注意的是，一些组织会有未加入域的机器。这对于面向互联网的机器来说尤其常见。

从技术上讲，Active Directory 可能令人生畏，因为它包含了许多我们无法在本模块中全面涵盖的概念和功能。相反，我们将介绍基本的 AD 术语和语言，以及构建我们的枚举和利用能力所需的额外知识。

> Active Directory 环境对域名系统 (DNS) 服务具有非常关键的依赖关系。因此，典型的 AD 域控制器通常也托管一个对于特定域具有权威性的 DNS 服务器。请注意，在实验室环境中，您还可能找到与 Active Directory 无关的 DNS 服务器，它们为其他计算机提供查询服务。

### 21.2 Active Directory 枚举

通常，针对 Active Directory 基础设施的攻击始于对域工作站或服务器成功利用或客户端侧攻击，随后是对 AD 环境的枚举。

> 一些渗透测试从假设的违规开始，其中客户端提供对工作站的初始访问权限。这节省了时间，加速了评估，并允许花费更多时间评估其余的内部基础设施，包括 Active Directory。

一旦我们建立了立足点，目标就是提升我们的权限级别，直到我们获得一个或多个域的控制权。有几种方法可以实现这一点。

在 AD 内部，管理员使用组来向成员用户分配权限，这意味着在我们的评估过程中，我们将瞄准高价值组。在这种情况下，我们可以破坏 *Domain Admins*（域管理员）组的一个成员，从而获得对域中每台计算机的完全控制。

获得域控制权的另一种方法是成功破坏域控制器，因为它可能被用于修改所有加入域的计算机或在它们上执行应用程序。此外，正如我们稍后将看到的，域控制器包含了每一个域用户帐户的所有密码哈希值。

在学习本模块的过程中，我们将通过一系列 AD 枚举和利用技术来演示典型的域入侵。在现实场景中，我们可以使用前面模块中概述的许多 Windows 枚举和利用技术。然而，在本模块中，我们将重点介绍专门设计用于枚举和利用 AD 用户和组的技术。

我们将基于以下假设：我们已经通过本课程之前介绍的技术获得了 Windows 10 工作站的访问权限。我们还将假设我们破坏了 *OffSec* 域用户，该用户也是加入域的工作站的本地管理员组的成员。这将使我们能够专注于 Active Directory 相关的枚举和利用技术。

在这个场景中，我们的第一个目标将是枚举域用户，并尽可能多地了解他们的组成员身份，以寻找高价值目标。为此，我们将利用几种工具和技术，其中许多可以在没有任何管理权限的情况下执行。

#### 21.2.1 传统方法

第一种技术，我们将其称为“传统”方法，利用了内置的 `net.exe`<sup>605</sup>应用程序。具体来说，我们将使用 `net user`<sup>606</sup>子命令，它枚举所有本地帐户。

```
C:\Users\Offsec.corp> net user

User accounts for \\CLIENT251

admin          Administrator       DefaultAccount

Guest          student             WDOGtU1ityAccount

The command completed successfully.
```

Listing 661 - 运行 `net user` 命令

添加 `/domain` 标志将枚举整个域中的所有用户：

```
C:\Users\Offsec.corp> net user /domain

The request will be processed at a domain controller for domain corp.com.

User accounts for \\DC01.corp.com

adam           Administrator      DefaultAccount

Guest          iis_service        jeff_admin

krbtgt              offsec              sql_service

The command completed successfully.
```
