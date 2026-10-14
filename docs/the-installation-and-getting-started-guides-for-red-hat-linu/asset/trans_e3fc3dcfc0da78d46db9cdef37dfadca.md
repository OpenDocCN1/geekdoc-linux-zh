
installation)。如果您需要 PCMCIA 支持，系统会提示您插入 PCMCIA 支持软盘。插入后请选择 Ok。安装程序随后会显示进度条，表示正在加载支持软盘。

## 选择安装方法

接下来，系统会询问您希望使用何种类型的安装方法。您可以通过以下五种基本方法之一安装 Red Hat Linux（请参阅 Installation Methods），如果在安装过程中使用 PCMCIA 设备，则需要使用支持软盘。简而言之，您可以从以下位置安装 Red Hat Linux：

- **CD-ROM**
  - 如果您拥有 CD-ROM 驱动器和 Red Hat Linux CD-ROM。只有在安装过程中使用 PCMCIA 设备时才需要 PCMCIA 支持软盘。请参阅 Installing from CD-ROM 以选择 CD-ROM 安装方法。

- **Hard Drive**
  - 如果您已将 Red Hat Linux 文件复制到本地硬盘。只有在安装过程中使用 PCMCIA 设备时才需要 PCMCIA 支持软盘。请参阅 Installing from a Hard Drive 以选择硬盘安装方法。

- **NFS Image**
  - 如果您是从导出 Red Hat Linux CD-ROM 或 Red Hat Linux 镜像的 NFS Image 服务器进行安装。只有在安装过程中使用 PCMCIA 设备时才需要 PCMCIA 支持软盘。需要网络启动盘。请参阅 Installing via NFS 以选择 NFS 安装方法。

- **FTP**
  - 如果您直接从 FTP 服务器安装。只有在安装过程中使用 PCMCIA 设备时才需要 PCMCIA 支持软盘。需要网络启动盘。请参阅 Installing via FTP 以选择 FTP 安装方法。

- **HTTP**
  - 如果您直接从 HTTP Web 服务器安装。只有在安装过程中使用 PCMCIA 设备时才需要 PCMCIA 支持软盘。需要网络启动盘。请参阅 Installing via HTTP 以选择 HTTP 安装方法。

如果您选择执行 CD-ROM 或硬盘安装，请参阅第 4 章获取相关安装说明。

如果您选择执行基于网络的安装（NFS、FTP 或 HTTP），请参阅第 5 章获取相关安装说明。

## 4 本地媒体安装

## 选择安装方法

现在您必须决定希望使用何种类型的安装方法（请参阅 Figure 4-1）。突出显示适当的选项并选择 Ok，或按 [Enter]。

![](img/46f4935125ba89e12897afbe9d77a097_74_0.png)

### Figure 4-1: Selecting an Installation Method

如果您不是执行本地媒体类型安装（CD-ROM 或硬盘），请跳至第 5 章进行网络类型安装。

如果您计划执行本地媒体类型安装，请继续阅读。

## 从 CD-ROM 安装

如果您要从 CD-ROM 安装 Red Hat Linux，请选择“CD-ROM”，并选择 Ok。安装程序随后会提示您将 Red Hat Linux CD-ROM 插入 CD-ROM 驱动器。插入后，请选择 Ok，并按 [Enter]。安装程序随后会探测您的系统并尝试识别您的 CD-ROM 驱动器。它首先会查找 IDE（也称为 ATAPI）CD-ROM 驱动器。如果找到，安装将继续。如果安装程序无法自动检测到您的 CD-ROM 驱动器，系统会询问您拥有什么类型的 CD-ROM。您可以从以下类型中选择：

### SCSI

如果您的 CD-ROM 连接到受支持的 SCSI 适配器，请选择此项；安装程序随后会要求您选择一个 SCSI 驱动程序。选择与您的适配器最相似的驱动程序。如有必要，您可以为驱动程序指定选项；不过大多数驱动程序会自动检测您的 SCSI 适配器。

### Other

如果您的 CD-ROM 既不是 IDE 也不是 SCSI CD-ROM，那就是“其他”。带专有 CD-ROM 接口的声卡就是这种 CD-ROM 类型的典型例子。安装程序会列出受支持 CD-ROM 的驱动程序列表 — 选择一个驱动程序，并在必要时指定任何驱动程序选项。

请注意：CD-ROM 的可选参数部分列表可在附录 D 中找到。如果您拥有 ATAPI CD-ROM 且安装程序未能找到它（换句话说，它询问您 CD-ROM 的类型），您必须重新启动安装，并输入 linux hdX=cdrom。将 X 替换为以下字母之一，具体取决于单元所连接的接口以及其配置为主设备还是从设备：

- a — 第一个 IDE 控制器，主设备
- b — 第一个 IDE 控制器，从设备
- c — 第二个 IDE 控制器，主设备
- d — 第二个 IDE 控制器，从设备

（如果您拥有第三个和/或第四个控制器，只需继续分配

