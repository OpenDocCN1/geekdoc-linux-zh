
## 表 1-7 网络打印服务

| 名称 | 支持情况（运行平台） |
|---|---|
| 通用互联网文件系统 (CIFS) | Linux, Windows 2000/XP/2002 |
| 打印机守护进程 (LPD); RFC 1154 | Linux, Windows 2000/XP/2002 |

我们将在后面的章节中讨论这两种选择的细节和权衡。再次，这些服务中的任何一个都能满足我们的需求。第14章“打印”将讨论网络打印。

## 防火墙服务

如今，互联网应该被视为一种带有风险副作用的有用连接介质。公司和组织需要隔离自己的网络免受来自互联网的入侵者的渗透，但同时又要让全部或部分员工访问互联网。这种隔离功能由防火墙提供。防火墙是一种桥接，根据描述合法数据包源、目的和应用程序的规则来过滤流量。关于防火墙技术的讨论，请参见第12章“安全”。Windows 2000 和 Linux 都支持防火墙（见表 1-8）。这两个系统都支持 NAT。

## 表 1-8 防火墙服务

| 名称 | 支持情况（运行平台） |
|---|---|
| IPChains（基于内核的防火墙） | Linux |
| BackOffice Site Server | Windows |

防火墙防止未经授权的流量在他们的内部网和互联网之间流动。NT 和 Windows 2000 的基础产品中都没有防火墙服务。Windows XP Professional 包含防火墙，Windows.NET Server 和 Advanced Server 将支持 IP 过滤。

## Web 服务器

Linux 和 Windows 操作系统都自带 Web 服务器（见表 1-9）。Windows 2000/XP/2002 为 Windows Professional（可选安装）、Server 和 Advanced Server 提供了互联网信息服务 (IIS)。大多数 Linux 发行版提供开源的 Apache Web 服务器。我们将在第19章“Web 服务器”中详细介绍 Web 服务器。

## 第1章 网络的规划与部署

## 表 1-9 Web 服务器

| 名称 | 支持情况（运行平台） |
|---|---|
| 互联网信息服务 (IIS) | Windows 2000/XP/2002 |
| Apache | Linux and Windows 2000/XP/2002 |

微软的 IIS 是一个高风险且高成本的选择。在过去的两年里，IIS 需要许多安全补丁。每个运行中的 IIS 服务器都必须安装每个补丁，且通常在每次安装后必须重启机器。如果配合 IIS 使用 Windows 安全功能，则需要按连接付费（客户端许可）。Windows 域安全意味着需要一个 Windows 域以及随之维护成本，Windows 域安全的复杂性促使我们为 Web 服务器选择更简单的解决方案：市场领先的 Web 服务器 Apache。

## 安全服务

这是一个棘手的领域。我们公司的人员大部分是软件开发人员，他们并不愿意将计算机的管理权交给 IT 组织。另一个复杂性在于，如果组织执行了某些策略，则开发环境必须频繁豁免。开发、测试和支持系统通常不受 IT 策略的限制，因为软件开发需要对计算机的安全模型具有管理级访问权限。管理级访问在 Linux 上翻译为“root”权限，在 Windows 上翻译为“administrator”权限。

全局登录是另一个敏感领域。Linux 和 Windows 在有限的连接环境中都支持全局登录。如果一个组织决定建立单点登录环境，那么它必须选择在处处部署单一的安全模型。我们组织的部署范围很小，因此 Windows 域或 NIS（网络信息系统）都可以满足我们的需求。

我们将有一个用于共享设施（文件和打印机）的全局安全数据库。否则，我们将允许个人根据需要进行临时共享。全局安全数据库将用于访问文件、源码树、打印机、营销和销售演示稿以及电子邮件。此类服务可以通过 Active Directory (AD)、Windows 域或 NIS 支持，如表 1-10 所示。对于 Windows 域，Samba 可以作为域控制器，消除为每个需要共享资源的临时客户端支付许可的费用。由于我们讨论的是大约 100 个客户端，微软许可的费用约为每个客户端 40 美元，折算在我们公司约为 4000 美元。我们将在第15章讨论 Samba 的细节和网络服务的选择。Windows 2000 域将在第2章“安装和配置 Windows”中讨论（参见 `http://www.microsoft.com/WINDOWS 2000/guide/server/pricing/pricingwindows.asp`）。

## 表 1-10 网络安全账户

| 名称 | 支持情况（运行平台） |
|---|---|
| 活动目录 (AD) | Windows |
| 网络信息服务 (NIS) | Linux, Windows |
| Windows NT 域 | Windows NT 4.0, Samba, Windows 2000/XP/2002 |

## 电子邮件

需要电子邮件和讨论/协作组件。Windows 和 Linux 都支持 SMTP 邮件服务器和客户端。任何一种操作系统都能满足我们的需求。Linux 的邮件选择比 Windows 多得多。我们只关注两个服务器和三个客户端。表 1-11 和 1-12 分别显示了我们作为电子邮件客户端和服务器的候选方案。

## 表 1-11 电子邮件客户端

| 邮件客户端 | 支持情况（运行平台） |
|---|---|
| Microsoft Outlook | Windows |
| Eudora | Windows and Linux |
| Netscape Mail Reader | Windows and Linux |

## 表 1-12 邮件服务器

| 邮件服务器 | 支持情况（运行平台） |
|---|---|
| Microsoft Exchange Server | Windows |
| sendmail | Linux |

# 安装与配置 Windows

## 本章内容

- Windows 域
- 安装 Windows 专业版
- 安装 Windows Server
- 创建域

本章介绍了安装 Windows 的机制。我们将介绍台式机系统和独立服务器，或者通过域提升过程进行介绍。我们对微软域的描述将仅限于足够创建一个域。关于微软域的进一步讨论将在第 11 章“企业域设计”中进行。我们还提到了断开域连接、移动域控制器（有时称为 DC）以及何时需要此类操作。最后，我们简要提到了一个并不显而易见的启用多处理器的方法。在本章以及第 3 章“安装与配置 Linux”中，我们将讨论在新的磁盘系统上安装操作系统的细节。我们不会进行过详细的描述，但会指出安装问题的相似之处。

出于多种原因，E-solutions 将不会部署 Windows 安全域。首先，开发人员在咨询和开发工作中不需要它。简单的 Linux 安全模型就能满足他们的需求，而无需域、树和森林的复杂性。公司规模较小。Windows 服务器许可费和客户端访问许可证（CAL）的额外费用将无法提供足够的功能回报。Windows 域不支持标准的 Internet 连接软件，即 Berkeley 互联网命名域（BIND）。Linux 自带 BIND 8.2 版本。基本上，为了减少复杂性、遵循行业标准并降低成本，更倾向于使用 BIND 的轻量级解决方案。

我们将使用第 1 章“网络规划与部署”中给出的员工列表，并使用表 1–3 所示的硬件清单。生产机是真实的运行机器。它们包括提供文件、打印和互联网网关服务的台式机系统和服务器系统。开发机用于软件开发和测试。它们可以配置为 Linux 或 Windows。通常，它们是支持双启动的。对于我们的目的，我们假设一次订单交付的系统足够大，支持 Linux 或 Windows、软件产品以及我们可能需要的服务。文件服务器将拥有额外的内存和磁盘。Linux 的系统要求很小，我们按照 Windows XP 的配置配置系统，其磁盘、CPU 和内存需求大于 Windows 2000。目前，Windows 2000 产品的系统要求可以在 `http://www.microsoft.com/windows2000/professional/evaluation/sysreqs/default.asp` 找到。

Windows XP 系统要求适用于一个满足 Windows 2000 要求且至少有 128 MB RAM 的系统（参见 `http://www.microsoft.com/windowsxp/ready/default.asp#ready`）。

记住，Windows XP 有个人版或专业版。NET 服务器的要求在本文编写时尚可用。请参考微软网站获取最新进展。我们所有的系统将超过当前的 Windows 2000 服务器要求：

- 133 MHz Pentium 兼容 CPU
- 256 MB 内存
- 2 GB 磁盘，至少有 1 GB 空闲空间
