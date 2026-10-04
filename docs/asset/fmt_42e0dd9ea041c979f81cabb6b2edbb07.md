
# 试题答案解析

## 49
答案 C 正确。APIPA 只向客户端分配 `169.254.x.x` 范围私有 IP 地址——它不会像 DHCP 服务器那样发布信息（例如默认网关）。其他所有答案都是错误的。

## 50
答案 D 正确。只要运行微软系统的机器具有 CD-ROM 支持和软磁盘，你就可以从中创建安装磁盘。因此，Bob 不需要去 Windows 2000 机器；他可以通过运行 `makebt2` 程序使用 Windows 98 机器；因此，答案 A 是正确的。`winnt32` 程序用于安装 Windows 2000，而不是创建安装磁盘；因此，答案 B 是错误的。由于 Windows 98 是 32 位操作系统，他无法使用 `makebt2` 程序；因此，答案 C 是错误的。

## 51
答案 B 和 C 正确。Windows 2000 DNS 主机记录要么是手动创建，要么通过 DHCP 客户端注册自动添加。其他所有答案都是错误的。

## 52
答案 A、B 和 C 正确。它们都是内存问题存在的良好指标。缓存故障是处理器的测量值；因此，答案 D 是错误的。

## 53
答案 D 正确。默认情况下，本地管理员账户被授予独立工作站和服务器的恢复帐户角色。其他所有答案都是错误的。

## 54
答案 C 正确。虽然系统监视器和任务管理器允许你监控性能，但它们没有性能日志和警报的日志功能；因此，答案 A 和 B 是正确的。性能监视器用于之前的 Windows 版本；因此，答案 D 是错误的。

## 55
答案 A 和 C 正确。复杂度要求相当严格，最小密码长度可以设置为至少 1。其他选项不存在，因此是错误的。

## 56
答案 B 正确。分区是在格式化硬盘时设置的硬盘空间逻辑划分。其他所有答案都是错误的。

## 57
答案 B 正确。这里最可能的情况是新显卡的驱动程序没有正确安装，或者没有提供所需的分辨率色彩深度。大多数情况下，从驱动程序选项安装最新的驱动文件可以解决此问题。视频适配器极可能兼容 Windows 2000，只需更新驱动程序；因此，答案 A 是错误的。安装默认的即插用显示器将无法解决问题；因此，答案 C 是错误的。在这种情况下不需要重启到安全模式并删除视频适配器，因为视频适配器正在工作，只是没有提供完整功能；因此，答案 D 是错误的。

## 58
答案 A 和 B 正确。因为辅助镜像磁盘故障，Milena 的处理非常简单。她必须打破镜像集，更换磁盘，然后重新创建镜像。由于主磁盘仍在运行，因此不需要恢复数据；因此，答案 C 是错误的。只有当镜像集中的主磁盘故障时，才需要创建特殊的 Windows 2000 磁盘；因此，答案 D 是错误的。

## 59
答案 C 正确。唯一的限制是你购买的许可数量和你的服务器的性能（马力）。其他所有答案都是错误的。

## 60
答案 D 正确。只有包含在 Windows 2000 中的 NTFS 5 支持文件和文件夹加密。其他所有答案都是错误的。

# 附加资源

关于 Windows 2000 服务器和微软认证有很多信息。本附录提炼了我们在这些主题上找到的一些最佳资源。

## 网络资源

- 微软培训与认证主页：`http://www.microsoft.com/traincert/default.asp`
- 微软提供的 Windows 2000 服务器主页：`http://www.microsoft.com/windows2000/server/default.asp`
- Windows 2000 资源包在线：`http://www.microsoft.com/windows2000/techinfo/reskit/en-us/default.asp`
- 在 Web上搜索 TechNet：`http://www.microsoft.com/technet`
- Windows 2000 部署指南：`http://www.microsoft.com/windows2000/techinfo/reskit/dpg/default.asp`
- Cramsession Windows 2000 服务器学习指南：`http://studyguides.cramsession.com/cramsession/microsoft/win2kserver`
- Certguide.com：`http://www.certguide.com/2000/70215.asp`
- Cram4Exams 免费考试：`http://www.cram4exams.com/exams/w2kersbig2.shtml`
- John Savill 关于 Windows 2000 服务器的常见问题：`http://www.windows2000faq.com/`
- MCSE 信息门户：`http://www.hardcoremse.com/`
- CertCities MCSE 认证社区：`http://www.certcities.com/certs/microsoft/`
- TechTarget 的 Windows 2000 仓库：`http://searchwin2000.com`
- Windows 模拟考试：`http://www.certutor.com`
- Paul Thurrott 的 Windows 超站点：`http://www.activewin/default.asp`

# 术语表

## 绑定 (binding)
在操作系统层面将网卡（NIC）、协议和服务进行关联，通过相关组件的关联来最大化性能。

## 启动盘 (boot disks)
一组用于启动 Windows 的软盘。这些磁盘有时被用于启动启动失败的系统。

## NetWare 客户端服务 (CSNW)
一种 Windows 服务，为 Windows 2000 客户端计算机提供与 NetWare 服务器交互的界面。

## 启动分区 (boot partition)
存储 Windows 2000 操作系统文件的分区。这些文件通常存在于名为 `WINNT` 的文件夹中。

## 压缩 (compression)
通过压缩数据来节省磁盘空间的过程。

## 证书 (certificate)
由第三方（称为证书颁发机构或 CA）颁发的数字签名，声称已验证服务器或个人的身份。

## 计算机账户 (computer account)
代表域内特定（Windows 2000）计算机的账户。

## 碎片整理 (defragment)
重新组织文件的过程，使其在硬盘上以连续方式存储。

## CHKDSK
用于检查硬盘上文件和文件夹结构的实用程序。你可以让 `CHKDSK` 检查硬盘的物理结构。`CHKDSK` 可以根据需要执行修复。

## 设备管理器 (Device Manager)
一种 Windows 2000 管理工具，用于安装、配置和管理硬件设备。

## 客户端 (client)
网络上的计算机，用于向另一台计算机（通常称为服务器）请求资源或服务。

## 数字签名 (digital signature)
一种用于验证客户端身份的电子化证书。

## 客户端访问许可 (CAL)
连接到服务器的授权连接数。许可选项包括按席位和按服务器。按服务器许可是基于连接的许可模型。在该模型中，你为连接到特定机器的每一个连接购买一个许可。按席位许可允许用户连接到所有服务器。

## 磁盘清理 (Disk Cleanup)
一种用于通过删除临时、孤立文件或下载的文件；清空回收站；压缩很少使用的文件；压缩索引目录文件来重新获得硬盘空间的工具。

## 磁盘碎片整理 (Disk Defragmenter)

## 磁盘管理 (Disk Management)
一种允许你在 Windows 2000 中管理存储设备的工具。

## 磁盘配额 (disk quota)
一种配置设置，允许你限制用户消耗的存储空间。

## 分布式文件系统 (Dfs)
一种 Windows 2000 服务器服务，在单一层次结构中管理共享网络资源。

## 域控制器 (domain controller)
用于验证域登录的计算机。它还维护 Windows 2000 域的活动目录（Active Directory），该目录存储了关于用户、组、策略、计算机和资源的所有目录信息和关系。

## 域名系统 (DNS)
一种用于将主机名转换为 IP 地址，并在基于 TCP/IP 的网络上定位资源的命名系统。

## 域用户和组 (Domain Users and Groups)
活动目录中的此默认内置组包含以下组：账户操作员（Account Operators）、管理员（Administrators）、备份操作员（Backup Operators）、来客（Guests）、打印操作员（Print Operators）、复制器（Replicator）、服务器操作员（Server Operators）、用户（Users）。

## 驱动程序 (driver)
操作系统用于与设备通信的特定设备软件组件。

## 签名 (driver signing)
签名驱动是指完整性经过微软验证并经过数字签名以便安装的驱动程序。Windows 2000 可以拒绝安装任何未签名的驱动程序。来自微软和批准供应商的所有驱动程序都经过了签名。

## 动态磁盘 (dynamic disk)
一种 Windows 2000 硬盘，只能包含通过磁盘管理工具创建的动态卷。动态磁盘不包含分区或逻辑驱动器，且无法被 DOS 访问。

## 紧急修复磁盘 (ERD)
一种可以修复故障系统的磁盘；通过备份实用程序创建。

## 加密文件系统 (EFS)
一种 Windows 2000 支持的文件系统，可为存储在 NTFS 卷上的数据提供加密。

## 事件查看器 (Event Viewer)
Windows 2000 内置的一种实用程序，用于查看和管理 Windows 2000 事件日志。事件查看器包括用于应用程序相关事件的应用程序日志、用于安全和审计相关事件的安全日志，以及用于记录与 Windows 2000 服务器本身和任何已安装驱动程序相关的硬件和软件问题的系统日志。

## 文件分配表 (FAT)
最初随 DOS 引入的文件系统；它不提供文件系统安全功能。

## NetWare 文件和打印服务 (File and Print Services for NetWare)
一种 Windows 2000 服务，允许 NetWare 客户端访问 Windows 2000 文件和打印资源。

## 文件复制服务 (FRS)
一种服务，在运行 Windows 的指定服务器之间以及存储在指定目录树中的登录脚本和策略之间提供多主文件复制。

## Macintosh 文件服务 (File Service for Macintosh)
一种 Windows 2000 服务，允许 Macintosh 客户端访问 Windows 2000 基于文件的资源。

## Unix 文件服务 (File Services for Unix)
一种 Windows 2000 服务，允许 Unix 客户端访问 Windows 2000 资源。

## NetWare 网关服务 (GSNW)
一种 Windows 2000 服务，在 Windows 2000 服务器和 NetWare 之间提供连接性服务，允许 Windows 2000 客户端通过连接到 Windows 2000 服务器来偶尔访问 NetWare 资源。

## 组策略对象 (GPO)
一种安全机制，用于对网络设置配置的谁、什么、何时、何地、如何以及为什么提供细粒度的控制。通过使用 GPO，你可以轻松地为网络上的每个组配置安全设置。

## 硬件兼容列表 (HCL)
一个 Windows 支持的硬件设备列表。Windows 2000 服务器发行光盘上有一个 HCL 版本，但网站 `http://www.microsoft.com/hwdq/hcl/` 会进行定期更新。

## 互联网连接共享 (Internet Connection Sharing)
内置在 Windows 2000 中的一项功能，允许计算机与其他计算机共享互联网连接。

## 互联网信息服务 (IIS)
一种用于 Windows 的 Web 服务器平台。

## 互联网数据交换 (IPX/SPX)
一种由 Novell 开发的专用协议。

## 最后已知配置 (Last Known Configuration)
存储最后工作设置的系统，以允许计算机启动。

## 许可 (licensing)
授权软件使用的方法。

## 本地用户和组 (Local Users and Groups)
用于管理用户组的 Windows 组件。

## 微软管理控制 (MMC)
一种通过单元程序实现的 Windows 标准管理界面。

## 镜像卷 (mirrored volume)
一种容错磁盘配置，数据写入两个磁盘而不是一个，以便在其中一个故障时数据仍然可以访问。

## NetBIOS 增强接口 (NetBEUI)
微软的一种网络协议，由于其使用非表格广播定位资源而正在被淘汰。

## 网络适配器 (network adapter)
允许计算机与网络通信的硬件设备。

## 网络地址转换 (NAT)
一种标准，允许局域网使用一组地址进行内部流量，使用另一组地址连接到互联网。

## 策略 (policy)
自动配置用户设置的组件。

## 打印设备 (print device)
产生打印输出的物理硬件设备。

## 网络监视器 (Network Monitor)
一种用于查看和排除数据包故障的 Windows 2000 实用程序。

## 打印服务器 (print server)
网络上打印服务的计算机。

## NTFS 文件系统 (NTFS)
Windows 2000 首选的文件系统，支持文件级安全、加密、压缩、审计等。

## Unix 打印服务 (Print Services for Unix)
一种允许 Unix 客户端访问 Windows 2000 打印资源的 Windows 2000 服务。

## 打印机 (printer)
运行在打印服务器上的托管打印服务的软件组件。

## NTFS 压缩
一种减少数据在 NTFS 上磁盘空间的工具。

## 打印驱动程序 (printer driver)
用于与打印设备以及操作系统和应用程序通信的软件。

## NWLink
微软对 Novell IPX/SPX 协议簇的实现。

## 协议 (protocol)
跨网络通信的定义的规则集。大多数协议限于 OSI 参考模型的一个或多个层。例如用于通过网络传输文件的文件传输协议 (FTP)，以及交付 Web 页面的超文本传输协议 (HTTP)。

## 分区 (partition)
硬盘空间的逻辑划分。

## 性能 (performance)
对系统运行效率的衡量。

## 即插即用 (Plug and Play)
允许操作系统识别设备、安装正确的驱动程序并自动启用设备的技术。

## RAID-5 阵列 (RAID-5 array)
由三个或更多硬盘组成的磁盘配置，数据以等量写入所有磁盘。为了分担负载。为了容错，写入的数据中添加了校验信息，以便在驱动器故障时进行恢复。

## 恢复控制台 (Recovery Console)
一种在核心系统组件或驱动程序故障时用于系统恢复的命令行控制系统。通过恢复控制台，可以使用简单命令将操作系统恢复到功能状态。

## 注册表 (Registry)
Windows 系统中以值对形式存储所有系统信息的分级数据库。

## 注册表编辑器 (Registry editor)
用于直接编辑注册表的工具，应仅由经验丰富的管理员操作，且仅在执行并验证了完整的注册表备份后进行。

## 远程访问服务 (RAS)
远程访问服务允许远程客户端拨入 Windows 2000 服务器以访问网络资源，就像它们物理连接到网络一样。

## 远程管理模式 (Remote Administration Mode)
Windows 终端服务器模式允许你远程连接到服务器，并像坐在控制台前一样管理它。

## 安全模式 (Safe Mode)
一种允许系统以加载最少设备驱动程序和服务启动的恢复工具。安全模式通过减少发生问题时需要考虑的因素数量，有助于简化诊断。

## 安全模板 (security template)
一个包含配置系统安全设置内置指南的文件。

## 服务 (service)
服务器执行的任何操作，无论是通过操作系统执行，还是根据客户端请求执行。

## 服务包 (Service Pack)
一种提供将一组文件替换为另一组文件的可执行程序。对于操作系统（如 Windows 2000），服务包是分发错误修复和修复程序的一种。

## 安装磁盘 (setup disks)
一组四张磁盘，用于执行从 Windows 2000 CD-ROM 启动时的操作。

## 安装管理器 (Setup Manager)
一种用于为无人安装创建答案文件的实用工具。

## 简单卷 (simple volume)
一种本质上与基本存储分区相同的存储卷；磁盘空间仅使用来自一个物理磁盘。

## 预整合 (slipstreaming)
一种在 Windows Server 安装过程中将最新的服务包、修复程序和文件应用的过程。

## 系统监视器 (System Monitor)
一种 MMC 插入组件，允许你查看来自服务器或网络或其他服务器或工作站的计数器的实时性能数据。

## 跨卷 (spanned volume)
一种可以利用 2 到 32 块物理磁盘空间创建一个逻辑上连续的大型存储卷。跨卷不提供容错能力，因此如果一个磁盘故障，整个集合都将丢失。

## 系统分区 (system partition)
活动分区；换句话说，计算机 BIOS 从之开始启动过程的分区。

## 系统状态 (System State)
一组用于备份目的的设置集合，包括注册表、COM+ 类注册数据库和系统启动文件。对于作为证书服务器运行的 Windows 2000 服务器，系统状态数据包含证书服务数据库。

## 条带卷（带校验） (striped volume (with parity))
