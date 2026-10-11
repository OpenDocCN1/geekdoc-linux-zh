
选择用户名的常用约定是使用您的名字，后跟姓的首字母。例如，John Doe 的用户名可以是 `johnd`。用户名区分大小写，应以小写字母开头，可以包含数字，长度不能超过 16 个字符。某些词是被保留的，不能作为用户名。如果您选择保留字（如 Linux 命令）作为用户名，系统会发出警告。

### 6 启用以下按钮之一：

- 安装标准桌面 (Install Standard Desktop) — 安装最常用的应用程序、实用程序和文件。如果您不确定安装哪些 Corel LINUX 组件，请使用此项。您可以之后添加或删除组件。这是大多数用户的推荐选项。
- 显示高级安装选项 (Show Advanced Install Options) — 允许您选择安装哪些 Corel LINUX 组件。此选项让您对安装过程最大的最多。如果您需要安装标准安装中未包含的特殊组件，请选择此选项。更多信息请参阅下表。如果您选择此选项，请选择随后的安装选项，然后继续执行此过程的第 7 步。

### 8 如果您的计算机有多个硬盘，系统会提示您选择安装到哪个硬盘。在这种情况下，您选择的硬盘将被擦除。所有其他硬盘将保留其当前文件并在 Corel LINUX 中可用。

| 高级安装选项 | 解释 |
| :--- | :--- |
| 标准桌面 (Standard Desktop) | 选择此选项等于选择“安装标准桌面”。这是大多数用户的推荐选项。 |
| 桌面增强 (Desktop Plus) | 此选项提供了标准桌面选项中的所有项目，外开发工具、编辑器和编译器组件。 |
| 服务器 (Server) | 此选项为多种服务器提供了桌面增强选项的所有项目，包括 Web、FTP、电子邮件和打印服务器。 |
| 自定义 (Custom) | 此选项允许您选择安装哪些 Corel LINUX 组件，并对安装过程提供最大的控制。如果您需要安装其他安装选项未包含的特殊组件，或者想安装更少的组件，请选择此选项。 |

您可以将 Corel LINUX 安装到现有的 DOS/Windows 分区。此安装选项允许在运行 MS-DOS 6、Microsoft Windows 3.1x、Windows 95 或 Windows 98 的计算机上从 MS-DOS 模式启动 Corel LINUX。Windows 不不支持 MS-DOS。

将 Corel LINUX 安装到 DOS/Windows 分区需要在计算机的某个硬盘上留出安装空间。如果您不确定是否使用 Linux 操作系统，这是一个很好的安装选择，因为它让您在决定格式化硬盘创建分区或删除现有操作系统之前尝试使用 Corel LINUX。有关磁盘分区的更多信息，请参阅第 21 页的“理解 Install Express 和磁盘分区”。

Windows 文件系统必须是 FAT 16、FAT 32 或 VFAT 才能使用此安装过程。更多信息请查阅您的 Windows 文档。

- 1 按照第 25 页“用 Corel LINUX 替换 Microsoft Windows”程序中的步骤 1 到 6 操作。
- 2 启用“安装到 DOS/Windows 分区 (Install In DOS/Windows Partition)”按钮，点击“下一步”按钮。
- 3 从“设备”列表中选择安装 Corel LINUX 的驱动器，并在“分区大小”框中输入分区大小。
- 4 准备好开始安装时点击“安装”按钮。不建议在点击“安装”按钮之前禁用“格式化期间扫描坏块 (Enable The Scan Bad Block During Format)”选项。该选项会在安装前扫描硬盘错误，并会延长安装 Corel LINUX 所需的时间。

- 1 点击“开始”按钮，点击“关机”。
- 2 在“关机”对话框中，启用“重新计算机”，点击“确定”。
- 3 当看到“启动 95/98”时，按 F4。
- 4 点击“安全模式，命令提示符”，并按 Enter 键。
- 5 在命令行提示符处，进入安装 Corel LINUX 的文件夹。通常，Corel LINUX 安装在 `C:\CDL` 文件夹。要进入该文件夹，输入 `C:\` 并 Enter，然后输入 `cd CDL` 并 Enter。
- 6 输入 `StartCDL.BAT`。

Corel LINUX 可以在同一计算机上与多个操作系统共存。要让 Corel LINUX 与其他系统共存，硬盘必须分区，且至少有一个分区供 Corel LINUX 使用。“理解 Install Express 和磁盘分区”见第 21 页。以下程序基于 Corel LINUX 与 Microsoft Windows 共存，适用于经验用户。

- 1 按照第 25 页“用 Corel LINUX 替换 Microsoft Windows”程序中的步骤 1 到 6 操作。
- 2 启用以下按钮之一：
  - 使用空闲磁盘空间 (Use Free Disk Space) — 此选项需要在分区硬盘上有未分配的磁盘空间。在安装 Corel LINUX 之前，Install Express 将此空间格式化为 Linux 分区和交换文件分区。Linux 分区的文件系统格式为 `ext2`。
  - 编辑分区表 (Edit Partition Table) — 此选项允许您在硬盘上删除和创建分区。在使用此选项之前，您应该将重要数据备份到其他介质。此选项不允许您编辑分区大小。
- 3 点击“下一步”，按照 Install Express 中的安装说明操作。
- 有关在多操作系统计算机上启动 Corel LINUX 的信息，请参阅第 31 页的“启动 Corel LINUX 和其他操作系统”。

某些版本的 Corel LINUX 包含 Corel LINUX 安装（启动型）软盘。如果您需要此软盘，可以使用一张 3.5 英寸高密度软盘进行创建。此启动盘可以使用 Windows 95、Windows 98、Windows NT 或 Linux 操作系统创建。

在 Windows NT 中，您可能可以重新配置计算机以使 CD-ROM 能够启动。

- 将软盘标记为“Corel LINUX boot”，并将其插入软盘驱动器中。
- 此磁盘的内容将被擦除。
- 将 Corel LINUX 安装 CD-ROM 插入 CD-ROM 驱动器。确保 Windows 已经启动。
- 双击“我的电脑”图标。
- 右键点击 CD-ROM 驱动器并点击“打开”。
- 双击“工具”文件夹。
- 双击 `BOOTFLOPBAT` 文件并按照说明操作。
- 在 Windows NT 中，点击“开始”、“设置”、“控制面板”。
- 双击“设备”。
- 从设备列表框选择 Cdrom。
- 点击“启动”按钮。
- 启用“启动”按钮，并点击“确定”。
- 上述过程可能不受所有的 CD-ROM 硬件。
- 除了在 Windows NT 中更改 CD-ROM 设置外，您可能还需要更改计算机 BIOS 设置中的设置。有关更多信息，请参阅您的计算机用户手册。
- 将软盘标记为“Corel LINUX boot”，并将其插入软盘驱动器中。
- 此磁盘的内容将被擦除。
- 2 将 Core LINUX 安装 CD-ROM 插入 CD-ROM 驱动器，并以 `root` 身份登录 Linux。
- 3 在 shell 环境中输入以下命令挂载 CD-ROM：

```
mount -t iso9660 /dev/cdrom /mnt/cdrom
```

- 4 在 shell 环境中输入以下命令：

```
diff if=/mnt/cdrom/boot/boot1440.img of=/dev/fd0
```

如果您购买并安装了 Core LINUX，可以向 Corel 注册您的 Core LINUX 。通过注册，您可以收到有关更新、服务补丁和升级的最新信息。注册后，您还可以获得 Corel 的优质技术支持。

要进行注册，您需要 Core LINUX 产品真伪卡片上的序列号。您可以访问 Corel 网站并在以下地址填写注册表单

安装 Core LINUX 后，您可以登录计算机并开始使用您的新操作系统。通过登录，您识别了自己的身份为 Core LINUX 用户。根据您的用户名，Core LINUX 会为您授予计算机选项和权限，记住您的个人设置，并保护您的信息和数据。

您可以使用安装期间创建的用户名登录，也可以使用 `root` 账户登录。Linux 中的 root 账户用于系统管理，并在安装期间自动创建。通过 root 用户（系统管理员）身份登录计算机，您拥有无限权限；您可以添加和删除用户账户、更改用户权限并配置 Core LINUX。为了安全起见，您在第一次作为 root 用户登录时，应为 root 账户设置密码。有关使用 root 账户的更多信息，请参阅第 101 页的“管理 Core LINUX 系统”。
