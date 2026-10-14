
可能用于 Solaris 的 `PC Netlink` 软件可能是提供的最大的互操作性创新。该软件使 Solaris SPARC 架构系统能够像 Windows NT4 服务器一样运行，并取代它们成为域控制器。`PC Netlink` 曾被称为 `Project Cascade`，它为 Windows NT 服务器带来了可靠性和可扩展性，这是 PC 环境中极力缺失的。

在办公网络中采用 Windows NT 平台标准的公司面临着适应指数级增长并仍提供可靠、可用的平台以交付客户所需服务的双重问题。`PC Netlink` 通过在基于 SPARC 架构的 Solaris 系统上运行 Windows 网络服务解决了这两个问题，这些系统提供高可用性且完全可扩展。`PC Netlink` 运行在全系列服务器上，从 `Ultra 5` 到 `Enterprise 10000`。

竭力控制 Windows NT 服务器泛滥的系统管理员可以用单个基于 Solaris 的 SPARC 服务器替换大量基于 PC 的服务器。这显著降低了维护和管理成本，因为 `PC Netlink` 服务器可以使用标准 Windows NT 工具进行管理，就像 PC 服务器一样一样；因此，不需要对现有的操作程序进行任何更改。

`PC Netlink` 软件提供以下原生服务：

- 主控制器和备用域控制器，NT 目录服务 (`NTDS`)
- 网络文件和打印服务
- 安全与身份验证
- 支持 NT 文件系统 (`CIFS/SMB`)
- Windows NT 命名服务
- 支持所有主要客户端类型 (Windows 2000、95、98、3.11 和 NT 工作站)
- 支持多达 2,000 个并发用户
- 符合服务包标准

## Windows Support（Windows 支持）

对 Windows 系列产品的支持仅包括客户端——例如原生 Windows 2000 环境。因此，不支持作为 Windows 2000 Server 的一部分引入的 Active Directory（活动目录）等功能。

图 10.1 显示了基于 SPARC 架构的 Solaris 服务器如何集成到办公室网络。

![](img/20459f772e7361286cec3e76e3bd26b4_228_0.png)

图 10.1 将 Windows NT 服务器整合到 Solaris 平台降低了总成本，简化了管理，并提供了一个完全可扩展且可靠的 NT 网络。

## 第10章 与 PC 的工作

尽管 `PC Netlink` 支持所有主要客户端，但实际上并不运行任何 Windows NT 应用程序，它可以存储并向客户端提供它们。这是因为实际应用程序运行在客户端本身上，而不是服务器上。

由于整合和总成本是 IT 领域非常受欢迎的目标，该产品提供了一个一次性实现这两个目标的切实机会。此外，它还增加了可靠性，并能够适应各地公司正在经历的增长因素。

## Totalnet Advanced Server（Totalnet 高级服务器）

`Totalnet Advanced Server` (`TAS`) 是 Syntax (`http://www.syntax.com`) 提供的一种互操作产品，允许不同的操作系统在局域和广域网上成功共享文件、打印和应用程序资源。

该软件运行在 Solaris 等 UNIX 环境中，并创建一个公共系统，使其能够作为 2000/NT/95/98、Network、Macintosh 以及其他 UNIX 变体的文件、打印和应用程序服务器。它允许用户在其原生环境中创建和存储文件，并充分利用例如 Solaris 系统的力量和可靠性。

`TAS` 实现了这些不同环境之间的互操作性，每个环境定义了特定的操作系统和传输组合：

- `CIFS` 域：运行 `NetBIOS` over `TCP/IP` 或 `NetBIOS` over `NetBEUI` 的 LAN Manager、Windows NT、Windows 2000、Windows 95/98 以及 IBM OS/2/2 客户端
- `NetWare` 域：运行 `IPX/SPX` 传输的 NetWare 客户端，支持 NETX/VLM、Windows 200、Windows 95/98、Windows NT 和 NetWare 客户端
- `AppleTalk` 域：运行 `AppleTalk` 或 `TCP/IP` 传输的 Macintosh 客户端

## Samba

`Samba` 免费适用于公有领域，可以从 Samba 网站（`http://www.samba.org`）或其它提供 Solaris 系统公有领域软件的网站（如 `http://www.sunfreeware.com`）下载。`Samba` 是免费的，并附带源代码。

`Samba` 运行在如 Solaris 等 UNIX 平台上，但它可以像原生系统一样与 Windows 客户端通信。运行 `Samba` 的 Solaris 系统被集成到 Windows 网络邻域中，为 Windows 客户端提供文件和打印服务，而这些客户端并不知道服务是由 Solaris 系统提供的——也就是说，这些服务对客户端来说是透明的。`Samba` 基于 `SMB` 协议和通用文件接口 (`CIFS`)。

在许多方面，`Samba` 的功能与 Solaris `PC Netlink` 相似，但 `Samba`（尚）无法完全模仿（甚至替换）Windows NT 域控制器——而 `PC Netlink` 可以做到这一点。

- 文件和打印——`Samba` 守护进程 (`smbd`) 管理这些设施，使 UNIX 系统看起来像是一台 PC 文件服务器。
- 身份验证与授权——由 `smbd` 守护进程还管理共享模式和用户模式的身份验证与授权。该功能允许对网络共享（如打印机）应用密码。根据模式不同，所有用户使用同一个密码（共享模式），或者用户拥有用户名和密码，由系统管理员进行单独管理。
- 名称解析——这可以有两种形式。在广播模式下，客户端广播系统的主机名并等待返回 IP 地址。广播名称解析局限于本地网络。第二种名称解析是点对点的，使用 `NetBIOS` 名称服务 (`NBNS`) 服务器。在此配置下，客户端将 `NetBIOS` 名称及其相应的 IP 地址发送到 `NBNS` 服务器，并将其存储在简单的数据库中。然后由服务器进行名称解析请求。存在一个 `nmblookup` 实用程序用于查询服务器。`NBNS` 与 `DNS` 非常相似，但安全性稍低，因为用于检查授权客户端的控制措施较少。
- 浏览——在此语境下，浏览与 Web 浏览不同。它是网络上计算机提供的文件和打印服务的一份“可浏览”列表。
- `Samba` 客户端——servlet 是一种 FTP 风格的接口，用于访问 PC 资源，例如来自打印机或 `NetBIOS` 系统的文件等。
- `tar`——`Samba` 客户端软件包含一个 `tar` 扩展，以便可以将 PC 系统备份到 Solaris 主机上。
- 管理工具——`Samba` 管理工具 (`SWAT`) 允许管理员使用 Web 浏览器远程配置 `Samba`。

`Samba` 用于集成和合并现有 Windows 网络和资源。这与 Solaris `PC Netlink` 不同，后者还可以替换 Windows NT 域控制器，尽管这是 Solaris 团队的最终目标。

## 适用于 Solaris 的 Citrix Metaframe

最近发布的适用于 UNIX 的 Citrix Metaframe 允许 Solaris 应用程序交付到几乎任何设备上。该软件支持基于 SPARC 平台的 Solaris 2.6，以及基于 SPARC 和 Intel 平台的 Solaris 7 和 8。该产品提供了应用程序到本地桌面的无缝集成，使用户能够调整窗口大小，并在本地和远程应用程序之间轻松切换，就像这些程序都运行在本地系统上一样。

当与适用于 Windows 的 Citrix Metaframe 配合使用，此版本的 Citrix Metaframe 可以交付几乎任何设备，包括但不限于 Windows 2000、9x、3.x 和 NT，以及 DOS、OS/2、Macintosh、无线设备和手持设备、终端和网络计算机。

对于使用多平台环境和各种设备的组织来说，另外一个非常有用的功能是 Metaframe 授予用户对本地资源（如剪贴板）的完全访问权限。这使得在本地应用程序和使用 Citrix 独立计算架构 (`ICA`) 部署的远程应用程序之间复制粘贴图形和文本变得简单。使用它，整个应用程序过程在服务器上执行，减少了带宽需求，并消除了其他终端仿真产品中存在的问题。

对于使用多平台环境和多种设备的组织，Citrix Metaframe 不仅为运行在强大且可靠的 Solaris 系统上的 UNIX 应用程序提供了更好的无缝体验，还提供了简化管理。这使得系统管理员能够充分利用 Solaris 的可扩展性、处理能力和可靠性，同时扩大了其潜在客户群。

## PC 连接产品

允许 PC 连接到运行不同操作系统的主机的产品已以多种形式存在多年。当同时需要 PC 和非 PC 连接时，Telnet 和 X 系统连接消除了在桌面上使用单独专用控制台或显示器的需求。

尽管这些产品不是上一节描述的那种全 PC 集成软件包，但它们仍然可以帮助系统管理员进行资源的合理化和整合，这在 IT 部门正变得日益流行。
