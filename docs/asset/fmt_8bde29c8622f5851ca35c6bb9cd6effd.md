
### 4. 现在您必须提供您想使用 AutoYaST 的信息。

在引导提示符下，输入以下参数（假设安装仓库可通过 `10.0.0.3/data/SL_ES10/` 通过 NFS 访问）：

```bash
autoyast=floppy:///autoinst.xml install=nfs://10.0.0.3/data/SL_ES10/ splash=verbose
```

最后一个参数会在引导过程中切换到详细显示，以便您可以轻松查看引导消息。经过短暂时间后，YaST 启动。安装以 Novell 软件许可协议开始（该协议将被自动接受）。经过一些检查后，软件包将从 NFS 服务器复制。系统在安装过程结束时重新启动。重新启动后，如果 AutoYaST 配置文件中未设置密码，您可以无需密码以 root 身份登录。您应立即为 root 设置密码。

### 总结

| 目标 | 摘要 |
| :--- | :--- |
| 1. 自动安装基础 | AutoYaST 是一个用于自动化安装的工具。<br><br>安装由一个 XML 文件控制，该文件包含特定于机器的信息。<br><br>AutoYaST 最佳使用时需配合也运行 TFTP 和 DHCP 服务器的安装服务器。<br><br>安装服务器可通过 NFS、HTTP 和 FTP 协议访问。 |
| 2. 设置安装服务器 | 要设置安装服务器，请使用 YaST 模块`安装服务器`：<br>`yast2 > Miscellaneous > Installation Server`<br>或<br>`yast2 instserver` |
| 3. 为 AutoYaST 创建配置文件 | 要为 AutoYaST 创建配置文件，请使用 YaST 模块`自动安装`：<br>`yast2 > Miscellaneous > Autoinstallation`<br>或<br>`yast2 autoyast`<br>AutoYaST 配置文件的默认目录是<br>`/var/lib/autoinstall/repository/`。 |
| 4. 启动安装 | 要启动自动化安装，请将 XML 文件复制到包含 FAT 文件系统格式的软盘中。<br><br>提供所有网络信息的 DHCP 服务器和安装服务器可以简化安装。<br><br>在启动引导过程之前，将 CD 1 和软盘插入机器。<br><br>您还可以通过网络分发 XML 文件。 |

# 附录：将服务从 RedHat 迁移到 SUSE Linux Enterprise Server 10

以下各页的幻灯片来自 Brainshare 06 上的一次演示，涵盖了从 RedHat 迁移到 SUSE Linux Enterprise Server 10 时需要关注的不同要点。

这些幻灯片是在 SLES 10 发布之前制作的。虽然其中一些信息可能已过时，但它们仍包含许多您可能会觉得有用的技巧。

### 目标

1. 服务迁移

## 目标 1：服务迁移

### 图 B-1

![](img/63e88022bf135307e3eac051ad238b5b_469_0.png)

![](img/63e88022bf135307e3eac051ad238b5b_469_1.png)

![](img/63e88022bf135307e3eac051ad238b5b_470_0.png)

![](img/63e88022bf135307e3eac051ad238b5b_470_1.png)

### 图 B-4

![](img/63e88022bf135307e3eac051ad238b5b_471_0.png)

### 图 B-5

![](img/63e88022bf135307e3eac051ad238b5b_471_1.png)

允许硬拷贝 - 禁止分发

### 图 B-6

![](img/63e88022bf135307e3eac051ad238b5b_472_0.png)

### 图 B-7

![](img/63e88022bf135307e3eac051ad238b5b_472_1.png)

允许硬拷贝 - 禁止分发

### 图 B-8

### SLE 10 特性（续）

- 用于虚拟化配置的 YaST 模块

- 用于虚拟机（资源监控和管理）的 CIM 提供程序

- NFS 4.x 客户端和服务器

- AppArmor

- 改进的扩展性（1024 个 CPU、>10TB RAM、12000 个 LUN 等）

- Novell Linux 内核调试器（带 GUI）

- 适用于所有产品的统一 SDK

- Mono 2.x 和 Java 1.5 运行时环境

![](img/63e88022bf135307e3eac051ad238b5b_473_0.png)

### 图 B-9

### 新的服务器特性

- 增强的数据中心部署和管理

    - Xen 3 虚拟化

    - 对 Intel Vanderpool 和 AMD Pacifica 的支持极大地提高了系统利用率以及多核处理器的优化

    - 改进的性能和 SMP 扩展性

    - 先进的管理、仪表化和监控工具

- 扩展的硬件支持

    - 支持最新硬件：存储、网络、平台管理、图形、音频、蓝牙和 USB 设备

    - 增强的存储能力：集成 Oracle 集群文件系统 (OCFS)、EVMS 和 Heartbeat 的 HA 集群存储基础；NFS v4, iSCSI

> SUSE Linux Enterprise Server 是工程化做得最好的 Linux 服务器。是任务关键型工作负载的最佳选择。

![](img/63e88022bf135307e3eac051ad238b5b_473_1.png)

![](img/63e88022bf135307e3eac051ad238b5b_474_0.png)

- 新的最终用户生产力水平

- 强大的桌面生产力工具：电子邮件、桌面搜索、Firefox Web 浏览器、即时通讯、多媒体

- OpenOffice.org 2.0 办公套件和 Visual Basic 宏转换

- 易于学习的桌面环境，具有高级动画和渲染

- 与企业系统的无缝集成

- 对 USB 和蓝牙设备的硬件支持增强

- 与混合网络的无缝连接，包括 Novell eDirectory 和 Active Directory

- 打印机支持，包括自动驱动下载和安装，M5 打印机支持

- 灵活的部署选项

- 瘦客户端和胖客户端点击部署

- 轻松部署和桌面锁定

![](img/63e88022bf135307e3eac051ad238b5b_474_1.png)

- 订阅和更新服务

- 一个工具管理购买、续订、到期

- 轻松报告合规性并预测未来购买需求

- 集成的补丁管理和更新服务，由 ZENworks 提供支持

- 访问 Novell 支持

- 易于使用的支持门户

- 一个位置访问知识库、电子支持请求和下载

- 直观的管理控制台

- 一个控制台发现、更新和管理 Linux 系统

允许硬拷贝 - 禁止分发

### 图 B-12

![](img/63e88022bf135307e3eac051ad238b5b_475_0.png)

### 图 B-13

![](img/63e88022bf135307e3eac051ad238b5b_475_1.png)

### 图 B-14

### 一些差异（续）

- 应用程序安全（SELinux 和 AppArmor）

    - AppArmor 开销更低，不需要程序修改，且易于使用。

- 管理工具

    - `system-config-*` 对比 `yast`

- 更新方法

![](img/63e88022bf135307e3eac051ad238b5b_476_0.png)

### 图 B-15

### 一些相似之处

- 实际上技术上更相似而非不同

- 共享大量相同的代码...

- 都是基于 RPM 的发行版

- LSB/FSH 在此派上用场...了解 LSB 吗？

    - `http://www.linuxbase.org` - 去看看！

- 使用 `chkconfig`（用于设置每个运行级别的服务）并在 `/etc/init.d/*` 中有启动脚本

- 相同的 init 进程，两者都使用 `grub`

![](img/63e88022bf135307e3eac051ad238b5b_476_1.png)

允许硬拷贝 - 禁止分发

### 图 B-16

### 一些想法...

- 考虑多发行版环境，但可以自由标准化到一个

- 选择允许您在需要/想要时进行更改的基础设施部分/应用程序

- 竞争和灵活性是关键

- 没有它就无法避免供应商锁定

![](img/63e88022bf135307e3eac051ad238b5b_477_0.png)

### 图 B-17

![](img/63e88022bf135307e3eac051ad238b5b_477_1.png)

允许硬拷贝 - 禁止分发

### 图 B-18

### 迁移什么？
