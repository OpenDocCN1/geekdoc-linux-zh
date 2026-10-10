
## 介绍 Active Directory 域服务

![](img/a8ee53dbf1310726255b6fbb9f296fb2_43_0.png)

Windows Server 2008 中的 Active Directory 域服务 (AD DS) 为 Microsoft 网络提供集中式认证服务。Active Directory DS 的一些优点包括分层组织结构、多主认证（从多个管理点访问和修改 AD DS 的能力），以实现容错和冗余、对网络资源的单点访问，以及能够创建与运行旧版本 Active Directory 甚至 UNIX 的外部网络之间的信任关系。Windows Server 2008 包含许多改进 Active Directory 的新功能，包括引入只读域控制器 (RODC)、细粒度密码策略、改进的图形用户界面 (GUI)、改进的 Active Directory 修改和删除审核、无需完全重启域控制器即可作为服务启动和停止 Active Directory 以进行维护的能力，以及引入 Server Core，这是 Windows Server 2008 的一种最小化安装，与服务器操作系统的完整安装相比，其攻击面大大减少。

## 识别 Active Directory 的功能和优势

Microsoft 在 Windows Server 2000 中引入了 Active Directory 服务，作为 Microsoft 网络上有关网络用户、计算机、服务及其他资源信息的主要存储库。尽管 Windows Server 2003 和 Windows Server 2008 中后续版本的 Active Directory 引入了新的功能和安全特性，但该服务的基本前提保持不变：为大型和小型组织提供集中式的认证和授权存储库。

目录服务允许企业定义、管理、访问和保护网络资源，包括文件、打印机、人员和应用程序。如果没有目录服务的高效性，企业将难以跟上快节奏数据交换的需求。随着企业网络在复杂性和重要性上持续增长，企业对促进自动化的网络提出了越来越多的要求。在 Windows Server 2008 中，Microsoft 提供了两个可以目录服务角色：

- **Active Directory 域服务 (AD DS)** 提供了完整的目录服务，在 Windows Server 2003 和 Windows 2000 中被称为 *Active Directory*。
- **Active Directory 轻型目录服务 (AD LDS)** 提供一个轻量级、灵活的目录平台，Active Directory 开发者可以使用它而无需承担完整的 Active Directory DS 目录服务的开销。例如，应用程序开发人员可以使用 AD LDS 来提供与 AD DS 集成的员工照片目录，而无需实际在整个公司存储数百或数千个图形文件。

配置了 Active Directory DS 角色的 Windows Server 2008 计算机被称为*域控制器 (DC)*。域控制器是一个存储 Active Directory 数据库并在登录期间对网络用户进行认证的服务器。每个域控制器积极参与存储、修改和维护 Active Directory 数据库信息，这些信息存储在每个域控制器上，在一个名为 ntds.dit 的文件中。Active Directory 是一个*多主数据库*，这意味着管理员可以从任何域控制器更新 ntds.dit。将每个域控制器与网络其他地方发生的更改保持同步的过程称为*复制*。当域控制器向网络上的其他域控制器传输复制信息时，这称为*出站复制*。相反，当域控制器从网络上的其他域控制器接收 Active Directory 数据库的更新时，这称为*入站复制*。

![](img/a8ee53dbf1310726255b6fbb9f296fb2_43_1.png)

有关 Active Directory 轻型目录服务的更多信息，请参阅第 2 课。

考虑一个具有三个域控制器的小型网络：DC1、DC2 和 DC3。用户更改了她的密码，更新了 DC1 上的 ntds.dit 数据库。DC1 必须将此更改复制到 DC2 和 DC3。域控制器会自动与同一域中的其他域控制器进行复制，以确保 Active Directory 数据库的一致性。Windows Server 2008 依赖一个或多个域控制器来管理对网络服务的访问。

Active Directory 旨在通过处理各种规模的组织（从小型企业到全球企业）来实现可扩展性。实际上，Active Directory 在理论上可扩展到持有 4,294,967,041 ($2^{32}$ - 255) 个独立对象。从实际角度来看，这意味着 Active Directory 数据库的最大尺寸实际上仅受限于部署在域控制器上的硬件的处理能力。

高性能的 Active Directory 域服务的主要优势包括：

- 集中式资源和安全管理
- 访问全球资源的单点登录
- 容错和冗余
- 简化的资源定位

### 集中资源和安全管理

Active Directory 提供了一个单点，管理员可以从中管理网络资源及其相关的安全对象。组织可以根据组织模型、业务模型或被管理的功能类型来管理 Active Directory。例如，组织可以选择通过逻辑划分用户来管理 Active Directory，划分依据包括用户工作的部门、地理位置或这些特征的组合。

> 有关功能级别的信息，请参阅本课后面的“使用林和域功能级别”。

Active Directory 可以简化所有网络资源的安全管理，并扩展与各种应用程序和设备的互操作性。通过集中访问管理工具和 Active Directory 网络资源数据库来简化管理。在 Windows Server 2008 中，通过使用功能级别，提供了与以前版本 Microsoft Windows 的互操作性。

当安装和配置 Active Directory 时，它包含许多可用于在详细级别管理网络服务、资源和安全的 GUI 和命令行工具。可以从网络中的任何域控制器或安装了这些工具的管理工作站访问这些管理工具。当你将 Windows 2008 Server 配置为 Active Directory 域控制器时，你会看到以下工具被添加到“管理工具”文件夹中：

- Active Directory 用户和计算机
- Active Directory 域和信任关系
- Active Directory 站点和服务
- ADSI 编辑

你会在整个书中看到对这些管理工具的描述。当你接触到新概念时，将注明每个相关任务应使用的工具。这将允许你以可管理的节奏构建你的管理知识。

> 与 Windows 2000 和 Windows Server 2003 中的 Active Directory 不同，Windows Server 2008 不再支持使用 Windows NT 域控制器。

### 提供资源访问的单点

在目录服务引入企业网络之前，所有用户都需要登录到许多不同的服务器才能访问各种不同的资源。这要求用户多次输入其认证信息，并且管理员必须在组织中的每个服务器上维护重复的用户帐户。想象一下...

