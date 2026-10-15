

z/OS 类比：Language Environment 的功能与 z/OS 中的相同。

## 2.3.9 OSA/SF

Open Systems Adapter-Express（OSA-Express）和 Open Systems Adapter-Express2（OSA-Express2）是集成硬件功能，允许 System z 平台直接为本地局域网（LAN）和广域网（WAN）上的客户端提供工业标准连接。

Open Systems Adapter Support Facility（OSA/SF）是随 z/VM 提供的基于主机的工具，可让您自定义 OSA 的操作模式。您可以通过 CMS 用户 ID、通过对 OSA/SF API 的 REXX 调用，或通过基于 Java™ 的图形用户界面（GUI）访问 OSA/SF。

z/OS 类比：OSA/SF 的功能与 z/OS 中的相同。

## 2.3.10 REXX/VM

REXX/VM 包含 REXX/VM 解释器，用于处理类英语的重构扩展执行器（REXX）编程语言。它还包含 SAA® REXX 编程语言的 z/VM 实现。REXX/VM 为 CMS 和 GCS 组件中的 REXX/VM 解释器提供单一源代码库。REXX/VM 解释器利用 31 位寻址。

REXX/VM 解释器有助于提高您组织的生产率。使用 REXX，您可以编写定制的应用程序和命令过程、定制 CMS 命令，并创建新的 XEDIT 宏。

z/OS 类比：REXX/VM 与 z/OS 中的 REXX 存在细微差异。例如，z/VM 上的默认 REXX 环境为 CMS，而在 z/OS 中则为 TSO。

## 2.3.11 TSAF

Transparent Services Access Facility（TSAF）提供 VM 系统集合内的通信服务，而无需使用 VTAM。TSAF 在 CMS 虚拟机中运行。

最多八个安装并运行 TSAF 的 VM 系统可以组成一个 TSAF 集合。TSAF 集合中一个 VM 系统上的 APPC/VM 程序可以与集合中其他 VM 系统上的其他 APPC/VM 程序通信。路由对应用程序是透明的。应用程序之间的通信就像应用程序运行在同一系统上一样进行。

## 2.3.12 VMSES/E

Virtual Machine Serviceability Enhancements Staged/Extended（VMSES/E）可帮助您安装 z/VM 和其他启用 VMSES/E 的产品，并应用纠正或规避所报告问题的代码更改。VMSES/E 处理源代码和目标代码。

VMSES/E 还可帮助您定义、构建和管理保存的段。VMFSGMAP 命令提供保存段映射接口，让您在系统上实际构建之前修改保存段定义并查看保存段布局。

z/OS 类比：VMSES/E 在概念上与 SMP/E 相似。

下一节提供 z/VM 可选功能的概述。

## 2.3.13 DFSMS/VM

Data Facility Storage Management Subsystem for VM（DFSMS/VM）可让您更高效地控制数据和存储资源。

z/OS 类比：DFSMS/VM 的功能与 z/OS DFSMS™ 相似。

DFSMS/VM 提供空间管理、minidisk 管理、ISMF 和 IBM 磁带库数据服务器支持。这些在以下各节中进行了描述。

### 空间管理

DFSMS/VM 通过自动管理 SFS 文件池中的空间来改善 DASD 使用。作为 SFS 管理员，DFSMS/VM 允许您：

- 通过为文件和目录分配管理类，将 SFS 存储转换为 DFSMS 管理的存储。每个管理类告诉 DFSMS/VM 如何在管理文件池的过程中处理其成员。

## 2.3.14 DirMaint

利用系统架构固有的可靠性、可用性和可维护性优势。

- DirMaint 允许任何需要分配或释放 minidisk 区的事务自动处理。
- DirMaint 允许所有用户发起的事务受密码控制并记录用于审计目的。
- 命令授权通过将 DirMaint 命令分配给特权命令集来控制。用户可以被授权从多个命令集发出命令。DirMaint 提供九个预定义的命令集，但最多支持 36 个集合。
- 用户退出例程使远程系统的集中目录维护成为可能。某些退出例程还使 DirMaint 能够与其他设施（如 RACF）交互。
- 开放的命令结构允许您用自己的用户编写命令替换所有命令。
- 用于复制 CMS minidisk 文件的自动化流程最大限度地减少了人为错误的可能性。此过程在将旧（源）minidisk 归还到可用 minidisk 池之前，可选择对其进行格式化。
- 通过防止新 minidisk 空间意外分配到现有区上来确保 CMS 文件的完整性。
- DirMaint 通过最大限度地减少所需的 DIRECTXA 实用程序运行次数来提高整体系统效率。更新就地设施（DIAGNOSE 代码 X'84'）可用于立即在线放置许多更改。
- 通过提供强制定期更改密码的能力来增强系统安全性。更改密码时，用户需要输入两次新密码以防止打字错误。
- DirMaint 允许通过要求为每个用户事务输入密码来实现额外的安全级别。这是默认值。

## 2.3.15 Performance Toolkit for VM

Performance Toolkit for VM™，源自 FCON/ESA 程序（5788-LGA），可在以下方面协助操作员和系统程序员或分析员：

- 以全屏模式操作系统操作员控制台
- 支持管理多个 VM 系统
- VM 历史文件的后处理
- 性能监控
- 通过 Web 服务器提供数据以便使用 Web 浏览器查看

