

## 4.5 将 z/OS 映像作为 z/VM 客户机运行

将 z/OS 系统作为 z/VM 的客户机运行的过程与运行任何其他客户机系统基本相同。本节讨论将 z/OS 映像从 z10 LPAR 迁移到作为 z/VM 客户机操作系统运行。这应该适用于任何 System z 处理器上的系统。这可能是许多站点的场景，因为 LPAR 限制、服务器整合或简化其测试环境。z/VM 的一个优势是它能够虚拟化硬件，例如虚拟化耦合设施、通道到通道适配器等。也可以操作设备地址，从而最大限度地减少硬件配置（IOCDS）的管理需求。后者能够在需要时快速高效地设置新的测试映像。

该过程本质上与为作为 z/VM 客户机运行而创建新的 z/OS 系统的情况相同。确定所需资源仍需规划，并且在我们将现有的 z/OS 系统作为 z/VM 客户机 IPL 的点上，将执行 z/OS 安装过程。

### 4.5.1 z/OS 候选说明

我们从 LPAR 迁移到 z/VM 客户机的 z/OS 映像为其定义了特定的资源。它具有 SYSNAME SC59，你可能想将其用作你的 z/VM 用户 ID，但不是必需的。它没有 CTC，并且未使用 CF 或其他需要考虑的硬件，除通过 OSA 适配器进行通信外。它的硬件配置与表 4-2 中简化的列表类似：

表 4-2：资源表

| 资源类型 | 描述 | 注释 |
|---|---|---|
| Sysname | SC59 | 可以是 z/VM 用户 ID |
| 内存 / CS | 2 GB | 初始存储 |
| 处理器 / CPs | 4 | — |
| DASD / 磁盘 | 53 个卷 | 3390 Mod 3 和 Mod 9 |
| OSA 网络适配器 | 2000-2005 | QDIO |
| 控制台 | 地址 F008 | 3270 控制台 |

### 4.5.2 z/VM 所需定义

表 4-2 中第 219 页列出的资源是你在打算启动 z/OS 映像的虚拟机中必须定义的资源。请注意，该表不包含所有必要的细节，例如所有 DASD 磁盘设备地址。

### 4.5.3 在 USER DIRECT 中定义 z/OS 客户机

在获得有关 z/OS 映像配置的必要数据后，我们登录到 z/VM MAINT 用户 ID 并更新了 z/VM USER DIRECT 文件（参见第 18 页的 2.2.4 节“用户目录”和第 294 页的“USER DIRECT 文件”）。

> 注：使用相应的 z/OS sysname 为客户机命名可能有意义。

图 4-36 显示了 z/OS 客户机的定义。

```
USER SC59 GUESTZOS 2G 4G G
INCLUDE IBMDFLT
ACCOUNT ITS30000
IPL CMS PARM AUTOCR
MACHINE ESA 4
OPTION MAINTCCW QUICKDSP
CONSOLE F00B 3215
NICDEF 2000 TYPE QDIO DEVICES 6 LAN SYSTEM VSW1
MDISK 0191 3390 2390 2 LX6W02 MR
MDISK 813A 3390 0 END OP1TSA MWV
MDISK 8244 3390 0 END OP1HFC MWV
....
MDISK C730 3390 0 END IODFPK RR
MDISK D42A 3390 0 END Z19RF1 RR
```

图 4-36 SC59 用户 ID 的 USER DIRECT 条目。

根据图 4-36 中的行号对语句的描述：

- 1 建立 USER SC59，密码为 GUESTZOS。它最初定义为 2 GB 存储，最大为 4 GB，并定义为特权类 G 用户（无特殊特权）。
- 2 包含 PROFILE IBMDFLT（此处未显示）。
- 3 提供记账信息。
- 4 在登录时 IPL CMS，这将自动执行 PROFILE EXEC（如果存在）。从 PROFILE EXEC，你可以执行其他 exec。
- 5 定义客户机的模式。对于此特定用户，体系结构为 ESA，最多 4 个 CPU。
- 6 为客户机用户 ID 建立选项。MAINTCCW 意味着客户机允许初始化其使用的任何 DASD。QUICKDSP 导致客户机在有工作要做时立即添加到调度列表中，而不进入合格列表。
- 7 将客户机控制台地址定义为与 z/OS 控制台相同的地址。请注意，由于 z/VM 控制台要求，此阶段必须将其定义为 3215。它将在 IPLSC59 EXEC 中重新定义为 3270 以便 IPL z/OS（参见第 225 页的示例 4-18）。
- 8 将到 z/VM vswitch 的连接定义为 OSA 设备，从地址 2000 开始的六个连续地址。
- 9 定义客户机在 CMS 中的 minidisk。用于 CMS 文件系统，例如 PROFILE EXEC（后面描述）。
- 10 11 提供 z/OS 所需的 DASD 定义。它们都定义为 minidisks，从第 0 个柱面开始到最高柱面结束（整个磁盘）。在我们的例子中，每个设备的实际地址和虚拟地址是相同的。磁盘地址可以使用除实际地址之外的地址来定义，以简化测试映像的配置管理。还请注意，磁盘定义为访问模式 MWW，即多写访问。最后的 V 定义 CP 应为此 minidisk 的 I/O 操作使用其虚拟保留/释放支持。这是为了确保如果从多个客户机访问时的完整性。如果有共享只读 DASD，则访问可以定义为只读（RR）。

> 注：并非所有磁盘都列出，只有几个示例用于说明目的。还有其他 minidisks 定义给客户机 SC59。

> 提示：你可以将 minidisks 定义为访问模式 RR 以防止它们被更新，如果这是期望的。这对于防止对某些磁盘（例如你的 SYSRES 或 IODF 磁盘）的分配或更新很有用，而无需在 RACF 或类似产品中调整任何访问规则。

