

按字母顺序从控制器到控制器，从主设备到从设备排列字母。）一旦识别出您的 CD-ROM 驱动器，系统会提示您将 Red Hat Linux CD-ROM 插入 CD-ROM 驱动器。插入后请选择 Ok。稍作延迟后，下一个对话框将会出现。继续阅读 Upgrading or Installing 以获取升级或完整安装说明。

## 从硬盘安装

如果您要从本地连接的硬盘安装 Red Hat Linux，请突出显示“hard drive”并选择 Ok。在启动安装程序之前，您必须先将所有必要文件复制到本地连接硬盘上的一个分区。如果您尚未执行此操作，请参阅 Installing from an HTTP site。继续阅读 Upgrading or Installing 以获取升级或完整安装说明。

## Upgrading or Installing

在您选择安装方法后，安装程序会提示您进行安装或升级（见图 4-2）。

![](img/46f4935125ba89e12897afbe9d77a097_76_0.png)

图 4-2：Upgrading or Installing

## The Installation Guide for Red Hat Linux 6.0

## Installing

您通常将 Red Hat Linux 安装在干净的磁盘分区或一组分区上，或覆盖另一套 Linux 安装。

请注意：在另一套 Linux 安装（包括 Red Hat Linux）上安装 Red Hat Linux 不会保留任何先前安装的信息（文件或数据）。请确保保存任何重要文件！如果您担心保存现有系统上的当前数据（而不自行备份），您应考虑执行升级而不是安装。

如果您希望执行完整安装，请选择 Install，然后跳至 Installation Class。

## Upgrading

Red Hat Linux 6.0 的安装过程包括从基于 RPM 技术的前期版本 Red Hat Linux（版本 2.0 及更高版本）升级的能力。升级系统会安装模块化的 2.2.x 内核以及当前安装在您机器上的软件包的更新版本。升级过程通过使用 .rpmsave 扩展名（例如，sendmail.cf.rpmsave）重命名它们来保留现有配置文件，并在 /tmp/upgrade.log 中留下操作日志。随着软件的演进，配置文件格式可能会发生变化，因此在整合更改之前，您应仔细比较原始配置文件和新文件。如果您希望升级 Red Hat Linux 系统，请选择 Upgrade。

请注意：某些升级的软件包可能需要安装其他软件包才能正常运行。升级程序会处理这些依赖关系，但它可能需要安装一些不在您现有系统上的额外软件包。

请注意：如果您机器上已安装 X Window System（以及可能的老版本 GNOME），您可能会看到一个屏幕，提示您安装本发行版中包含的最新版本 GNOME。

## Installation Class

如果您选择执行完整安装，安装程序会要求您选择一个安装类别（见图 4-3）。如果您选择执行升级，则不会看到此屏幕。您可以从以下安装类别中选择：

![](img/46f4935125ba89e12897afbe9d77a097_78_0.png)

图 4-3：Installation Class

- **Workstation** — 工作站类安装将自动擦除您计算机硬盘上的所有 Linux 分区。此安装类型还将尝试自动设置双启动环境。
- **Server** — 服务器类安装将自动擦除您计算机硬盘上的所有分区（Linux 或其他）。
- **Custom** — 自定义类安装让您完全控制与分区相关的问题。如果您过去安装过 Red Hat Linux，自定义类安装与过去的安装最相似。

## The Installation Guide for Red Hat Linux 6.0

请注意：如果您选择 Workstation 或 Server，您计算机所有驱动器上的部分（或全部）存储数据将被擦除！系统会要求您确认您的决定；然而，请记住，一旦安装程序收到您的确认，擦除操作就不可逆转。

请注意：警告 — 如果您选择执行工作站类或服务器类安装，数据擦除将是不可逆的。被擦除数据的严重程度因安装类型而异：

- Workstation-class — 系统上任何硬盘上任何现有 Linux 分区上的数据将被擦除
- Server-class — 所有驱动器的所有分区上的数据将被完全擦除，无论是否在现有 Linux 分区上。

如果您选择工作站或服务器类安装，您将能够跳过自定义类安装所需的某些步骤。对于硬盘安装，请继续阅读。对于 CD-ROM 工作站或服务器类安装，您应转到第 6 章以继续安装。

## SCSI Support

接下来，安装程序将探测您的系统以查找 SCSI 适配器。在某些情况下，安装程序会询问您是否拥有任何 SCSI 适配器。如果您选择 Yes，下一个对话框会列出 SCSI 驱动程序。选择最接近您 SCSI 适配器的驱动程序。然后安装程序会给您一个机会来指定所选 SCSI 驱动程序的选项；大多数 SCSI 驱动程序应能自动检测您的硬件。

## 为 Red Hat Linux 创建分区

此时，有必要让安装程序知道它应该将 Red Hat Linux 安装在哪里。这是通过为一个或多个将安装 Red Hat Linux 的磁盘分区定义挂载点来完成的。您此时可能还需要创建和/或删除分区。

请注意：如果您尚未计划如何设置分区，请转到 Disk Partitions，并查看所有内容直到

