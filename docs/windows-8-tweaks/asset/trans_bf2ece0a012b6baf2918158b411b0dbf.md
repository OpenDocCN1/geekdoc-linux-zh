

## 表 13-2

| 名称 | 用途 |
| --- | --- |
| Security Accounts Manager | 作为账户信息的数据库，用于身份验证和校验。这是一个系统关键服务，不应禁用。 |
| Security Center | 监控所有安全应用程序，例如防病毒和恶意软件防护。该服务还负责通知消息，这些消息可能会让高级 Windows 用户抓狂。你可以随意禁用此服务，但如果保护软件（如防病毒实用程序）和你的防火墙被关闭，你将不会收到警告。 |
| Sensor Monitoring Service | 监控环境传感器，使你的计算机能够适应不同的亮度级别和其他条件。 |
| Server | 允许你在网络上共享文件、打印机和其他设备。这不是一个系统关键服务，但在家庭网络环境和企业中通常很有用。 |
| Shell Hardware Detection | 提供自动播放硬件事件的通知。 |
| Smart Card | 跟踪你的计算机使用过的智能卡。如果未使用智能卡，可以禁用此服务。 |
| Smart Card Removal Policy | 监控你的智能卡，当智能卡被移除时锁定你的计算机。 |
| SNMP Trap | 处理通过简单网络管理协议接收的消息。 |
| Software Protection | 为下载的软件提供数字许可证支持。请勿禁用。 |
| Spot Verifier | 检查潜在的文件系统损坏。 |
| SSDP Discovery | 使用 SSDP 协议在网络上查找其他兼容的网络设备，例如游戏控制台和扩展器设备。你可以禁用此服务，但这样做不仅会影响媒体中心扩展器，还会影响其他即插即用网络设备。 |
| Still Image Acquisition Events | 当你将相机连接到你的 PC 时启动相关应用程序。 |
| Storage Service | 为存储相关的组策略提供支持。 |
| Superfetch | 通过缓存应用程序信息来加速应用程序加载。你可以禁用此服务，但其好处超过了加载该服务时的初始性能下降。 |
| System Event Notification Service | 监控系统事件并向其他 COM 组件报告。 |
| System Events Broker | 用于 Windows Store 中所有应用程序的 WinRT 应用程序框架的后台任务支持。请勿禁用。 |
| Task Scheduler | 使你能安排进程在指定间隔运行时执行。Windows 8 使用此服务进行所有后台维护，如果禁用此服务，维护将停止。我不推荐禁用此服务。 |
| TCP/IP NetBIOS Helper | 提供通过 TCP/IP 连接的 NetBIOS 协议支持。这主要用于局域网上的机器名称解析。如果你在 Windows PC 之间共享文件，请勿禁用。 |
| Telephony | 为应用程序与调制解调器交互提供支持。由于如今调制解调器很少使用，因此可以禁用此服务。 |
| Themes | 为视觉样式提供支持，使非经典 Windows 外观成为可能。禁用此服务会导致整个界面恢复到经典 Windows 外观。 |
| Thread Ordering Server | 为 Windows 应用程序和组件提供线程管理和优先级设置。禁用此服务可能会使应用程序崩溃，并会禁用 Windows 音频服务。 |
| Time Broker | 为所有 Windows Store 应用程序使用的 WinRT 应用程序框架提供时间和事件相关服务。请勿禁用。 |
| Touch Keyboard and Handwriting Panel Service | 启用触摸键盘和笔功能。仅在需要时启动。 |
| UPnP Device Host | 提供在计算机上托管 UPnP 设备以在本地网络上使用的功能。此服务是 Windows Media Player 库共享所必需的。 |
| User Profile Service | 这是一个系统关键服务，在你登录时加载你的用户配置文件。 |
| Virtual Disk | 负责管理你的驱动器和文件系统。请勿禁用此服务；它是许多操作系统请求所必需的。此外，当不需要时它不会运行。 |
| Volume Shadow Copy | 为备份应用程序使用的卷影副本硬盘数据提供支持。 |
| WebClient | 为 WebDAV 协议提供支持，用于通过资源管理器访问 Internet 上的远程服务器。如果你不需要此协议，可以安全地禁用此服务。 |
| Windows All-User Install Agent | 用于 Windows Store 应用程序的 AppX 安装包支持的一部分。 |
| Windows Audio | 为 Windows 8 提供音频。除非你不喜欢音频，否则我不推荐禁用此服务。但谁不喜欢音频呢？ |
| Windows Audio Endpoint Builder | Windows Audio 的辅助服务，用于管理你计算机中的各种音频相关硬件设备。 |
| Windows Backup | Windows 8 中备份应用程序的一部分，使你能够备份文档和其他重要数据。 |
| Windows Biometric Service | 使应用程序能够捕获、比较、操作和存储生物特征数据。 |
| Windows Color System | 允许其他应用程序在 Windows 8 中配置你的显示器颜色设置。 |
| Windows Connect Now - Config Registrar | Windows Connect Now 功能的一部分，该功能让你通过将一台机器的配置保存到 USB 闪存盘，然后使用它来设置新 PC，从而自动化将其他计算机添加到你的无线网络。 |
| Windows Connection Manager | 根据可用连接和组策略设置提供智能网络连接决策。我不推荐禁用此服务。 |
| Windows Defender Service | Windows 8 中的反间谍软件保护应用程序。如果你使用不同的反间谍软件实用程序，可以随意禁用此服务。 |
| Windows Driver Foundation - User-mode Driver Framework | 支持用户模式下的驱动程序。请勿禁用。 |
| Windows Error Reporting Service | 当出现错误时，此服务让你可以与 Microsoft 联系，查看他们是否为你提供了解决方案，并通知 Microsoft 你的计算机正在发生什么。如果你不想通知 Microsoft 你的错误消息？你可以安全地禁用此服务。 |
| Window Event Collector | 提供订阅远程事件源以监控活动和存储数据的能力。请勿禁用。 |
| Windows Event Log | 这是所有本地事件管理和收集的主要来源。可以停止此服务，但它被 Windows 8 中的许多性能增强功能使用。停止它会导致负面的性能影响。 |
| Windows Firewall | 通过根据应用的防火墙规则阻止入站和出站网络访问来提供网络安全。除非你使用第三方防火墙应用程序，否则请勿禁用此服务；其好处超过了任何性能下降。 |
| Windows Font Cache Service | 通过缓存常用字体数据来优化应用程序。 |
| Windows Image Acquisition (WIA) | 为应用程序提供接口，用于处理各种类型的扫描仪和相机。此服务仅在需要时运行。 |
| Windows Installer | 允许打包到 MSI 文件中的应用程序在你的计算机上安装和卸载。除非你不想安装、卸载或修改任何软件，否则请勿禁用此服务。 |
| Windows Management Instrumentation | 为脚本和其他应用程序提供接口，以控制 Windows 8 的各个组件。禁用此服务会导致 Internet 连接共享、IP 辅助程序和安全中心服务也停止。如果你不使用这些服务，可以随意禁用它。 |
| Windows Media Center Receiver Service | 为媒体中心应用程序提供电视和无线电接收功能。 |
| Windows Media Center Scheduler Service | 为媒体中心应用程序提供关于何时开始和停止录制应用程序的通知。 |

