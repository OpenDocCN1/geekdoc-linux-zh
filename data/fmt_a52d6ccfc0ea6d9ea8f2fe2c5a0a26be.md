
# 7. 测试动作小组 (JTAG) 定义了访问电子组件的标准调试接口。

图 5-1 显示了连接到硬盘背面针脚座的 USB 线。

![](img/7fe0d6d164be3169c3098d32371b2eec_150_0.png)

图 5-1：通过串口口访问硬盘固件

**注意**

**警告：** *在没有专业培训或工具的情况下，不应使用此方法。存在物理损坏硬盘无法修复的风险。*

连接终端并开启硬盘电源后，会显示启动信息。输入 `CTRL-Z` 将硬盘进入诊断模式，来自硬盘固件的命令提示符（类似于 UNIX 终端或模拟调制调器）。

```
$ cu -s 38400 -1 /dev/ttyUSB0
Connected.
```

Boot 0x01M

Spin Up[0x00000000][0x0000B67C][0x0000BA10]

Trans.

Rst 0x01M

MC Internal LPC Process

Spin Up

(P) SATA Reset

ASCII Diag mode

F3 T>

*Attaching Subject Media to an Acquisition Host 123*

通过此诊断接口，可以检索有关硬盘的详细底层信息。在接下来的示例中，Level 2 x 命令显示了内部物理硬盘几何结构以及用户区和系统区的分：

### F3 2x2

### 用户分区 (User Partition)

LBAs 000000000000-0000075D672E

PAs 000000000000-0000076F8EDD

HSkew 006E, Cyl1 002D

ZonesPerHd 11

Head 0, PhyCyls 00000-040001, LogCyls 00000-03F19C

| Physical Logical Sec Sym Data |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Zn Cylinders Cylinders Track Wedge Track Rate |
| 00 | 00000-0003FB | 00000-003FB | 010F | 0077 | 0F4D40 | 1263.750 |
| 01 | 0003C-0003FB | 0003C-05A1 | 0130 | 0077 | 0F4D40 | 1263.750 |

*(注：此处原文逻辑数据似乎有重叠，已按样翻译)*

Head 1, PhyCyls 00000-040001, LogCyls 00000-03F19C

| Physical Logical Sec Sym Data |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Zn Cylinders Cylinders Track Wedge Track Rate |
| 00 | 00000-0003FB | 00000-003FB | 010F | 0077 | 0F4D40 | 1263.750 |
| 01 | 0003C-0003FB | 0003C-0001 | 0100 | 0077 | 004440 | 1233.700 |

  1,Cyls 00000-03F19C

| Physical Logical Sec Sym Data |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Zn Cylinders Cylinders Track Wedge Track Rate |
| 00 | 00000-0003FB | 00000-003FB | 010F | 0077 | 0F4D40 | 1263.750 |
| 01 | 0003C-0003FB | 0003C-0001 | 0100 | 0077 | 004440 | 1233.700 |

| Physical Logical Sec Sym Data |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Zn Cylinders Cylinders Track Wedge Track Rate |
| 00 | 00000-0003FB | 00000-003FB | 010F | 0077 | 0F4D40 | 1263.750 |
| 01 | 0003C-0003FB | 0003C-0001 | 0100 | 0077 | 004440 | 1233.700 |

*(注：由于原文表格数据存在重复或异常，此处译文严格遵循原文格式输出)*

### 系统分区 (System Partition)

LBAs 000000000000-00000972CF

PAs 000000000000-000009811F

HSkew 006E, Cyl1 0018

ZonesPerHd 02

Head 0, PhyCyls 04002-040155, LogCyls 00000-01552

| Physical Logical Sec Sym Data |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Zn Cylinders Cylinders Track Wedge Track Rate |
| 00 | 04002-0400AB | 00000-000A9 | 0394 | 063D | 0072AE0 | 592.500 |
| 01 | 0400AC-04155 | 000AA-00152 | 0394 | 063D | 0072AE0 | 592.500 |

两个安全级别控制着正确密码的行为。安全级别（Security level）指的是 T13 标准中的主密码能力（MASTER PASSWORD CAPABILITY）位，可以设置为“高（high）”或“最高（maximum）”。如果安全级别设置为高，可以使用用户密码或主密码解锁硬盘。如果安全级别设置为最高，主密码将允许执行安全擦除命令，但只有用户密码可以解锁硬盘。

某些 PC 在启动后可能会发出安全冻结命令，以防止发送后续命令（以防止恶意的密码设置攻击）。`hdparm` 的安全输出将指示硬盘是否被冻结。许多 USB 桥器会自动以未冻结状态启动连接磁盘，但如果你仍然遇到困难，可以尝试几种方法：

- 检查 BIOS 中的启用/禁用冻结命令的设置
- 使用取证启动光盘（forensic boot CD），其防止发出冻结命令
- 将磁盘连接到独立的控制器卡（而非主板内置）
- 将磁盘热插到系统（（如果硬件支持）
- 使用不发出冻结命令的主板

如果你知道用户密码且硬盘安全处于冻结状态，你可以通过以下方式解锁硬盘：

```
# hdparm --security-unlock "mysecret99" /dev/sdb
security_password="mysecret99"
```

/dev/sdb:

正在发出 SECURITY_UNLOCK 命令，password="mysecret99", user=

默认情况下，使用 `hdparm` 提供用户密码，而主密码需要通过额外的命令行参数显式指定。如果你知道主密码且安全级别设置为“高”，你可以使用主密码解锁硬盘：

```
# hdparm --security-unlock "companysecret22" /dev/sdb
security_password="companysecret22"
```

/dev/sdb:

正在发出 SECURITY_UNLOCK 命令，password="companysecret22", user=master

如果密码未知，则无法使用常规工具访问磁盘。密码信息存储在磁盘的服务区/系统区（service/system areas）中，通常在没有特殊硬件或工具无法访问。然而，这里将提供并讨论进一步的选项。

主密码可能设置为出厂默认值，并可用于访问硬盘（如果安全级别设置为高而非最高）。你可以从互联网上轻松找到出厂默认密码。

使用暴力破解来识别主密码或用户密码是不足的，硬盘在五次尝试失败后必须重置。如果你有一组可能的少量密码，多次尝试将变得可行，并可能幸运成功。

专业的数据恢复公司提供服务和硬件工具，可以从磁盘的服务区恢复或重置 ATA Security Set 密码。并非所有磁盘都能保证成功，但数据恢复公司会列出它们支持的磁盘。在某些情况下，你可能需要将磁盘邮寄到公司的实验室，这可能涉及监管链（chain-of-custody）问题。更多信息请参见第 122 页的“磁盘服务访问”。

硬盘厂商可能能够提供重置 ATA 密码的协助。这取决于硬盘厂商的配合、证明磁盘及其内容所有权的能力、请求方的权限以及恢复数据的动机。

硬件和固件的破解技术以及研究人员发表的方法可能会为某些硬盘型号提供访问权限。安全研究社区不断发现访问和修改难以访问区域创新方法。

# 识别并解锁 Opal 自加密驱动器

自加密驱动器（SED）是全盘加密（FDE）的一种形式。与基于软件的 FDE（如 `TrueCrypt`、`FileVault`、`LUKS` 等，由操作系统管理加密）不同，SED 将加密能力直接构建在硬盘固件中。SED 是与厂商无关的并基于独立厂商的标准。负责定义该标准的国际机构是可信计算组织（`TCG`; http://www.trustedcomputing.org/）。该标准为 TCG 存储安全子系统类：`Opal`，规范版本 2.0。

本节识别具有 Opal 加密的硬盘，并描述如何使用适当的密钥来解锁硬盘。加密密钥的恢复不在本书的范围内。此处显示的示例假设密钥已知。

通过对硬盘进行物理检查可以判断其是否为 Opal SED。硬盘标签上打印的*物理安全 ID*（`PSID`）字符串的存在如图 5-2 所示。该字符串用于 Opal RevertSP 功能，该功能可以安全地生成新密钥，破坏所有数据并将硬盘重置为原始出厂状态。`PSID` 无法从硬盘查询，如果存在二维码，则必须通过物理读取或扫描。`PSID` 字符串的存在并不意味着硬盘已锁定并设置了密码；它仅表示硬盘支持 Opal 全盘加密。

6GB/s SED 5V 1.7A

510E69A241

007 HALOGEN FREE

NA

PSID: 54BADE82-5B0B-6578-E100-000089C981B5

图 5-2：Opal SED PSID

全盘加密存在“鸡生蛋”问题。如果整个硬盘都经过加密（包括引导区），如何执行主引导记录（`MBR`）并请求密码或其他安全凭据？解决方案是实现影子 MBR（shadow MBR）并将其存储在磁盘的系统区（存储 SMART 数据、块列表等存储的地方）。当 Opal 硬盘处于锁定状态时，主机对影子 MBR 是可见的。这是一组未加密的扇区（可以很大——例如 50MB 大小），通过影子 MBR 可让主机执行可信平台模块（`TPM`）并请求密码或其他安全凭据。

一个开源的工具创建于 https://github.com/opaltools/sedutil/。该工具最初名为 `sed`，现在已重命名为 https://github.com/opaltools/sedutil/。该工具在所有硬盘上都可能有效，但该工具在某些硬盘上无法工作，因为这些硬盘是加密的。
