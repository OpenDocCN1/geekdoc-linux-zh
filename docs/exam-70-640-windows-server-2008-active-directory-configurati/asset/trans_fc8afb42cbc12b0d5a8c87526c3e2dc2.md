
## 使用 Active Directory 命名标准

Active Directory 的可扩展性和集成能力源于其对命名格式和目录功能所采用的行业标准，特别是 *轻量级目录访问协议（Lightweight Directory Access Protocol，LDAP）*。LDAP 于 20 世纪 90 年代初由互联网工程任务组（Internet Engineering Task Force，IETF）开发，旨在促进 X.500 在电子邮件中的实施。（X.500 是定义全球目录应如何构建和组织的标准。）

自 LDAP 引入以来，该协议已成为一个行业标准，实现了目录服务与应用之间的数据交换。LDAP 标准定义了 Active Directory 数据库中所有对象的命名，因此提供了一个可以与其他目录服务（如 Novell *eDirectory*）及支持 Active Directory 的应用（如 Microsoft Exchange）进行集成的目录。

对 Active Directory 对象的查询和修改几乎完全通过 LDAP 进行。因此，有必要了解 Active Directory 中对象的引用方式。请参阅图 1-2 中的示例。

![](img/a8ee53dbf1310726255b6fbb9f296fb2_50_0.png)

LDAP 使用对象的*可分辨名称（distinguished name，DN）*来引用对象，该名称使用完整的层级路径引用 Active Directory 数据库目录结构中的对象，从对象本身开始，包括所有父对象，直到域的根。LDAP 定义了标识对象名称各部分的命名属性。这些属性如表 1-1 所示。

**注意**

有关 LDAP 定义的对象的更多信息，请在 [www.rfc-editor.org/rfc-search.html](https://www.rfc-editor.org/rfc-search.html) 的 RFC 编辑器搜索页面中搜索 LDAP。

### 表 1-1
Active Directory 对象类和命名属性

| 对象类 | LDAP 命名属性 | 命名属性定义 |
| :--- | :--- | :--- |
| 用户或任何叶对象 | Cn | 通用名称 |
| 组织单元对象 | Ou | 组织单元名称 |
| 域 | Dc | 域组件，DNS 名称的每一部分对应一个 |

以图 1-2 作为参考，J.Smith 的**可分辨名称（distinguished name）**如下：

**cn=jSmith, ou=sales, dc=lucernepublishing, dc=com**

并非所有 Active Directory 管理工具都要求您指定对象的完整可分辨名称来管理该对象。在许多情况下，您可以指定简化的账户名称，如 “jsmith”。然而，了解可分辨名称的结构在这些需要它的时候非常重要。例如，您可能需要恢复一个从 Active Directory 数据库中意外删除的对象。在这种情况下，了解可分辨名称的结构对于完成所需的恢复操作至关重要。

除了理解 DNS 和 LDAP 在 Active Directory 名称格式中的意义外，理解 User Principal Name（UPN）在 Windows Server 2008 中的使用也很重要。UPN 遵循 *username@lucernepublishing.com* 的格式。这种约定为复杂的域结构提供了一种简单的解决方案，在这种结构中，用户可能难以记住可分辨名称。它还提供了在用户的电子邮件名称和其登录名称之间保持一致性的机会。

**参考**

有关执行 Active Directory 对象恢复的更多信息，请参阅第 11 课。

**参考**

有关 UPN 的更多信息，请参阅第 2 课。

## 理解 DNS

您经常会听到 Active Directory 管理员说“Active Directory 依靠 DNS 生存”。自从 Windows 2000 引入 Active Directory 以来，*域名系统（Domain Name System，DNS）*一直是 Active Directory 的默认名称解析方法。正确配置 DNS 是任何 Active Directory 管理员的关键任务，因为 Active Directory 环境的健康状况在很大程度上取决于 DNS 支持 Active Directory 的功能是否良好。

- 这四个八位组的 IP 地址是一个 IP 版本 4（IPv4）地址。这指的是 IP 的第 4 版，这是目前部署最广泛的 IP 版本。Windows Server 2008 和 Windows Vista 也原生支持 IPv6，这是下一代 IP。有关 IPv6 的更多详细信息，请参阅 MOAC 642 指南。

在大多数现代网络中，TCP/IP 是用于系统间通信的主要网络协议。IP 网络上的所有设备都使用唯一的数字来标识自己及其在网络上的位置。这被称为 IP 地址。IP 地址由四个八位组组成，通常以点分十进制表示，例如 192.168.10.1。

访问资源的一种方式是通过其 IP 地址。然而，当计算机系统使用 32 位数字来识别资源时，期望用户通过 IP 地址访问资源充其量是繁琐的。这就是 DNS 发挥作用的地方。DNS 是一种分布式名称解析服务，为 Active Directory 域提供名称解析。除了 IP 地址之外，所有计算机在安装时都被分配了一个 DNS 主机名。虽然主机名有助于定义设备的位置或用途，但它需要被翻译成计算机能理解的数值。这就是您需要 DNS 的原因。DNS 将计算机的主机名映射到其 IP 地址。当用户或应用程序引用计算机的主机名时，DNS 提供主机名到 IP 地址的转换，从而使流量能够被适当地路由到正确的目的地。

### 集成 DNS 和 Active Directory

DNS 是 Active Directory 的基础要求；除非服务器可以在同一台机器或网络上的某处找到合适的 DNS 服务器，否则无法在服务器上安装域控制器角色。

除了在网络中提供计算机主机名到 IP 地址的映射外，DNS 在 Active Directory 的功能中扮演着更重要的角色。Active Directory 依赖 DNS 为网络上的客户端提供定位服务。该定位服务为需要了解哪台服务器执行何种功能的客户端提供指导。例如，如果用户试图登录网络，定位服务将尝试向客户端提供位于与客户端工作站相同站点内的域控制器的名称和 IP 地址（如果可能的话）。

这个定位服务在 Active Directory 内是必要的，因为 Active Directory 是一个多主目录服务。因此，网络服务并不总是由同一台服务器提供。容错、负载平衡和冗余是即使在小网络中也设置多台服务器的原因之一，这使得该定位服务对于客户端能够访问域控制器和其他 Active Directory 资源至关重要。

- SRV 记录由 BIND DNS 4.9.7 及更高版本支持。动态更新由 BIND DNS 8.2.2 及更高版本支持。

在许多情况下，组织将依赖 Windows Server 2008 中内置的 DNS 服务器角色为 Active Directory 提供 DNS 名称解析。但在某些情况下，公司可能已经部署了第三方 DNS 服务，例如 UNIX 提供的 BIND DNS 服务。在使用第三方 DNS 部署 Active Directory 时，您需要确保 DNS 服务器能够支持 SRV 记录。SRV 记录是 DNS 中的定位记录，允许客户端定位 Active Directory 域控制器或全局目录。如果不能解析 SRV 记录，客户端将无法针对 Active Directory 进行身份验证。

除了必须支持 SRV 记录外，现代 DNS 实现还具备支持动态更新的能力。动态更新允许 DNS 客户端在 DNS 数据库中自动注册和更新其信息。例如，当向林中添加域控制器时，其 SRV 和 A 记录可以通过动态更新动态添加到 DNS 数据库，以保持 DNS 定位服务的最新状态。动态 DNS 提供了一种便捷的方法来协助保持数据库的更新。Active Directory 的运行不需要动态更新，但利用此功能可以大大简化管理。

## 使用林和域功能级别

林和域功能级别旨在支持运行各种受支持操作系统的 Active Directory 域控制器。当您停用旧版域控制器时，可以修改这些功能级别以暴露 Active Directory 中的新功能。例如，Active Directory 中的某些功能直到林中的所有域控制器都升级到 Windows Server 2003 系列后才可激活，而某些域范围的 Active Directory 功能只能存在于处于 Windows Server 2008 功能级别的域中。

随着企业扩展和更新其网络，它们通常不会同时升级整个网络。选择的升级策略将取决于网络的规模以及升级对用户生产力和网络访问的影响。因此，Microsoft 创建了功能级别，使企业能够基于对新功能的需求和愿望，逐步迁移其 Active Directory 域控制器。您可以在多域环境中更改单个域的功能级别，而无需其他域进行相同的更改。这允许*滚动升级*，以符合时间、预算和应用兼容性因素的要求。

请注意，林和域功能级别不会自动更改。例如，即使某个域中的所有域控制器都在运行 Windows Server 2008 操作系统，域功能级别也不会切换到 Windows Server 2008，直到管理员手动进行更改。这是因为功能级别的更改是*不可逆的*；一旦您升级了功能级别，除非对 Active Directory 数据库执行域或林范围的恢复，否则无法返回到以前的级别。由于这种更改的永久性，Active Directory 要求管理员手动干预以更改 Active Directory 环境的林或域功能级别。

## 提高域功能级别

Windows Server 2008 支持三种域功能级别，具体取决于部署在域中的域控制器的操作系统。当您提高域功能级别时，Active Directory 中将有额外的功能可用。

在 Active Directory 中，域功能级别是按域配置的。这允许林中的不同域处于向 Windows Server 2008 过渡过程的不同阶段——父域可以处于 Windows Server 2003 域功能级别，而子域已经提升到 Windows Server 2008 功能级别。Windows Server 2008 支持 Windows 2000、Windows Server 2003 和 Windows Server 2008 域控制器。Windows NT 4.0 域控制器*不再受支持*。

Windows Server 2008 中可用的以下域功能级别：

- **Windows 2000 原生。** 此级别允许与 Microsoft Windows 2000 向后兼容。它还允许 Windows 2000、Windows Server 2003 和 Windows Server 2008 域控制器。
- **Windows Server 2003。** 此功能级别仅允许 Windows Server 2003 和 Windows Server 2008 域控制器。它不允许存在 Windows 2000 域控制器。

