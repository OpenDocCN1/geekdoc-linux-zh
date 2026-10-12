
## 8.3 硬件故障排查

本节提供以下内容：

- 检查点的说明，以帮助您判断问题是硬件还是软件引起的。
- 硬件识别及确定每个问题步骤的流程。

### 8.3.1 硬件或软件故障的初步判断

当出现问题时，您首先需要确认该问题。首先收集 `dbginfo.sh` 和 `s390dbf`。确定以下事项：

- 设备是否被识别？
- 性能是否符合预期？
- 设备是否可以使用？

即使设备识别和性能方面可能没有问题，某些错误仍可能会报告，请查看 `/etc` 目录。

确认问题后，检查那些可以轻易观察到的组件（例如，是存储子系统故障？网络故障？）。确定这是否是与 I/O 相关的问题。I/O 故障应最后进行调查。

可能表明硬件问题的消息包括：

- 远程支持设施 (RSF) 通知
- HMC 的图标状态
- LPAR 的检查停止

**区分硬件或软件问题**

要确定是明显的硬件还是软件问题，错误消息和问题范围（单系统或多系统）提供了很好的线索。硬件错误消息显示在 Linux 日志、HMC 上、z/VM 控制台上，或在 IBM z/VM 环境记录编辑和打印 (EREP) 报告中。问题排查流程的流程图如图 8-7 所示。

![](img/f332344337ca8bf6846cb313a66ee0b3_271_0.png)

*图 8-7 硬件和软件问题排查流程图*

**注意：** Linux 上的 `var/log/messages` 不包含在 Linux 挂起、停机或重启期间显示的消息。

### 8.3.2 调查硬件相关消息

z/VM 中的硬件错误消息基本上包含错误代码及其含义。请查阅您 z/VM 版本各组件的消息和代码手册。

我们没有关于 Linux 中硬件消息的手册。从过去案例中搜索消息含义是一种很好的调查方法。您可以在 z/VM 技术问答库和 Bugzilla 中搜索。Linux 源代码中也会有其含义。

这里我们提供一些硬件错误消息的示例。

**DASD 硬件错误消息示例**

Sense data（感测数据）是从 SCSI 设备返回的错误。Sense data 存在于感测缓冲区中。有关 sense data 的更多信息，请参见：

http://www.linux.org/docs/1dphowto/archived/SCSI-Programming-HOWTO/SCSI-Programming-HOWTO-10.html

Sense data 的描述直接在消息中显示。示例 8-6 显示了此 sense data 的一个示例。

![](img/f332344337ca8bf6846cb313a66ee0b3_272_0.png)

关于 DASD 的另一个硬件错误消息示例是设备检查错误。

- 设备检查 (EQC) 通常指示硬件错误。
- 示例 8-7 中的消息指示复位事件的 EQC。当通道路径复位后首次访问时，控制单元会返回复位事件。当 ESCON® 或 FICON 的物理连接断开后发生重连时，通道路径会被复位。
- 当消息显示时，您不会看到连接断开的情况。

**示例 8-7 /var/log/messages**

```
Feb 6 01:07:19 xxxxxxxx kernel: dasd_erp(3990): 0.0.7404: Equipment Check - environmental data present
Feb 6 01:07:19 xxxxxxxx kernel: dasd_erp(3990): 0.0.7404: FORMAT 0 - Reserved
Feb 6 01:07:19 xxxxxxxx kernel: dasd_erp(3990): 0.0.7404: dasd_3990_erp_action_4: first time retry
Feb 6 01:07:21 xxxxxxxx kernel: dasd_erp(3990): 0.0.7403: Equipment check or processing error
```

**FCP 设备错误消息示例**

在示例 8-8 中，我们看到带有 FCP 连接的磁带机出现错误。

以下消息是在备份到磁带时输出的。如果发生这种情况，首先从错误消息中检查适配器的地址。以下列表参考了示例 8-8：

- 发现地址 (ADISC) 请求失败。
- 端口未与 SAN 网络连接。
- 恢复失败。

**示例 8-8 /var/log/messages**

```
Apr 3 07:07:21 xxxxxxxx kernel: zfcp: ELS request rejected/timed out, force physical port reopen (adapter 0.0.1902, port d_id=0x00390001) (1)
Apr 3 07:07:52 xxxxxxxx kernel: zfcp: The adapter 0.0.1902 reported the following characteristics:
Apr 3 07:07:52 xxxxxxxx kernel: WNNN 0x5005076400cd191f, WWPN 0x50050764106077b7, S_ID 0x00390010,
Apr 3 07:07:52 xxxxxxxx kernel: adapter version 0x3, LIC version 0x606, FC link speed 2 Gb/s
Apr 3 07:07:52 xxxxxxxx kernel: zfcp: Switched fabric fibrechannel network detected at adapter 0.0.1902.
Apr 3 07:07:52 xxxxxxxx kernel: zfcp: warning: failed gid_pn nameserver request for wpwn 0x500507630f400d04 for adapter 0.0.1902 (2)
Apr 3 07:07:52 xxxxxxxx kernel: zfcp: port erp failed (adapter 0.0.1902, wpwn=0x500507630f400d04) (3)
```

示例中的 ELS 指的是扩展链路服务。在这种情况下，ELS 请求目标端口的地址信息。

**gid_pn** 指的是获取端口标识符 - 端口名称。向名称服务器发送端口名称以获取端口 ID。

**看似硬件错误的消息示例**

在这个例子中，我们试图识别未格式化的 DASD。

以下消息（如图 8-9 所示）会显示，但这并不意味着它是硬件错误。如果 DASD 已格式化，错误消息将不会显示。

```
Example 8-9 /var/log/messages
--------------------------------------------------------------------
Mar 17 16:01:05 XXXXXX kernel: unable to read partition table
 dasdaa:<3>dasd_erp(3990): /dev/dasdaa (94:104),29d002b: EXAMINE 24: No Record Found detected - fatal error
 dasd(eckd): Sense data:
 dasd(eckd):device 2900 on irq 43: I/O status report:
 dasd(eckd):in req: 01a04600 CS: 0x40 DS: 0x0E
 dasd(eckd):Failing CCW: 01a046d0
 dasd(eckd):Sense(hex) 0-7: 00 08 00 00 d0 00 00 00
 dasd(eckd):Sense(hex) 8-15: 00 00 00 00 00 00 00 05
 dasd(eckd):Sense(hex) 16-23: 27 00 72 80 20 0a 0f 00
 dasd(eckd):Sense(hex) 24-31: 00 00 40 e2 00 00 00 00
 dasd(eckd):24 Byte: 0 MSG 0, no MSGb to SYSOP
--------------------------------------------------------------------
```

示例 8-10 是另一个看似硬件错误的消息示例。当使用 ext3 文件系统时显示此消息。存储系统不支持事务屏障功能。

事务屏障功能是一种用于保持数据完整性的辅助机制。

为避免这种情况，只需在 `zipl.conf` 文件中添加参数 “barrier=off”。

```
Example 8-10 /var/log/messages
--------------------------------------------------------------------
JBD: barrier-based sync failed on dasdx - disabling barriers
--------------------------------------------------------------------
```

### 8.3.3 硬件问题的处理方法

解决硬件问题应采取的方法是首先联系您的硬件支持人员。您需要硬件支持人员进一步调查硬件问题。

他们需要的一些基本信息包括：

1. 机器类型
2. 序列号
3. 机器房电话号码

需要提供给支持人员的信息包括：

1. 问题的描述
2. 问题发生时您正在做什么
3. 发生时间
4. 问题发生前是否更改了任何设置
5. 指定硬件的信息
6. 硬件信息（例如，地址）
7. Linux 上的错误消息
8. 您可以从 HMC 获取的信息

**指定设备**

如果我们能明确指定出错的设备，则可能存在以下两种情况：

1. 某台设备出现错误。
2. 设备状态不正常。

如果我们无法指定出错的设备，则：

1. 性能问题可能是磁盘 I/O，这可能位于不同的存储系统上。
2. 在具有多个 NIC 的环境中，可能存在网络连接问题。

指定出错的设备后，检查状态并区分错误（硬件或软件）。

