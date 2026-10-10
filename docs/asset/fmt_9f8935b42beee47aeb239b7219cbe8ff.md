
访问资源的一种方式是通过其 IP 地址。然而，当计算机系统使用 32 位数字来识别资源时，期望用户通过 IP 地址访问资源充其量是繁琐的。这就是 `DNS` 发挥作用的地方。`DNS` 是一种分布式名称解析服务，为 `Active Directory` 域提供名称解析。除了 IP 地址之外，所有计算机在安装时都被分配了一个 `DNS` 主机名。虽然主机名有助于定义设备的位置或用途，但它需要被翻译成计算机能理解的数值。这就是您需要 `DNS` 的原因。`DNS` 将计算机的主机名映射到其 IP 地址。当用户或应用程序引用计算机的主机名时，`DNS` 提供主机名到 IP 地址的转换，从而使流量能够被适当地路由到正确的目的地。

### 集成 DNS 和 Active Directory

`DNS` 是 `Active Directory` 的基础要求；除非服务器可以在同一台机器或网络上的某处找到合适的 `DNS` 服务器，否则无法在服务器上安装域控制器角色。

除了在网络中提供计算机主机名到 IP 地址的映射外，`DNS` 在 `Active Directory` 的功能中扮演着更重要的角色。`Active Directory` 依赖 `DNS` 为网络上的客户端提供定位服务。该定位服务为需要了解哪台服务器执行何种功能的客户端提供指导。例如，如果用户试图登录网络，定位服务将尝试向客户端提供位于与客户端工作站相同站点内的域控制器的名称和 IP 地址（如果可能的话）。

这个定位服务在 `Active Directory` 内是必要的，因为 `Active Directory` 是一个多主目录服务。因此，网络服务并不总是由同一台服务器提供。容错、负载平衡和冗余是即使在小网络中也设置多台服务器的原因之一，这使得该定位服务对于客户端能够访问域控制器和其他 `Active Directory` 资源至关重要。

- `SRV` 记录由 `BIND DNS` 4.9.7 及更高版本支持。动态更新由 `BIND DNS` 8.2.2 及更高版本支持。

在许多情况下，组织将依赖 `Windows Server 2008` 中内置的 `DNS` 服务器角色为 `Active Directory` 提供 `DNS` 名称解析。但在某些情况下，公司可能已经部署了第三方 `DNS` 服务，例如 UNIX 提供的 `BIND DNS` 服务。在使用第三方 `DNS` 部署 `Active Directory` 时，您需要确保 `DNS` 服务器能够支持 `SRV` 记录。`SRV` 记录是 `DNS` 中的定位记录，允许客户端定位 `Active Directory` 域控制器或全局目录。如果不能解析 `SRV` 记录，客户端将无法针对 `Active Directory` 进行身份验证。

除了必须支持 `SRV` 记录外，现代 `DNS` 实现还具备支持动态更新的能力。动态更新允许 `DNS` 客户端在 `DNS` 数据库中自动注册和更新其信息。例如，当向林中添加域控制器时，其 `SRV` 和 `A` 记录可以通过动态更新动态添加到 `DNS` 数据库，以保持 `DNS` 定位服务的最新状态。动态 `DNS` 提供了一种便捷的方法来协助保持数据库的更新。`Active Directory` 的运行不需要动态更新，但利用此功能可以大大简化管理。

## 使用林和域功能级别

林和域功能级别旨在支持运行各种受支持操作系统的 `Active Directory` 域控制器。当您停用旧版域控制器时，可以修改这些功能级别以暴露 `Active Directory` 中的新功能。例如，`Active Directory` 中的某些功能直到林中的所有域控制器都升级到 `Windows Server 2003` 系列后才可激活，而某些域范围的 `Active Directory` 功能只能存在于处于 `Windows Server 2008` 功能级别的域中。

随着企业扩展和更新其网络，它们通常不会同时升级整个网络。选择的升级策略将取决于网络的规模以及升级对用户生产力和网络访问的影响。因此，Microsoft 创建了功能级别，使企业能够基于对新功能的需求和愿望，逐步迁移其 `Active Directory` 域控制器。您可以在多域环境中更改单个域的功能级别，而无需其他域进行相同的更改。这允许滚动升级，以符合时间、预算和应用兼容性因素的要求。

请注意，林和域功能级别不会自动更改。例如，即使某个域中的所有域控制器都在运行 `Windows Server 2008` 操作系统，域功能级别也不会切换到 `Windows Server 2008`，直到管理员手动进行更改。这是因为功能级别的更改是不可逆的；一旦您升级了功能级别，除非对 `Active Directory` 数据库执行域或林范围的恢复，否则无法返回到以前的级别。由于这种更改的永久性，`Active Directory` 要求管理员手动干预以更改 `Active Directory` 环境的林或域功能级别。

## 提高域功能级别

`Windows Server 2008` 支持三种域功能级别，具体取决于部署在域中的域控制器的操作系统。当您提高域功能级别时，`Active Directory` 中将有额外的功能可用。

在 `Active Directory` 中，域功能级别是按域配置的。这允许林中的不同域处于向 `Windows Server 2008` 过渡过程的不同阶段——父域可以处于 `Windows Server 2003` 域功能级别，而子域已经提升到 `Windows Server 2008` 功能级别。`Windows Server 2008` 支持 `Windows 2000`、`Windows Server 2003` 和 `Windows Server 2008` 域控制器。`Windows NT 4.0` 域控制器不再受支持。

`Windows Server 2008` 中可用的以下域功能级别：

- `Windows 2000 原生`。此级别允许与 Microsoft `Windows 2000` 向后兼容。它还允许 `Windows 2000`、`Windows Server 2003` 和 `Windows Server 2008` 域控制器。
- `Windows Server 2003`。此功能级别仅允许 `Windows Server 2003` 和 `Windows Server 2008` 域控制器。它不允许存在 `Windows 2000` 域控制器。

### Windows Server 2008

- `Windows Server 2008`。此功能级别不支持向后兼容。仅支持 `Windows Server 2008` 域控制器。

在 `Windows 2000 原生` 域功能级别下，可提供以下基本 `Active Directory` 功能：

- `从媒体安装`。此功能在 `Windows Server 2003` 中引入，允许你使用现有域控制器的备份将服务器提升为域控制器状态。
- `应用程序分区`。正如你已了解的，应用程序分区允许你对应用程序信息如何在 `Active Directory` 中复制进行更精细的控制。
- `拖放用户界面`。此功能允许你在诸如 `Active Directory 用户和计算机` 以及 `Active Directory 站点和服务` 等工具中，将对象从一个容器拖放到另一个容器。（此功能在 `Windows 2000` 中不可用。）
- `全局组嵌套和通用安全组`。此功能在创建 `Active Directory` 组对象时提供了更大的灵活性。
- `SIDHistory`。每个 `Active Directory` 用户、组和计算机都拥有一个安全标识符（`SID`），用于授予或拒绝访问 `Active Directory` 内部资源、文件服务器以及 `Active Directory` 感知应用程序的权限。`SIDHistory` 允许在对象从一个域迁移到另一个域时，用户保留对这些 `SID` 的访问权限。

在 `Windows Server 2003` 域功能级别下，域可以包含 `Windows Server 2003` 和 `Windows Server 2008` 域控制器。除了 `Windows 2000 原生` 模式下可用的所有功能外，还支持以下功能：

- `lastLogonTimestamp` 属性。`lastLogonTimestamp` 是用户类的一个属性，允许管理员跟踪域内计算机和用户的登录时间。
- `inetOrgPerson` 对象的密码。`Windows Server 2003` 引入对 `inetOrgPerson` 对象类的支持，可用于与其他目录服务（例如 `openLDAP`）互操作。在 `Windows Server 2003` 域功能级别下，可以为 `inetOrgPerson` 对象配置密码和权限，就像 `Active Directory` 用户对象一样。
- `域重命名`。顾名思义，此功能允许你重命名 `Active Directory` 域，例如将域名从 `example.com` 重命名为 `cohoweinyou.com`。此操作仍有一些限制。例如，你不能使用域重命名将子域重构为独立域树的父域。即使在单域环境中，重命名域也是一个非平凡的操作，需要在生产环境中尝试之前进行充分的规划和测试。
