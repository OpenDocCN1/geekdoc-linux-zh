
```
# swlist
# Initializing...
# Contacting target "actapppd1"...
# Target: actapppd:/
#
#
# Bundle(s):

B9788AA					1.3.0.01					Java 2 SDK 1.3 for HP-UX (700/800),
FA1-*					PA-1 + DX2.0 Add On

BUNDLIB11					B.11.11.0102.2			Required Patch Bundle for HP-UX 11i
CDS-English				B.11.11
FDDI-00					B.11.11.01				PCI FDDI;Support MWA3739A/A3739B;SW=3626A
FibChani-00					B.11.11.01.16			Support HSC/FibreChannel;
GOLDAPPS11				"B.11.11.0106.9 Gold Application Patches
GLDDABASE11				B.11.11.0106.9 Gold Base Patches for HP-UX 11i, June 2001
GIgChec-00				B.11.11.14				PCI/HSC Gigabit;Support
HW-AS55A					HW-AS42xA/AS439A/AS424A/AS45xA/SW=31642A
HPUXLII-OS-MC				B.11.11.0106				HP-UX Mission Critical
HPUXBase64				B.11.11				HP-UX 64-bit Base OS
HPUXBaseAux				B.11.11.0106				OP-UX Base OS Auxiliary
HW-enable11				B.11.11.0106				Hardware Enablement Patches for
									HP-UX 11i, June 2001
ITX-Recovery				B.3.3.116				Ignite-UX network recovery tool subset
QS235BA					B.04.13				Metascape Directory Server v4 for HP-UX
Onlinedlag				B.11.11.04				HPUX 11.11 Support Tools Bundle, Jun 2001
RAID-00					B.11.11.01				PCI RAID; Support HW-AS55A
#
# Product(s) not contained in a Bundle:
#

BVISION1				6.0				BroadVision One-To-One Enterprise
BVSNC-0AA				6.0.0				BroadVision One-To-One Enterprise 6.0_Patch AA
BVSNCeServerC2BMK7				6.0.0				BroadVision 1.1 Business-To-Business Contract Utility Installation
BVSNTreadingConnector				6.0.0				BroadVision 1.1 Adapter TradingConnector Application Installation
BVSNZbZ				6.0.0				BroadVision 1.1 Commerce Business-To-Business Installation
BVSNZb2AA				6.0.0-AA				BroadVision 1.1 Commerce Business Commerce Patch AA Installation
BVSNcwaa				6.0.0				BroadVision 1.1 Core Commerce Installation
BVSNcwaaa				6.0.0-AA				BroadVision 1.1 Core Commerce Base Commerce Patch AA Installation
BVSNcabv				6.0.0-AB				BroadVision 1.1 Core Commerce Patch AB Installation
BVSNVERITY261				2.6.1.0				Verity V2.6.1 Developer Kit
PHKL_23578				1.0				Software Distributor Cumulative Patch
PHKL_24625				1.0				Virtual Partitions manages cumul patch
PHKL_24546				1.0				vPar enablement patch
PHKL_24547				1.0				vPar enablement patch
PHKL_24548				1.0				vPar enablement patch
PHKL_24549				1.0				vPar enablement patch
PHKL_24550				1.0				Early boot, panic, Paeta & vPar enablement
PHKL_24551				1.0				thread cscop, vPar, Paeta, load averages
PHKL_24552				1.0				vPar enablement patch
PHKL_24553 1.0 console, chassis code, crash/dump, vPar PHKL_24554 1.0 vPar enablement patch PHKL_24555 1.0 PREFSETH LOCK 1/0, PR 8702 2.2, vPar PHKL_24556 1.0 vPar enablement patch PHKL_24557 1.0 vVar enablement patch PHKL_24559 1.0 vVar enablement patch PHKL_24559 1.0 SysLog overflow, high temp alerts, vPar PHKL_24560 1.0 vPar enablement patch PHKL_24561 1.0 Psetc & vVar Enablement PHKL_24562 1.0 vvar enablement patch PHKL_24563 1.0 vPar enablement patch PHKL_24564 1.0 vPar enablement patch PHKL_24565 1.0 vvar enablement patch PHKL_24566 1.0 Kernel Memory allocation, Faets Enablement PHKL_24570 1.0 Boot Bank, Faets & vPar enablement PHKL_24582 1.0 iSCSI Supports, Faets Enablement Patch PHKL_24585 1.0 Paets & vPar enablement patch PHKL_24985 1.0 vPar enablement patch PHKL_25080 1.0 vPar enablement patch FMBS_22535 1.0 Cumulative STRAAMS Patch FMNS_22713 1.0 iDGI) and linker tools cumulative patch Tivem 4.1.2 Tivol) Storage Manager make 3.60 00 06 HP-UX Virtual Partitions Functionality b 3.79.1 make
```

您在系统中看到的 `VirtualPartition` 软件版本将晚于示例中显示的版本。

维护额外的 HP-UX 文件系统（在运行 `vVars` 时很可能会发生这种情况）要求您考虑所需的额外磁盘空间，以及确保系统平稳运行的技术，例如恢复和操作系统及应用程序更新。请务必备份您的系统清单，并经常执行备份和创建可引导恢复磁带。

## 章节“简介”中的非 vPar 特定部分

在本章的这一节中，我们将重点关注以下内容：

- Veritas Volume Manager 概述
- 逻辑卷管理器 `LVM` - 您可能正在使用 `LVM` 来管理系统上的数据。我在本部分提供了 `LVM` 的背景知识。
- 使用 `LVM` 向系统添加 `XP 256` 磁盘的示例。
- 使用 `LVM` 重新配置磁盘的示例 - 我包含了一个在真实系统上执行的复杂磁盘重新配置示例，以展示使用了多少个 `LVM` 命令。虽然您的系统可能不需要这种磁盘重新配置，但它是使用 `LVM` 命令的一个很好的示例。
- 一些额外的文件系统命令。

### Veritas Volume Manager

`Veritas Volume Manager` 是 `HP-UX 11i` 的新特性，它随操作系统一起捆绑提供。
