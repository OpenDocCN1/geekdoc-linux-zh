
### 目标 3

#### 配置 eDirectory 用户访问 OES Linux 服务器

正如 NetWare 服务器上的用户和组通过 eDirectory 管理一样，Linux 服务器上的用户和组也是根据 `POSIX`（可移植操作系统接口）标准进行管理的。

由于 Novell OES 提供了运行在 Linux 和 NetWare 上的服务，Novell 开发了一项技术，让 eDirectory 用户在 Linux 服务器上也能作为 POSIX 用户使用。

这项技术被称为 `Linux 用户管理（LUM）`。

要配置 eDirectory 用户通过 LUM 访问 OES 服务器，你需要了解以下内容：

- LUM 基础
- 如何实现 LUM
- 如何启用 eDirectory 用户访问 Linux

关于 Linux 用户管理的完整信息，请参阅《Novell OES Linux User Management Technology Guide 首页 `lumadgd.pdf`）。
你可以从 `3077` 课程 CD 中的 `OES_Docs` 目录通过 `http://www.novell.com/documentation/oes` 获取该指南。

## LUM 基础

以下内容对你有所帮助：
- LUM 基础
- 如何实现 LUM
- 如何启用 eDirectory 用户访问 Linux

关于 Linux 用户管理的完整信息，请参阅《Novell OES Linux User Management Technology Guide》(`lumadgd.pdf`)。
你可以从 `3077` 课程 CD 中的 `OES_Docs` 目录通过 `http://www.novell.com/documentation/oes` 获取该指南。

# 以下列出了用于启用 用的核心实用程序：

# 表 5-2

| 命令 | 执行位置 | 任务 |
|---|---|---|
| `ftp` | 另一台主机 | 在 OES 服务器之间传输文件，在这种情况下，服务器是远程主机。 |
| `login` | - OES 服务器 | 登录 OES 服务器，可以可以直接登录，也可以通过与服务器的 SSH 会话登录。 |
| | 与 OES 服务器的 SSH 会话 | |
| `passwd` | - OES 服务器 | 修改 POSIX 密码。 |
| | 与 OES 服务器的 SSH 会话 | |
| `rlogin` | 另一台主机 | 登录 OES 服务器，在这种情况下，服务器是远程主机。 |
| `rsh` | 另一台主机 | 在 OES 服务器上执行命令，在这种情况下，服务器是远程主机。 |
| `ssh` | 另一台主机 | 与 OES 服务器建立安全的加密连接，在这种情况下，服务器是远程主机。 |
| `su` | - OES 服务器 | 临时变为另一个用户。 |
| | 与 OES 服务器的 SSH 会话 | |

**服务器上的 Novell Samba (SMB/CIFS) 共享。** 需要访问服务器上定义的 Samba 共享的 Windows 工作组用户必须是已配置访问服务器的启用 Linux eDirectory 用户，因为 Samba 需要 POSIX 身份识别才能访问。

扩展来说，需要访问指向服务器的 SMB/CIFS 存储位置对象（Storage Location Objects）的 NetStorage 用户也必须是具有服务器访问权限的启用 Linux eDirectory 用户。

- Linux 上的 Novell Remote Manager (`NRM`)。你可以通过以下方式访问 NRM：
- 具有查看 Linux 服务器上所有内容权限的 `root` 用户
- 受 POSIX 权限限制的本地 Linux 用户
- 启用了 Linux 的 eDirectory 用户，例如在安装期间创建的 Admin 用户。

# 具有某些 LUM 要求的服务

某些不需要 eDirectory 用户启用 Linux 即可访问服务，但对 LUM 有某些要求的服务，包括以下项：

- QuickFinder、Novell iFolder 2.1x 以及其他 Web 服务。如果只有本地用户访问这些 Web 服务，则不适用 Linux 启用，因为这些用户不是远程 eDirectory 用户。
- NCP 服务器。移植到 Linux 的 NCP 服务器仍然与 eDirectory 保持紧密集成，不需要 eDirectory 用户启用 Linux。

然而，当创建 NCP 卷指向服务器上 NSS 以外的分区时，如果用户未启用 Linux，则并非所有功能都可用。

例如，如果用户未启用 Linux，则无法进行跨协议访问。
- NSS。直接使用 NCP（Novell 客户端）访问 NSS 卷的 eDirectory 用户不需要启用 Linux。

然而，如果使用任何其他访问协议通过虚拟文件系统访问 NSS，使得 NSS 看起来像是一个符合 POSIX 标准的文件系统，则这些用户必须启用 Linux。

# 集成用于 Linux 版本的 Novell 企业级服务器

尽管上述服务不需要启用 Linux 访问，但服务本身作为符合 POSIX 标准的系统用户运行，这些系统用户代表访问服务的终端用户执行功能。

如果服务必须访问 NSS 卷，则系统用户必须启用 Linux，因为只有 eDirectory 用户才能访问 NSS 卷。

# LUM 访问不是对 OES Linux 的全局访问

当你计划为用户启用 Linux 以访问这些服务时，请记住，启用 Linux 用户需要访问的每台 OES Linux 服务器都必须与这些用户所属的启用 Linux 组相关联。

换句话说，如果他们需要访问多台服务器，仅为访问单个 OES Linux 服务器启用 Linux 是不够的。

必须使用 `iManager` 为用户需要访问的每台服务器配置用户所属的启用 Linux 组与服务器关联的 eDirectory UNIX 工作站（UNIX Workstation）对象之间的关联。

# 如何实现 LUM

以下是在你的 OES 网络中实现 LUM 的建议：

字体 哪些用户需要启用 LUM
- 为 eDirectory 用户启用 Linux 访问
- 启用用户 访问多台 OES Linux 服务器

# 哪些用户需要启用 LUM

当你在 OES Linux 服务器上安装 LUM 时，安装 LUM 的 Admin 用户对象会自动启用对服务器的 eDirectory LDAP 认证。

此外，你需要标识需要对 OES Linux 服务器进行 eDirectory LDAP 访问的用户（和组）。你可以通过以下操作来确定这一点：

1. 检查 5-23 页“需要启用 Linux 访问的 OES Linux 服务”下表格中的信息。
2. 识别将运行上述服务的服务器。
3. 记录你需要启用的用户和组，以及你需要允许它们访问的服务器。

# 为 eDirectory 用户启用 Linux 访问

你可以使用 `iManager 2.5` 或 `nambulkadd` 命令为 eDirectory 用户启用 LUM：

- `iManager`。你可以使用 iManager 中的 LUM 任务为现有的 eDirectory 用户启用 Linux 访问。

只要它们可以被分配到同一个主启用 Linux 组，你就可以在同一操作中启用多个用户。该过程允许将该组与一个或多个 OES Linux 服务器或 Linux 工作站关联。
- `nambulkadd`。如果你有需要启用 Linux 访问的 eDirectory 用户和组，可以使用 `nambulkadd` 命令同时修改多个对象。

当使用 iManager 管理 OES Linux 访问时，你可能会发现命名上的差异。

当创建 OES Linux 服务器时，eDirectory 中会创建一个 UNIX Workstation - `server_name` 对象，其中 `server_name` 是 OES Linux 服务器的 DNS 名称。

iManager 用户管理插件将服务器对象称为“Linux Workstation”对象。“Linux Workstation”和“Linux Workstation”（此处原文）指的是相同的 eDirectory 对象。

# 启用用户 访问多台 OES Linux 服务器

你可以通过将用户所属的启用 Linux 组与他们想要访问的每个 UNIX Workstation（Linux Workstation）对象关联，启用用户访问多台 OES Linux 服务器。

用户通过其启用 Linux 的组获得服务器访问权限，而不是通过直接分配给 UNIX Workstation（Linux Workstation）对象。

# 如何为 eDirectory 用户启用 Linux 访问

以下是启用 eDirectory 用户的步骤：

- 如何为 eDirectory 组启用 Linux 访问
- 如何为 eDirectory 用户启用 Linux 访问

你可以在安装了 LUM 的 OES Linux 服务器上启用用户。

# 如何为 eDirectory 组启用 Linux 访问

以下步骤假设 eDirectory 组对象已存在，并且任何想要启用的用户已分配到这些组。

要为 eDirectory 组启用 Linux 访问，请执行以下操作：

1. 以 eDirectory 管理员或等效身份登录 `iManager`。
2. 选择用户管理 > 启用组。
3. 浏览并选择一个多个组对象；点击确定。
4. （条件）如果你想对组内的所有用户启用，请确保勾选“启用这些组中的所有用户”选项。
5. 点击两次“下一步”。
6. 浏览并选择一个多个 UNIX Workstation（OES Linux 服务器）对象；点击确定。
7. 点击“下一步”，然后点击“完成”。
8. 点击确定。

# 如何为 eDirectory 用户启用 Linux 访问

以下步骤假设 eDirectory 用户对象已存在。

要为 eDirectory 用户启用 Linux 访问，请执行以下操作：

1. 以 eDirectory 管理员或等效身份登录 `iManager`。
2. 选择用户管理 > 启用用户。
3. 浏览并选择一个多个用户对象；点击确定。
4. 点击“下一步”。
5. 执行以下操作之一：

- 选择并启用现有的 eDirectory 组。
- 选择已启用 Linux 的 eDirectory 组。
或
- 指定要创建并启用 Linux 的新 eDirectory 组名称和上下文。
6. 完成后，点击“下一步”。
7. 浏览并选择一个多个 UNIX Workstation（OES Linux 服务器）对象；点击确定。
8. 点击“下一步”，然后点击“完成”。
9. 点击确定。

## 练习 5-1 将 DA1 Linux 服务器迁移到 DA-CORP 树

现在你已经复习了时间同步和 Linux 用户管理，可以准备开始练习 5-1 了。

目前，`DA2 NetWare` 和 `DA1 Linux` 服务器位于不同的树中：`DA2 NetWare` 位于 `DA-CORP` 树，而 `DA1 Linux` 位于 `DA-SERVICES` 树。每台服务器都使用其自己的本地时钟作为时间提供源。

练习的起始步骤是配置 `DA2 NetWare` 服务器使用 `DA1 Linux` 服务器作为时间提供源，以便两台服务器实现时间同步。

由于 `DA1 Linux` 服务器目前托管着 `DA-SERVICES` eDirectory 树，在将 `DA1` 安装到 `DA-CORP` 树之前，你必须将该服务器从树中移除。

由于 `DA1 Linux` 服务器还托管着一个与 `DA-SERVICES` 树工作的 LUM 配置，练习的一部分将涉及移除当前的 LUM 配置，然后重新配置 LUM 以与 `DA-CORP` 树工作。

练习 5-1“将 DA1 Linux 服务器迁移到 DA-CORP 树”位于你的《Linux Novell Open Enterprise Server 集成教程》第 5-2 页。

## 目标 4

## 描述 Novell OES 存储解决方案

要描述 Novell OES 可用的存储解决方案，你需要理解以下内容：

- Novell OES 中的文件系统支持
- Linux 上的 NetWare 协议支持（Novell 客户端支持）
- 存储选项
- OES 文件存储规划

### Novell OES 中的文件系统支持

如下所示，两种 Novell OES 服务器平台都支持 Novell® Storage Services™ (`NSS`) 及其传统文件系统：

图 5-6

![](img/1dca8e8a8784dadffa032dcfe0460e55_352_0.png)

以下是文件类型的摘要：

- 传统的 Linux 文件系统。Novell OES Linux (`SLES 9`) 支持多种不同的文件系统，最常见的是 `ext2`、`ext3` 和 `ReiserFS`。

在各种 Linux 传统文件系统上，对 OES 服务的支持没有差异。

在 OES Linux 上，Linux 和 Novell Storage Services (`NSS`) 之间的服务支持存在差异。

### 在 Linux 上集成 Novell Open Enterprise Server

**传统 NetWare 文件系统。**尽管它在 NetWare 服务器上被认为是遗留文件系统，但 NetWare 传统文件系统仍然强大强大，并支持 NetWare 文件服务访问模型。

**Novell Storage Services (`NSS`)。** `NSS` 允许你为任何规模的组织共享文件存储。

在 NetWare 上，`NSS` 的特性包括：

- 可见性
- Trustee 访问控制支持
- 多个并发命名空间支持
- 原生 Unicode
- 用户和目录配额
- 丰富的文件属性
- 多数据数据流支持
- 事件文件列表
- 文件救援子系统

这些许多功能在 OES Linux 的 `NSS` 中也得到了支持。

![](img/1dca8e8a8784dadffa032dcfe0460e55_353_0.png)

要比较 NetWare 和 Linux  NSS，请参考《Novell Storage Services File System Administration Guide》(`nss_enu.pdf`) 第 413 页的“NetWare 上 NSS 与 Linux 上 NSS 的比较”。

你可以从 `3077` 课程 CD 上的 `OES_Docs` 目录通过 `http://www.novell.com/documentation/oes` 访问该指南。

### Linux 上的 NetWare 协议支持（Novell 客户端支持）

许多组织依赖 NetWare Core Protocol™ (`NCP`) 和 Novell Client™ 软件来实现文件存储服务的高安全性访问。

OES Linux 的 NCP 服务器允许你使用 Novell Client 软件连接到 Linux。

### 存储选项

要理解 Novell OES 存储选项，你需要了解以下内容：

- 直接连接存储选项（NSS 和传统）
- 高级存储选项（仅限 NSS）

### 直接连接存储选项（NSS 和传统）

如图 5-6 所示，你可以在两种 Novell OES 平台上安装传统卷和 Novell 存储系统 (`NSS`) 卷。

这些设备可以安装在服务器内部，也可以通过外部 SCSI 总线直接连接到服务器。

### 高级存储选项（仅限 NSS）

`NSS` 卷支持以下高级存储解决方案：

- 网络附属存储 (`NAS`) 解决方案。`NAS` 是一个专用的数据服务器或设备，通过现有的网络基础设施为用户和应用程序服务器提供集中访问。它使用以太网和 TCP/IP 等传统的 LAN 协议。

使用千兆以太网时，访问速度与直接连接存储设备的速度相似。

缺点是数据请求和数据会竞争网络带宽。
- 存储区域网络 (`SAN`) 解决方案。`SAN` 是由服务器和存储媒体组成的独立专用网络，通过高速互连连接。

Novell iSCSI。你可以使用 Novell iSCSI 创建 SAN，它使用 Novell eDirectory 管理 iSCSI 资源，包括授予 trustee 权限和用户访问。

容错和高可用架构。你可以使用以下一种或多种技术：

- 多路径 I/O。`NSS` 通过自动识别每个 NetWare 服务器与其存储设备之间的多条路径，帮助防止 CPU 与存储设备之间连接的故障。
- 软件 RAID。`NSS` 支持软件 RAID，通过增强数据容错和 I/O 性能来提高存储的可用性和性能。
- 服务器集群。你可以将 OES NetWare 配置为高可用集群，当托管服务器故障时，资源和服务将自动配置从一台服务器切换到另一台服务器。你也可以手动从一台服务器切换到另一台，以帮助维护服务器。

### OES 文件规划

以下内容帮助你规划 OES 存储：

- 文件服务考虑因素
- NSS 考虑因素

### 文件服务考虑因素

以下说明了哪些文件服务可以访问 OES 中的卷类型：

图 5-7

![](img/1dca8e8a8784dadffa032dcfe0460e55_356_0.png)

### NSS 考虑因素

以下是 `NSS` 的考虑因素：

**设备大小限制。** `NSS` 识别的逻辑或物理设备最大大小为 `2TB`。如果你的存储磁盘大于 `2TB`，请使用存储设备实用程序将其分区为较小的逻辑设备以供 `NSS` 使用。在规划 OES Linux 上的 `NSS` 时特别要注意，因为 Linux 传统卷的大小限制为 `8TB`。

**其他 NSS 规划主题。** 规划 `NSS` 时，请考虑以下主题：
* 系统要求
* 安全考虑
* 未来存储需求规划
* 在 eDirectory 中创建和命名存储对象

有关存储规划的详情，请参考《Novell Storage Services File System Administration Guide》(`nss_enu.pdf`) 第 65 页的“规划 NSS 解决方案”。

你可以通过 `http://www.novell.com/documentation/oes` 或从 `3077` 课程 CD 上的 `OES_Docs` 目录访问该指南。

## 目标 5

## 使用 NCP 服务器提供文件访问

Windows 版 Novell Client 是一种长期软件解决方案，用于从 Windows 工作站访问基于 NCP 的 NetWare 数据。

Novell Client 扩展了 Windows 桌面的能力，使其能够访问 Novell 服务，例如 eDirectory 身份验证、网络浏览和服务解析，以及安全的文件系统访问。

它支持 `NCP`、`RSA` 和 `NDAP` 等传统的 Novell 协议，并与 `LDAP` 等开放协议协作。

Linux 版 Novell Client 为 Linux 工作站提供相同的服务。预计 Linux 版 Novell Client 将 OES 发布后作为免费下载提供。

由于现在 OES Linux 上提供了 NCP，Novell Client 用户可以像连接到 NetWare 服务器一样轻松地连接到 OES Linux 服务器。

Linux NCP 服务器启用了对登录脚本、OES Linux 服务器驱动器映射以及与 Novell Client 访问常用的服务的支持。

在本目标中，你将学习 Novell OES 包含的 NCP 服务的相关知识：

* NCP 的用途
* 如何安装和配置 NetWare NCP 服务器
* 如何安装和配置 Linux NCP 服务器

> Novell OES 的初始版本不支持事务跟踪（Transaction Tracking）和乐观锁定。

## NCP 的用途

通过 Novell OES，NetWare 核心协议 (`NCP`) 支持 OES NetWare 和 OES Linux 服务器上的许多网络服务。

Windows 用户可以使用 Novell Client 像在 NetWare 服务器上一样，访问 OES Linux 服务器上的数据、管理文件和文件夹，并映射驱动器。

以下说明了 NCP 文件服务的基本知识：

![](img/1dca8e8a8784dadffa032dcfe0460e55_359_0.png)

## 如何安装和配置 NetWare NCP 服务器

在安装 OES NetWare 服务器后，在安装了 Novell Client 的工作站上的 eDirectory 用户可以访问您授予其访问权限的所有目录和文件。

对于 OES NetWare 上的 NCP 卷，可以通过 `NRM` 或通过 Novell Client 管理权限。

您可以通过以下步骤使用 Novell Client 来管理文件系统权限：

- 1. 使用 Novell Client 以具有 NCP 卷**管理员（Supervisor）**权限的用户身份登录树结构。
- 2. 导航到 NCP 卷（例如使用“我的网络位置”）并找到您想要管理权限的文件夹。
- 3. 右键点击**文件夹**并选择*属性（Properties）*；然后选择**NetWare 权限（NetWare Rights）**选项卡。
- 4. 浏览并选择您想要赋予受托（trustee）权限的**用户**；然后点击**添加（Add）**。
- 5. 从属性窗口顶部的受托列表中选择所需文件系统权限的*复框*；然后点击**确定（OK）**。

## 如何安装和配置 Linux NCP 服务器

安装 OES Linux 时，默认选择 NCP Server。可以使用 NCP Server 安装 NSS，但并不是必需的。

如果您安装了 Linux 版 NCP Server，相同的 eDirectory/Novell 客户端可以访问 OES Linux 服务器上的文件。然而，最初没有可用的目录或数据卷。

这些需要 OES NetWare 不需要的设置步骤。

要在 OES Linux 上配置 NCP，您需要了解以下内容：

- 默认 NCP 卷
- 如何创建卷指针
- 如何分配文件受托权限

## 默认 NCP 卷

Linux 版 NCP Server 允许 NCP 访问在 OES Linux 服务器上定义的 NCP 卷。

当您安装 NCP 服务器时，安装程序会创建一个名为 `SYS` 的 NCP 卷，映射到 Linux 服务器上的 `/usr/novell/sys` 文件夹。

此 NCP 卷包含 `LOGIN` 和 `PUBLIC` 目录，这些目录又包含了与 NetWare 中同名目录相同的一小部分文件。

## 如何创建卷指针

最初，连接到 OES Linux 服务器的 Novell Client 没有任何可用的 NCP 主目录或数据卷。

如果您希望用户在服务器上拥有 NCP 主目录或数据目录，您必须决定希望这些目录出现在服务器目录结构的何种位置，并使用 Linux 提示符下使用 `NCPCON` 工具创建 NCP 卷。

例如，如果您想创建一个名为 `HOME` 的 NCP 卷（指针），将执行以下步骤：

- 1. 确定您想将其挂载到 Linux 服务器上的 `/home` 挂载点。
- 与 Linux 系统上的其他挂载点不同，可以将 NCP 卷挂载到已填充的目录。该挂载点下的文件和目录供 NCP 客户端访问。
- 2. 创建卷指针：
    a. 在终端提示符下，输入 `ncpcon`。
    b. 在 `ncpcon` 提示符下，输入 `create volume HOME /home`。

创建卷指针后，Novell Client 即可连接到 OES Linux 服务器并看到 `HOME` 卷以及安装创建的 `SYS` 卷。

NCP 卷指针始终以大写名称（`HOME`、`SYS` 等）创建，无论创建卷指针时指定的大小如何。

## 如何分配文件受托权限

您使用 Novell Client 为 OES Linux 服务器上的 NCP 卷创建文件系统受托的方法与在 OES NetWare 上的 NCP 卷相同。

然而，OES Linux 上的 Novell Remote Manager 不能用于创建文件系统受托或管理 NCP 卷上的权限。

OES Linux 上 NCP 卷的受托分配存储在该卷的 `.trustee_database.xml` 文件中。该 XML 文件存储在用作 NCP 卷点的文件夹中。

文件名开头的点表示这是一个隐藏文件。

例如，对于挂载在 `/home` 的 `HOME` 卷，受托分配保留在 `/home/.trustee_database.xml` 文件中。以下是一个未配置任何受托分配的 `.trustee_database.xml` 文件示例：

5-9

```xml
