
![](img/7489105e357b7dff3e56cd1cbb0de4fa_43_0.png)

图 2.2：DEFT Linux 启动菜单

从 DEFT Linux DVD、启动闪存或其他介质启动时，你会看到各种选项，包括将 DEFT Linux 安装到硬盘、作为现场响应工具或作为操作系统使用，通过选择 DEFT Linux 8 选项，如下所示：

![](img/7489105e357b7dff3e56cd1cbb0de4fa_44_0.png)

图 2.3：DEFT Linux 菜单

在之前的截中可以看到 DEFT Linux 8 中有多个取证类别，例如反恶意软件、数据恢复、哈希、镜像、移动取证、网络取证、密码恢复和报告工具。每个类别中都存在多种工具。

# 数字取证操作系统对比

![](img/7489105e357b7dff3e56cd1cbb0de4fa_45_0.png)

图 2.4：DEFT Linux 菜单

![](img/7489105e357b7dff3e56cd1cbb0de4fa_46_0.png)

图 2.5：CAINE 启动菜单

# 数字取证引论

![](img/7489105e357b7dff3e56cd1cbb0de4fa_47_0.png)

图 2.6：CAINE 12 界面

# 数字取证操作系统对比

让我们来看看 CAINE 中“分析”`Analysis`菜单下的工具。正如之前看到的，DEFT 中有更多的图形用户界面`GUI`数字取证与响应`DFIR`工具：

![](img/7489105e357b7dff3e56cd1cbb0de4fa_49_0.png)

图 2.10：CAINE 12 中提供的分析工具

我们在 CAINE 的“内存取证”`Memory forensics`菜单中也有多种可用工具：

![](img/7489105e357b7dff3e56cd1cbb0de4fa_49_1.png)

图 2.11 – CAINE 12 中提供的内存取证工具

如需查看发布时 CAINE 包含的特性和软件包完整列表，请访问 `http://www.caine-live.net/page11/page11.html`。

# 数字取证简介

最新版本的 CAINE 12.4 Sidereal 可以从 `https://deb.parrot.sh/direct/parrot/iso/caine12.iso` 下载（ISO 格式），大小约为 3.9 GB。

如前所述，如果你想使用可安装的 CAINE 11 Wormhole，可以从 `https://deb.parrot.sh/direct/parrot/iso/caine/caine12.4.iso` 下载。

若要在 USB 驱动器上进行安装，请确保驱动器容量不少于 8 GB；不过，可以使用 `Rufus` 工具自动创建可启动的 Kali Linux，如第 3 节“安装 Kali Linux”所示。

# CSI Linux

CSI Linux 在该领域相对较新，由富有远见的 Jeremy Martin 及其出色的团队开发。他们整合了一个极其稳健的取证/蓝队对抗平台，我使用它的频率经常与 Kali Linux 一样高。CSI Linux 2022.1 提供了适用于 VirtualBox 和 Kali Linux 的虚拟机设备安装版本，也可以作为用于实时 DFIR 的启动镜像下载。此外还计划在近期发布 CSI Linux 安全信息和事件管理`SIEM`系统。

CSI Linux 2022.1 可以直接从 `https://csilinux.com/download` 下载。

> 友好提示
> 
> 如果使用 CSI Linux，用户名和密码均为 `csi`。

![](img/7489105e357b7dff3e56cd1cbb0de4fa_50_0.png)

图 2.12：CSI Linux 登录界面

与 DEFT、CAINE 和 Kali 类似，CSI Linux 拥有非常用户friendly桌面界面：

![](img/7489105e357b7dff3e56cd1cbb0de4fa_51_0.png)

图 2.13：CSI Linux 桌面界面

点击 CSI Linux 菜单按钮会显示详尽的分类列表，包括开源情报`OSINT`与在线调查、暗网以及威胁情报类别。在我看来，这是 CSI Linux 真正闪光的地方，因为其他平台缺乏这些预装工具：

![](img/7489105e357b7dff3e56cd1cbb0de4fa_52_0.png)

再次为了对比，让我们来看看 `OSINT` 与在线调查、暗网 以及 `计算机取证` 菜单。

OSINT 与在线调查菜单包含多个子菜单，其中有针对社交媒体、电子邮件、电话和社交工程的非常实用的工具，这些工具我经常使用：

图 2.14：CSI Linux 取证工具

![](img/7489105e357b7dff3e56cd1cbb0de4fa_53_0.png)

图 2.15：CSI Linux OSINT 与在线调查工具

`暗网`调查工具在紫队对抗`purple teaming`中也广受欢迎，因为渗透人员和 DFIR 从业者都会使用它们：

# 数字取证简介

![](img/7489105e357b7dff3e56cd1cbb0de4fa_54_0.png)

图 2.16：CSI Linux 暗网调查工具

“计算机取证与事件响应”中包含了大量更新的现代图形用户界面`GUI`和命令行界面`CLI`工具，用于进行全面调查：

![](img/7489105e357b7dff3e56cd1cbb0de4fa_54_1.png)

图 2.17：CSI Linux 计算机取证工具菜单

# 数字取证操作系统对比

CSI Linux 在事件响应工具方面拥有令人印象深刻的分类列表，如图 2.18 所示：

![](img/7489105e357b7dff3e56cd1cbb0de4fa_55_0.png)

图 2.18：CSI Linux 事件响应菜单

我强烈建议下载并熟悉 CSI Linux。我们在本书中将学习使用的许多工具也安装在 CSI Linux 中，从而降低了学习曲线。

# Kali Linux

最后，我们将在下一章以及整本书中对这颗可爱的明珠——Kali Linux 进行详细讨论，从其安装到高级取证用法应涵盖：

- 首页：`https://www.kali.org/`
- 基于：Debian
- 分发版类型：渗透测试、取证和反取证

Kali Linux 是作为渗透测试工具创建的，在 2015 年更名为 BackTrack，后来演变为 Kali Linux。正如第 1 节“红蓝紫队对抗基础”提到的，它是渗透测试人员和安全爱好者的首选。它包含了从扫描、侦察到漏洞利用和报告的各种强大工具。

# 数字取证简介

与上述工具类似，Kali Linux 也可以作为实时响应工具使用，它包含了成功调查所需的许多工具。然而，Kali 还提供了移动设备（如 Nexus 和平板电脑）的许多工具。

值得注意的是，当 Kali 处于取证模式时，它不仅不会篡改原始数据，也不会将数据写入交换文件`swap file`，而最近访问并存储在内存中的数据可能位于此处。

当从 DVD 或闪存驱动器启动 Kali Linux 时，用户将看到安装选项。如下图所示：

![](img/7489105e357b7dff3e56cd1cbb0de4fa_56_0.png)

图 2.19：Kali 启动菜单

一旦启动 Kali 取证选项，调查人员将看到与任何 GUI 相同的主界面，如下所示：

# 数字取证操作系统对比

![](img/7489105e357b7dff3e56cd1cbb0de4fa_57_0.png)

图 2.20：Kali Linux 桌面

当然，Kali 也可以作为完整的操作系统安装在虚拟机或直接安装在硬盘上，这将在第 3 节“Linux”中介绍。这里是我的桌面场景，其中通过 `Wine` 安装了一些取证工具，例如 `FTK Imager` 和 `Autopsy` 图形界面：

![](img/7489105e357b7dff3e56cd1cbb0de4fa_57_1.png)

图 2.21：Kali Linux 定制桌面

## 数字调查中对多种取证工具的需求

Kali 可以作为实时响应取证工具运行，也可以作为一个完整的操作系统（如 Windows、macOS 和 Android）使用，因为它包含了多个用于生产力和日常使用的内置工具。Kali 可以安装在硬盘上，这一事实意味着可以定期下载并更新其他许多工具，从而确保能够持续访问所有的 IT 安全和取证工具。这允许你在使用工具时保存进度，而无需过于担心重启机器；你应该考虑将其作为一个完整的操作系统来使用。
