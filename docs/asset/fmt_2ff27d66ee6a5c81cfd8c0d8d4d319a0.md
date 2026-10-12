
Host: `10.11.10.4:1234`

User-Agent: `Mozilla/5.0`

Connection: `close`

[POST request 1/]

`POST /index.php HTTP/1.1`

Host: `10.11.10.4:1234`

```
图 306：在 Wireshark 中插入 HTTP 封装的流量
```

### 20.5.1 练习题

1. 以学生账户连接到你的专用 Linux 实验室，运行 `rdesktop` 并以 `root` 身份运行 `/root/port_forwarding_and_tunneling/http_tunnel.sh`。
2. 启动 `apache2` 服务器并利用托管在 `443` 端口的漏洞 Web 应用（在之前的模块中介绍过）来获取反向 HTTP Shell。
3. 使用你的专用客户端重现演示的场景。

### 20.6 总结

在本模块中，我们涵盖了端口转发和隧道技术的概念。该模块包含了在 Windows 和 NIX 操作系统上应用这些技术的工具，这允许我们绕过出站规则以及深度包检测。

## 活动目录 (Active Directory) 攻击

Microsoft Active Directory 服务（通常称为 Active Directory，简称 AD）是一项允许系统管理员在大范围内更新和管理操作系统、应用程序、用户和数据访问的服务。由于 Active Directory 是一个非常复杂且细粒粒度的管理层，它构成了一个非常大的攻击面，并值得关注。

在本模块中，我们将介绍 Active Directory 并演示枚举、身份验证和横向移动技术。

### 21.1 活动目录理论

让我们从简要概述 Active Directory 的概念和术语开始，在进入枚举和利用之前打下基础。

Active Directory 由多个组件组成。最重要的组件是域控制器（DC），它是一个安装了 Active Directory 域服务的 Windows 2000-2019 服务器。域控制器是 Active Directory 的中心和核心，因为它存储了关于特定 Active Directory 实例配置的所有信息。它执行大量的规则，规定了 Windows 域内的对象如何相互作用，以及终端用户可以使用哪些工具。Active Directory 的强大和复杂性基于于网络管理员可用的惊人细粒度控制。

> 有三个不同版本的 Windows Server 操作系统。第一个是原始的“桌面体验”版本。随 Windows Server 2008 R2 引入的 Server Core 是一个没有专用图形界面的精简服务器。最新版本 Server Nano 是 Windows Server 2016 中引入的，它比 Server Core 还要精简。标准的“桌面体验”版和 Server Core 版本可以作为域控制器。Nano 版本无法编辑

当配置 Active Directory 时，会创建一个名为 `corp.where` 的域，其中 `corp` 是组织的名称。在该域内，你可以添加各种类型的对象，包括计算机对象和用户对象。

系统管理员（几乎总是）借助组织单位（OU）的帮助来组织这些对象。OU 类似于文件文件夹，它们是用于存储和分组其他对象的容器。计算机对象代表实际的用户和工作站

⁶⁰ (Microsoft, 2017), https://docs.microsoft.com/en-us/windows-server/identity/ad-ds/get-started/virtual-dc/active-directory-domain-services-overview
⁶¹ (Microsoft, 2014), https://technet.microsoft.com/library/ct86438?vs=10).aspx
⁶² (Microsoft, 2008), https://msdn.microsoft.com/library/ee391626v?vs=85).aspx
⁶³ (Microsoft, 2017), https://docs.microsoft.com/en-us/windows-server/get-started/getting-starting-with-nano-server
⁶⁴ (Microsoft, 2018), https://technet.microsoft.com/library/ct9803.aspx

# 攻击性安全

Active Directory 对象随类型而异，可以被视为域的成员。例如，用户、组和打印机。将使用 Active Directory 相关的技术进行枚举和利用。在现实世界的场景中，可以使用之前模块中概述的许多 Windows 枚举技术。

但在本模块中，我们将专注于专门为 AD 设计的技术。我们假设已经获取了 Windows 10 工作站的访问权限，并假设已经攻破 Offsec 域用户，该用户是本地管理员组的成员。

我们在该场景中的第一个目标是枚举域用户并尽可能了解他们的组组成。为了实现这一点，我们将利用多种工具和技术，这些可以在没有任何管理员权限的情况下执行。

### 21.2 活动目录枚举

攻击通常从枚举开始。一旦建立了立脚点，目标就是枚举域用户和组组成。

### 21.2.1 传统方法

第一种技术（我们称为“传统”方法）利用内置的 `net.exe` 程序。具体来说，我们将使用 `net user` 子命令，它可以枚举所有本地账户。

```
C:\Users\offsec.corp net user
```

CLIENT251 的用户账户

| admin Administrator | DefaultAccount |
| Guest student | WDAGUtilityAccount |
| 命令成功完成。 |

添加 `/domain` 标志将枚举整个域的所有用户：

```
C:\Users\Offsec.corp net user /domain
```

请求将在 `corp.com` 域控制器处处理。

DC01.corp.com 的用户账户

| admin Administrator | DefaultAccount |
| Guest iis_service | jeff_admin |

# 攻击性安全

使用 Kali Linux 2.0 进行渗透测试

```
krbtgt sql_service

命令成功完成。
```

> 列表 662 - 运行 `net user domain` 命令

在生产环境中运行此命令可能会返回一个长得多的用户列表。有了这个列表，我们现在可以查询有关单个用户的信息。

根据上面的输出，我们应该查询 `jeff_admin` 用户，因为这个名字听起来很有戏。

> 我们过去的经验表明，管理员往往倾向于在用户名上添加前缀或后缀，以根据其功能识别账户。

```
C:\Users\Offsec.corp> net user jeff_admin /domain

请求将在域 corp.com 的域控制器上处理。
```

用户名 `jeff_admin`
全名 `Jeff_Admin`
注释
用户的注释
国家/区域代码 000（系统默认）
账户活动：是
账户过期：永不期
密码最后设置于 2018/2/19 下午 1:56:22
密码过期：永不期
密码可更改：2018/2/19 下午 1:56:22
密码需要：是
用户可以更改密码：是

允许的工作站：所有
登录脚本
用户配置文件
主目录
最后登录：从未登录

允许的登录时间：所有

本地组组成
组组成：*Domain Users *Domain Admins
命令成功完成。

> 列表 663 - 针对特定用户运行 `net user`

输出表明 `jeff_admin` 是 `Domain Admins` 组的成员，因此我们将尽力记住这一点。

为了列出域中的所有组，我们可以向 `net group` 命令提供 `/domain` 参数^467。

# 使用 Kali Linux 2.0 进行渗透测试

```
C:\Users\offsec.corp net group /domain

请求将在域 corp.com 的域控制器上处理。
```
