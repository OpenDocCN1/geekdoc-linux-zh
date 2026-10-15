
![](img/7df754bba6e7faadf914690e9e5ed087_84_0.png)

**图 3-27** 保存设置

SuSE Linux Enterprise Server 的安装完成。系统已运行并允许授权用户登录。

下一节将描述如何向系统添加光纤（Fibre Channel）连接存储。

## 3.5 Linux 下的 zSeries FCP 和磁盘存储

在本节中，我们关注引言中提到的通过光纤连接磁盘存储。

> **重要：** 市场上存在大量的 SCSI 设备。IBM 无法对所有这些设备进行完全测试以供 zSeries 系统使用。IBM 支持的设备与已使用且看起来工作正常但未被 IBM 正式支持 zSeries FCP 的设备之间存在区别。要获取支持设备的列表，请参阅：http://www-ibm.com/servers/eserver/zseries/connectivity/#fcp

### 3.5.1 使用 FCP 的 ESS

本节参考第 38 页 3.3 节“本红书使用的配置”中的物理设置。在这里我们讨论以下内容：

- 收集有关 SAN 设置的先决信息
- 设置 ESS 并为 zSeries 的 Linux 配置 LUN
- 手动加载所需的模块和参数以访问磁盘
- 使磁盘变为永久可用

### 先决信息

从软件配置的角度来看，你需要收集第 29 页 3.1.2 节“分布式存储连接”中描述的以下信息元素，以便准备 Linux 系统通过光纤访问企业级存储服务器（ESS）：

- 托管 Linux 系统的服务器主机名
- 连接到 Linux 的 FCP 端口设备地址 (`CHPID`)
- zSeries 上 FCP 端口的世界端口名称 (`WWPN`)
- ESS 上的 FC 端口
- ESS 上 FC 端口的世界端口名称

你可以从 HMC、ESS 专家以及 McData 交换机获取数据；在我们的案例中：

| 描述 | 值 |
| :--- | :--- |
| 托管 Linux 系统的服务器主机名 |  |
| 连接到 Linux 的 FCP 端口设备地址 (`CHPID`) |  |
| zSeries 上 FCP 端口的世界端口名称 (`WWPN`) |  |
| ESS 上的 FC 端口 |  |
| ESS 上 FC 端口的世界端口名称 |  |

（注：后续表格数据由于原文重复，此处省略重复翻译保持逻辑一致）

### 设置 Linux 系统

为了使用 FCP 设备访问 ESS，你必须安装以下模块：

- `qdio` - 该模块也用于其他 qdio 设备
- `scsi_mod` - SCSI 核心
- `zfcp` - 为 zSeries Linux 提供 FCP 支持
- `sd_mod` - SCSI 磁盘支持

模块应按列出的顺序加载。所有模块都可以通过 `modprobe` 加载。还存在针对其他 SCSI 设备的 SCSI 模块，例如磁带支持、用于 CD/DVD（只读）支持的 `sr_mod`。这些模块已测试可以在不同设备上工作，但书中将进行讨论。请参考红皮书《Getting Started with z Fibre Channel Protocol》，REDP-0205。

除 `zfcp` 外，所有模块都可以在不带参数的情况下加载。对于 `zfcp` 模块，需要 ESS 上 FCP 设备映射的参数。设备所需的参数为：

- zSCSeries 上 FCP 端口的设备号
- 从 1 开始的 SCSI ID
- ESS FC 端口的 `WWPN`
- Linux 内部从 0 开始的 SCSI LUN
- 目标模块到 ESS 的 FCP LUN

向模块提供参数的格式如下：

```
map="devno SCSI_ID:WWPN SCSI_LUN:FCP_LUN" 例如：
map="0x0600 1:0x505076300c89589 0:53310000000000000"
```

若要向模块添加更多设备，只需在参数行中添加更多语句并用分号隔开。接下来的示例显示了一个卷的模块加载（省略了 `qdio` 模块，因为它在我们的安装中已被 OSA Express 适配器使用并加载了）。

#### 示例 3-8 加载 scsi_mod 和 zfcp 模块

```
vmlinux:~# modprobe scsi_mod
vmlinux:~# modprobe zfcp map="0x0600 1:0x505076300c89589 \
0:5x331000000000000"

vmlinux:~# cat /proc/scsi/scsi
Attached devices:
Host:scsi0 Model: 21 Id: 01 Lun: 00
Vendor: IBM Model: 2105800  Rev: .101
Type: Direct-Access  ANSI SCSI revision: 03
vmlinux:~# modprobe sd_mod
vmlinux:~# cat /proc/partitions
```

| major name | blocks | rio | riomerge | rset | ruse | we | merge | wct | we | running | use | aeq |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 8 | 79926896 | da6 | 2 | 16 | 1 | 0 | 0 | 0 | 0 | 0 | 10 |  |
| 0 | 2259360 | da54 | 24 | 799 | 32810 | 460072 | 116350 | 34395 | 47194 | 654280 | 738410 | 0 | 175040 | 854800 |
| 9 | 2259264 | da7 | 24 | 78 | 32810 | 460274 | 116374 | 34395 | 47194 | 654280 | 738410 | 0 | 175000 | 854976 |
| 4 | 1460000 | da5b | 10 | 5 | 1264 | 86 | 0 | 0 | 0 | 0 | 80 | 80 |  |
| 4 | 2032064 | da5b | 32 | 15 | 2 | 99 | 46 | 0 | 0 | 0 | 40 | 40 |  |

示例显示了新的 SCSI 设备 `da` 是被系统访问的。但在在使用新卷之前，必须使用 `fdisk` 对其进行分区。

### 在 Linux 中实现 IBM 磁盘

对新卷分区后，可以使用命令行工具或 YaST 在分区上创建文件系统。在我们的案例中，分配了挂载点，格式化了 ext3 文件系统并应用了更改。现在新设备可以使用。

有关分区磁盘和创建文件系统的详情，请参考附录 A。

### 添加设备并持久化更改

要向 SCSI 配置添加多个设备，方便的方法是编写一个如示例 3-9 所示包含所有参数的小脚本。

#### 示例 3-9 模块加载

```
vmlux:~# cat scsi.sh
modprobe scsi_mod
modprobe zfcp map="0x0600 1:0x500505070c89589 0:0x530100000000000
0x0600 1:0x500505070c89589 1:0x530200000000000
0x0600 1:0x500505070c89589 2:0x530300000000000"
modprobe sd_mod
```

在执行脚本之前，确保模块已卸载。

#### 示例 3-10 模块加载

```
vmlux:~# sh scsi.sh
vmlux:~# cat /proc/scsi/scsi
Attached devices:
Host:scsi0 Channel: 00 ID: 01 Lun: 00
Vendor: IBM Model: 2105800
Type: Direct-Access Rev: .101
ANSI SCSI revision: 03
Host:scsi0 Channel: 00 ID: 01 Lun: 01
Vendor: IBM Model: 2105800
Type: Direct-Access Rev: .101
ANSI SCSI revision: 03
Host:scsi0 Channel: 00 ID: 01 Lun: 02
Type: 
```

或者，你也可以通过 `add_map` 向现有配置添加 SCSI 设备。然后你必须如示例 3-11 所示让 SCSI 栈识别这些设备。

#### 示例 3-11 通过 add_map 添加设备
