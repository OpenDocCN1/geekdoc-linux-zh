
1996年4月16日

Leonard N. Zubkoff
Dandelion Digital
lnz@dandelion.com

BusLogic, Inc 设计并制造多种高性能 SCSI 适配器，由于采用了 MultiMaster ASIC 技术，这些产品在不同的总线架构之间共享公共编程接口。此驱动支持所有的 BusLogic MultiMaster 主机适配器，并可以在很少或不修改的情况下支持未来的 MultiMaster 适配器。此驱动不支持基于新的 FlashPoint 架构的主机适配器；请咨询 `README.FlashPoint` 获取有关将 Linux 用户从不支持的 FlashPoint LT 升级到支持的 BT-948 的程序信息。

我编写这个全新的 Linux BusLogic 驱动的首要目标是实现 BusLogic SCSI 主机和现代外设能够实现的全部性能，并提供一个高度可靠的、可用于高性能关键任务应用程序的驱动程序。所有主要的性能和错误恢复功能都可以从 Linux 内核命令行进行配置，允许单独的的用户根据特定需求调整驱动性能和错误恢复。

BusLogic 是一家非常出色的合作公司，我强烈向 Linux 社区推荐他们的产品。1995 年 11 月，我有机会对他们最新的 MultiMaster 产品 BT-948 PCI SCSI 主机适配器进行 Beta 测试，随后于 1996 年 1 月对 BT-958 PCI 宽型 Ultra SCSI 主机适配器进行测试。由于是互利共利的，因为 BusLogic 获得了其内部测试小组无法轻易实现的某种程度和类型的测试，而 Linux 社区也获得了在上市前已过良好 Linux 测试的高性能主机适配器。这种关系也让我有机会直接与他们的技术人员交流，更深入地了解他们产品的内部工作原理，反过来向他们介绍 Linux 社区的需求和潜力。非常感谢他们的关注和支持。

与其他供应商不同，如果你在运行 Linux 时遇到问题并联系 BusLogic 技术支持，他们不会告诉你你使用他们的产品是不支持的。他们最新的产品营销材料指出“BusLogic SCSI 主机适配器兼容所有主流操作系统，包括：Linux...”。

BusLogic, Inc. 位于 4151 Burton Drive, Santa Clara, California, 95054, USA，可以通过电话 408/492-9090 或传真 408/492-1542 联系他们。BusLogic 在 `http://www.buslogic.com` 维护了一个全球网站，在 `ftp.buslogic.com` 维护了一个匿名 FTP 站点，并在 408/492-1984 维护了一个 BBS。BusLogic 技术支持可以通过电子邮件 techsup@buslogic.com 联系，或通过电话 408/654-0760 联系。在欧洲和日本的联系方式可在网站上查阅。

# 支持的适配器

以下列表包含了截至本文发布日期支持的 BusLogic SCSI 适配器。建议购买下表之外 BusLogic 主机适配器的人先联系作者以确认其是否支持。

'W' 系列适配器：

| 模型 | 接口 | 类型 |
| --- | --- | --- |
| BT-948 | PCI | Fast-ended SCSI-2 |
| BT-958 | PCI | Ultra Wide-ended SCSI-2 |
| BT-958D | PCI | Differential SCSI-2 |

'C' 系列适配器：

| 模型 | 接口 | 类型 |
| --- | --- | --- |
| BT-946C | PCI | Fast-ended SCSI-2 |
| BT-956C | PCI | Ultra Wide-ended SCSI-2 |
| BT-956D | PCI | Differential SCSI-2 |
| BT-445C | VLB | Fast-ended SCSI-2 |
| BT-747C | EISA | Fast-ended SCSI-2 |
| BT-757CD | EISA | Fast Wide-ended SCSI-2 |
| BT-757CD | EISA | Differential SCSI-2 |
| BT-545C | ISA | Fast-ended SCSI-2 |
| BT-540CF | ISA | Fast-ended SCSI-2 |

'S' 系列适配器：

| 模型 | 接口 | 类型 |
| --- | --- | --- |
| BT-645S | VLB | Fast-ended SCSI-2 |
| BT-747S | EISA | Fast-ended SCSI-2 |
| BT-747D | EISA | Differential SCSI-2 |
| BT-757S | EISA | Differential SCSI-2 |
| BT-757D | EISA | Differential SCSI-2 |
| BT-545S | ISA | Fast-ended SCSI-2 |
| BT-542D | ISA | Differential SCSI-2 |
| BT-742A | EISA | Single-ended SCSI-2 (742A revision H) |
| BT-542B | ISA | Single-ended SCSI-2 (542B revision H) |

'A' 系列适配器：

| 模型 | 接口 | 类型 |
| --- | --- | --- |
| BT-742A | EISA | Single-ended SCSI-2 (742A revisions A - G) |
| BT-542B | ISA | Single-ended SCSI-2 (542B revisions A - G) |

驱动支持真正的 BusLogic 克隆 AMI 磁盘主机适配器。

# 安装说明

## 主机

BT-948/958/958D PCI Ultra SCSI 适配器在安装 Linux 时某些功能需要注意。

### I/O 端口分配

当配置为出厂设置设置，BT-948/958/958D 只识别主板 BIOS 的 PCI I/O 端口分配。BT-948/958/958D 不响应以前 BusLogic SCSI 适配器响应的任何 ISA 端口。此驱动支持 PCI 配置，如果由于任何原因（例如 Linux 发行版在其引导内核中未使用此驱动），BusLogic 提供了一个 AutoSCSI 配置选项来启用旧 ISA 端口。

要启用此后兼容选项，请在系统启动时通过 `Ctrl-B` 调用 `AutoSCSI` 工具，选择“Adapter Configuration”、“View/Modify Configuration”，然后将“ISA Compatible Port”设置从“Disable”更改为“Alternate”。一旦安装此驱动，应将“ISA Compatible Port”选项设回“Disable”以避免可能的 I/O 端口冲突。较老的 BT-946C/956C/956CD 也有此配置选项，但出厂默认设置为“Primary”。

### PCI 插槽扫描顺序

在带有多个 BusLogic PCI 主机适配器的系统中，BT-948/958/958D 的 PCI 插槽扫描顺序可能与 BT-946C/956C/956CD 反。主机适配器 BIOS 和内核一致才能正确从 SCSI 磁盘启动，确定哪个磁盘是启动设备，这要求它们以相同的顺序识别 PCI 主机适配器。主板 PCI BIOS 提供了一种枚举 PCI 主机适配器的标准，Linux 内核使用该方法。某些 PCI 实现按照编号和设备顺序枚举 PCI 插槽，而另一些则相反。

遗憾的是，微软发现 Windows 95 无论 PCI 枚举如何，始终按照编号和设备顺序枚举 PCI 插槽，并要求主机适配器 BIOS 支持其方案以获得 Windows 95 认证。BT-948/958/958D 的出厂设置按照编号和设备顺序枚举主机适配器。要禁用此功能，请在系统启动时通过 `Ctrl-B` 使用 `AutoSCSI` 工具，选择“Adapter Configuration”、“View/Modify Configuration”，按下 `Ctrl-F10`，然后将“Use Bus And # For PCI Scanning Seq.”改为 OFF。

此驱动将查询 PCI 顺序选项的设置，以便以主机适配器 BIOS 枚举相同的顺序识别主机适配器。

# BUSLOGIC 公告邮件列表

BusLogic 公告邮件列表提供了一个论坛，通知 Linux 用户新发布以及关于 BusLogic SCSI 适配器 Linux 支持的其他公告。要加入邮件列表，请向以下地址发送消息：

发送至 'BusLogic-announce-request@dandelion.com'，邮件正文包含 'subscribe' 行。

## BusLogicPoint 主机适配器

(版权所有 1995 Leonard N. Zubkoff <inz@dandelion.com>)

目前没有可用的 FlashPoint LT/DL/LW (BT-930/932/950) Linux 驱动程序，尚不清楚未来是否会提供。FlashPoint 板的架构与 MultiMaster 板不同，它们没有板载 CPU，只有一个 SCSI 序器引擎。它们被定位为桌面工作站产品，并不特别适用于 Linux 这种高性能多任务操作系统。

MultiMaster BT-948/958 带有板载 CPU，其邮箱接口允许操作系统与主机适配器之间进行并行处理和流水线操作，而 FlashPoint 板则需要频繁的干预。在负载的多任务系统中，随着中断延迟的增加，BT-948/958 应该能保持卓越性能，而 FlashPoint 的性能可能会迅速下降。此外，BT-948/958 的固件包含了与 SCSI 总线进行正确交互的底层知识，而使用序器时，Linux 驱动程序必须包含部分或全部此类信息，并且解决所有小问题通常需要很长时间。鉴于这些产品的市场价格差异相对较小，BT-948 或 BT-958 显然是 Linux 的更好选择。

### 公告
BusLogic FlashPoint/BT-948/958 升级计划
1996年2月1日

自去年 10 月推出以来，BusLogic FlashPoint LT 一直令 Linux 社区的成员感到困扰，因为这种新的 Ultra SCSI 产品没有提供 Linux 驱动程序。尽管它官方定位为桌面工作站产品，且并不适用于像 Linux 这样高性能的多任务操作系统，但 FlashPoint LT 仍然被计算机系统供应商进行了测试，并销售在他们的高端型号中，排挤了旧的 MultiMaster 产品。这给许多人带来了困扰，他们无意中购买了系统，本以为所有的 BusLogic SCSI 适配器都受 Linux 支持，结果发现 FlashPoint 不支持，而且在很长一段时间内都不会支持，甚至永远不会支持。

在发现这一问题后，BusLogic 联系了其 OEM 客户，以确保继续生产 BT-94GC/956C MultiMaster 卡，并让误订了带有 FlashPoint 系统的 Linux 用户能够升级到 BT-94GC。虽然这帮助了许多新系统的购买者，但对于 Linux 用户支持 FlashPoint 的整体问题来说，这只是部分解决方案。对于那些最初购买 FlashPoint 是为了支持的操作系统、后来决定运行 Linux 的人，或者那些因为认为 FlashPoint 受支持而购买后却无法退货的人来说，这没有任何帮助。

## 回应

在 12 月中旬，我请求与 BusLogic 的高级管理层会面，讨论与 FlashPoint 相关的 Linux 和自由软件支持问题。关于 BusLogic 对 Linux 社区的态度，公开场合一直流传着各种准确性不一的传言，我觉得直接解决这些问题是最好的。我在某一天晚上 11 点后发了那封信息，会议在第二天下午举行了。遗憾的是，公司机构的轮子运转得非常缓慢，尤其是当一家公司正被收购时，所以直到现在，细节才被完全确定并能够发布一份公开声明。

目前，BusLogic 尚未准备好发布第三方为 FlashPoint 编写驱动程序所需。现有的 FlashPoint 驱动均由 BusLogic 工程部门编写，且没有足够详细的 FlashPoint 文档允许外部开发者在没有实质性帮助的情况下编写驱动程序。虽然 BusLogic 内部有人不愿发布 FlashPoint 架构的细节，但这场辩论也尚未定论。无论如何，即使今天有可用文档，编写一个可用的驱动程序也需要很长时间，尤其是我不确定投入所付出的精力是值得的。

然而，BusLogic 仍然致力于为 Linux 社区提供高性能的 SCSI 解决方案，并且不希望任何人因为拥有一块 FlashPoint LT 而无法运行 Linux。因此，BusLogic 制定了一项升级计划，允许全球任何 Linux 用户将其 FlashPoint LT 换为新的 BT-948 MultiPCI SCSI 主机适配器。BT-948 是 BT-946 的 Ultra SCSI 继任产品，拥有了 BT-946 和 FlashPoint LT 的所有优秀功能，包括智能终端（smart termination）和用于每次固件更新的闪存 PROM，并且兼容 Linux 驱动程序。此升级的价格定为 145 美元，升级计划将通过 BusLogic 技术支持部门管理，可以通过电子邮件 techsup@BusLogic.com、电话 +1 408 695-0760 或传真 +1 408 492-1542 联系。

我曾 BT-948 的 Beta 测试站点，我的 BusLogic 驱动程序 1.2.1 和 1.3.1 版本已经包含了对 BT-948 的潜在支持。后续版本中将添加对 Ultra SCSI Mastercard 卡的额外外观支持。由于这种协作测试过程，发现了几个错误，因此请确保您的固件版本为 5.05R 或更高版本。我高负载的 Linux 测试系统为测试错误恢复过程提供了理想环境，这些过程在生产系统中很少被执行，但对整个系统的稳定性至关重要。能够直接与他们的固件工程师合作，在我目前正在处理的固件控制下演示问题是非常方便的。我正在处理一些性能问题，并预计在遥远的未来进行报告。BusLogic 要求我将此关于不支持的 FlashPoint (BT-930) 的公告发送给支持的 BT-948。总结来说，BusLogic 正在为 Linux 用户提供从不支持的 FlashPoint 升级。请联系 BusLogic 技术支持以利用他们的优惠。

Leonard N. Zubkoff
inz@dandelion.com

## 主机

PM3224 PCI Fast Single-ended SCSI-2
PM3224W PCI Wide Single-ended SCSI-2
PM3334W PCI Wide Single-ended SCSI-2
PM334UW PCI Ultra Wide Single-ended SCSI-2

以及上述控制器的差分版本。
来自以下标准的控制器：

NEC, AT&T, SNI, Olivetti, Alphatronix。

支持的配置：

- 槽位：全部
- 端口：全部
- IRQ：所有水平及边沿触发
- DMA 通道：ISA 全部，EISA/PCI 不适用
- IO：端口映射，总线主
- SCSI 通道：全部

自动探测 (Autoprobe)：

适用于所有支持的配置
最新版本的 EATA-DMA 驱动可在：

```
ftp.i-Connect.Net:/pub/Local/EATA/
```
