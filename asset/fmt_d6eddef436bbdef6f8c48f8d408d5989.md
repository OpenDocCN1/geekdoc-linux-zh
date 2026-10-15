
当设备通过 IBM SAN Data Gateway 连接时，网关 SCSI 通道上的 SCSI 目标 ID 和 LUN 会重新映射到其他值，然后呈现给主机操作系统。

> 注意：IBM SAN Data Gateway 和 3583 SDG 模块已于 2004 年停止销售。

服务器启动时，连接到启动 I/O 扫描过程遇到的第一个网关的设备将被分配 SCSI ID 0（LUN 范围在 0-127 之间）；连接到第二个网关的设备具有 SCSI ID 1，依此类推。

> 重要：对于连接到服务器的每个 SDG，LUN 0 由网关本身使用，LUN 2–126 用于连接到网关的磁带设备。磁带驱动器被分配偶数 LUN，并从 2 开始。机械库将具有奇数号。

对于这些磁带设备，网关在其连接的 SCSI 通道上发现设备时顺序分配 LUN。

这意味着添加和删除设备、更改电缆以及重新分配地址可能会导致分配的 LUN 序列出现间隙，因为 LUN 号分配每次服务器重启时都会进行。此问题可以通过在光纤 HBA 上启用持久绑定来解决。有关持久绑定的更多详细信息，请参考第 237 页的节 5.3，“Persistent binding”。

## 使用 NTUTIL 更新微代码

`NTUTIL` 同样允许您更新驱动器微代码。请参考第 168 页的 3.9，“Updating library, drive, and RMU firmware”以获取操作说明。

## 3.5.5 删除 LTO 设备

您可能需要从 Windows 设备配置中删除磁带设备或机械库。对于某些需要为机械库或磁带驱动器特定设备驱动程序的应用程序来说，这是必要的。您可能还想禁用驱动器，可能是出于故障排除的目的。在本节中，我们将描述如何在 Windows 200x 中禁用 IBM 磁带设备，以及如何删除设备驱动程序。

### 禁用磁带机械库或磁带驱动器

要在 Windows 200x 中禁用 IBM 磁带设备，打开设备管理器，找到该设备（在此情况下，位于“机械库”或“磁带驱动器”下），右键点击设备并选择“禁用”。或者，您也可以在设备属性的“常规”选项卡下进行操作。如图 3-71 所示。

![](img/a48407b38d72fd58ea3627423836388a_161_0.png)

图 3-71 禁用 IBM 磁带设备

### 禁用 RSM

我们建议在移除 Ultrium 设备之前从服务中禁用 RSM（选择开始 -> 程序 -> 管理工具 -> 服务，如第 135 页图 3-72 所示）。在执行此步骤之前，请确保所有设备活动已停止。

### 服务

| 名称 | 描述 | 状态 | 启动类型 | 登录身份 |
| --- | --- | --- | --- | --- |
| Performance Logs and Alerts | Configures perfo... | Started | Manual | LocalSys... |
| Plug and Play | Manages device... | Started | Automatic | LocalSys... |
| Print Spooler | Loads files to... | Started | Automatic | LocalSys... |
| Protected Storage | Provides network... | | Automatic | LocalSys... |
| OLE Auto Admission Control (RSVP) | Creates a connect... | | Manual | LocalSys... |
| Remote Access Connection... | Manages the map... | | Automatic | LocalSys... |
| Remote Procedure Call (RPC) | Provides the end... | | Automatic | LocalSys... |
| Remote Registry | Manages remova... | | Manual | LocalSys... |
| Remote Storage | Stores security in... | Started | Disabled | LocalSys... |
| Routing and Remote Access | Enables starting... | Started | Automatic | LocalSys... |
| RunAs | Supports the foll... | | Automatic | LocalSys... |
| Security Accounts Manager | Provides support... | | Manual | LocalSys... |
| Smart Card | Manages and... | | Manual | LocalSys... |
| Smart Card Helper | Includes t... | Started | LocalSys... |
| SNMP Service | Man | | Automatic | LocalSys... |
| Service | | | Manual | LocalSys... |
| Service | | | Automatic | LocalSys... |
| Service | | | Manual | LocalSys... |
| Service | | | Automatic | LocalSys... |
| Stopped | | | Manual | LocalSys... |
| Startup type | | | Automatic | LocalSys... |
| Startup type | | | Manual | LocalSys... |
| Service | | | | | LocalSys... |
| | | | | ||Sys... |
| | | | | | |
| Removable Storage | | | Manual | LocalSys... |
| Removable Storage | | | Automatic | LocalSys... |
| Removable Storage | | | Manual | LocalSys... |
| Removable Storage | | | Automatic | LocalSys... |
| Removable Storage | | | Manual | LocalSys... |
| | | | | | |
| Display name | | | Manual | LocalSys... |
| Display name | | | Automatic | LocalSys... |
| Display name | | | Manual | LocalSys... |
| Display name | | | Automatic | LocalSys... |
| Display name | | | Manual | LocalSys... |
| | | | | | |
| Path to | | | Manual | LocalSys... |
| Path to | | | Automatic | LocalSys... |
| Path to | | | Manual | LocalSys... |
| Path to | | | Automatic | LocalSys... |
| Path to | | | Manual | LocalSys... |
| | | | | | |
| Description | Configures perfo... | Started | Manual | LocalSys... |
| Description | Manages device... | Started | Automatic | LocalSys... |
| Description | Loads files to... | Started | Automatic | LocalSys... |
| Description | Provides network... | | Automatic | LocalSys... |
| Description | Creates a connect... | | Manual | LocalSys... |
| Description | Manages the map... | | Automatic | LocalSys... |
| Description | Provides the end... | | Automatic | LocalSys... |
| Description | Manages remova... | | Manual | LocalSys... |
| Description | Stores security in... | Started | Disabled | LocalSys... |
| Description | Enables starting... | Started | Automatic | LocalSys... |
| Description | Supports the foll... | | Automatic | LocalSys... |
| Description | Provides support... | | Manual | LocalSys... |
| Description | Manages and... | | Manual | LocalSys... |
| Description | Includes t... | Started | Automatic | LocalSys... |
| Description | | | Manual | LocalSys... |

...（下文）

- Device found: Changer0@Scsi Port 3\Scsi Bus 1\Target ID 0\Logical Id 1
- Device found: Tape0@Scsi Port 3\Scsi Bus 1\Target ID 0\Logical Id 2
- Device found: Tape1@Scsi Port 3\Scsi Bus 1\Target ID 0\Logical Id 4

## IBM 磁带驱动程序

要从系统中删除 IBM 磁带驱动程序，请执行以下操作：

1. 打开设备管理器并右键点击设备（图 74）。
2. 点击**卸载**。您将看到一个窗口确认您是否真的要卸载该设备。点击 **OK** 继续。
3. 在驱动程序解压的目录中运行 `uninst.exe`（图 75）。
4. 关闭操作系统并根据需要物理上断开库库连接。Uninstall.exe 不会删除 .zip 文件或从 .zip 文件中提取的文件。如果您想删除这些文件，则需要手动操作。

## Windows 200x SCSI 适配器

为了说明这种技术，我们使用直接通过 SCSI 连接到 Windows Intel 服务器的 IBM 3583 库，如图 3-78 所示。安装包括：

- 带有 Windows 2000 Server 的 Intel 服务器
- Adaptec 29160 LVD SCSI 适配器
- 带有 LVD 驱动器的 IBM 3583

![](img/a48407b38d72fd58ea3627423836388a_164_1.png)

关于 SCSI 接口和连接器类型的附加信息可以参阅：

- 第 33 页，1.7，“LVD 和 HVD”
- 第 34 页，1.8，“SCSI HD68 和 VHDCI 线连接器”

对于 Adaptec 设备，我们建议您从 Adaptec 网站获取 SCSI 适配器的最新驱动程序和固件更新：

```
```
