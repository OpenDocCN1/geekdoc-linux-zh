
http://www.adaptec.com/worldwide/support/suppupplyproduct.jsp?fromPage=driverindex&cat=%25Ftechnology%25FSCI+Host+Adapters

我们的配置使用了 Adaptec 29160 (LVD)。安装在 Windows 2000 机器上时，Windows 2000 会检测到卡并自动加载驱动程序。不过，您可以从 Adaptec 网站将适配器更新到更高的驱动版本。

> 注意：本节包含的屏幕是在 Windows 2000 系统上获取的。Windows 2003 的屏幕可能会略不同。

### 安装步骤

1. 您需要关闭系统以安装该卡。当 Windows 启动时，它会提示您重启（如图 3-79 所示），因为它已经加载了驱动程序。

![](img/a48407b38d72fd58ea3627423836388a_165_0.png)

图 3-79 系统设置更改

2. 选择“是”重启以进行清洁安装。重启后，您可以使用“设备管理器”更新到更高版本的设备驱动程序。右键点击“我的电脑”，选择“设备管理器 -> SCSI 和 RAID 控制器”，右键点击要更新的 SCSI 卡（在我们的示例中为 Adaptec SCSI 卡），并选择“属性”，如图图 3-80 所示。

![](img/a48407b38d72fd58ea3627423836388a_165_1.png)

图 3-80 访问 SCSI 控制器属性

3. 在属性窗口中（第 139 页的图 3-81），点击“驱动程序”选项卡并选择“更新驱动程序”。

![](img/a48407b38d72fd58ea3627423836388a_166_0.png)

图 3-81 Adaptec 属性。驱动程序选项卡

4. 升级设备驱动程序向导启动，如图 3-82 所示。点击`下一步`开始。

![](img/a48407b38d72fd58ea3627423836388a_166_1.png)

图 3-82 升级设备驱动程序向导

5. 系统提示您要搜索设备驱动程序还是显示已知的驱动程序列表（第 140 页的图 3-83）。选择`搜索`选项并点击`下一步`。

# 升级设备驱动程序向导

### 安装硬件驱动程序
驱动程序是一种使硬件设备能够与操作系统工作的软件程序。

向导程序为以下硬件设备升级驱动程序：

- Adaptive AIC-7992 UBA/166b/PCI SCSI 卡

升级到设备驱动程序的新版本可能起到提高此设备性能的功能。

您想做什么？

- 为我的设备搜索适当的驱动程序（推荐）
- 显示此设备的已知驱动程序列表，以便我选择特定的驱动程序

![](img/a48407b38d72fd58ea3627423836388a_167_0.png)

**图 3-83** 设备驱动程序搜索选项检查位置

6. 在查找文件窗口中（图 3-84），勾选`指定位置`。

![](img/a48407b38d72fd58ea3627423836388a_167_1.png)

**图 3-84** 设备驱动程序搜索位置

7. 指定用于升级的驱动程序文件位置（图 3-85）。这可以是光光形驱动器（如果使用了 CD 盘）或您下载设备驱动程序的目录。

![](img/a48407b38d72fd58ea3627423836388a_167_2.png)

**图 3-85** 设备驱动程序复制位置

8. 搜索结果窗口出现（第 141 页的图 3-86）。点击`下一步`。

# 升级设备驱动程序向导

### 驱动文件搜索结果
向导已完成对您的硬件设备驱动文件的搜索。请等待，向导正在为以下硬件设备搜索驱动程序文件：
Adaptec AIC-7992 Uba160m/n PCI SCSI 卡
搜索位置：
`C:\Windows\Inf`

![](img/a48407b38d72fd58ea3627423836388a_168_0.png)

9. 图 3-87 显示比当前安装的驱动程序更新版本。点击下一步。

![](img/a48407b38d72fd58ea3627423836388a_171_0.png)

点击 `Connect` 并输入您想要连接的主机或 IP 地址。默认情况下，它将查找本地主机适配器和发现的设备。您也可以指定备用 SANSurfer 主机，允许其连接、显示和控制另一个主机的 HBA 和设备。所有配置的 HBA 将如图 3-90 所示。我们的配置包含一个 QLA2300 适配器。

![](img/a48407b38d72fd58ea3627423836388a_171_1.png)

图 3-90 带 HBA 的 SANBlade Manager

点击 `Configure` 显示 HBA 的详细窗口（见图 3-91）。现在可以对 HBA 进行配置/关联连接的 SAN 设备。

![](img/a48407b38d72fd58ea3627423836388a_172_0.png)

图 3-91 配置 SAN 设备

默认情况下，启用自动配置路径。此选项将列出主机可见的所有 SAN 连接设备。将显示 WWN、WWPN、端口 ID 和拓扑结构。我们建议配置持久绑定，将在下一节中进行详细说明。

在配置完所有所需设备后，应用并保存配置。HBA 设备现在显示在 HBA 树中（见图 3-92）。

![](img/a48407b38d72fd58ea3627423836388a_172_1.png)

图 3-92 已配置的设备

从左侧列表中选择单个 SAN 设备将显示常规信息（第 146 页图 3-93）。

第 3 章 Windows 基础 IBM 带机设置 145

图 3-93 SAN 设备详情

还可以根据连接到 HBA 的设备类型修改 HBA 的设置。从 SANSurfer GUI 中选择 Settings 选项卡以修改默认参数。

我们勾选了 Enable Fibre Channel Tape Support（图 3-94）。

![](img/a48407b38d72fd58ea3627423836388a_173_0.png)

图 3-94 SANSurfer Settings 选项卡

146 在 Linux 和 Windows 中实现 IBM 带

从下拉菜单中选择 Advanced HBA Port Settings 以修改其他参数。如果连接带有多 LUN 架构的 IBM 带库，每个目标的 LUN 数量（LUNs per Target）必须大于零（见图 3-95）。

![](img/a48407b38d72fd58ea3627423836388a_174_0.png)

图 3-95 SANSurfer Advanced Adapter Settings

指定所需设置后，点击 Save 并输入密码（默认密码为 `config`）。您需要重启以启用更改。

还有其他可以设置的功能和选项。请参考《SANblade Host Bus Adapters User's Guide》适用于您特定的 HBA，该指南位于：

http://www.qlogic.com/support/drivers/software.app

# IBM Tivoli Storage Manager 用户说明

为了允许 HBA 在使用 IBM Tivoli Storage Manager 时正确处理较大的块大小，请修改 Windows 注册表下的 `MaximumSGList`：

```
HKEY_LOCAL_MACHINE->SYSTEM->Current Set->Services->vendor device name->Parameters->Device
```
