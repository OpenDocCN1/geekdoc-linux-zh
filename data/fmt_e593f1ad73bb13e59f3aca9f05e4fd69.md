
![](img/efbfd8c0b79408e6b4551c9993acdb3c_42_0.png)

图 1.3

如果你在“属性”对话框中看到 NTFS 字样，则你无法使用 FIPS 调整硬盘分区大小

### 在使用 FIPS 之前进行碎片整理

在实际使用 FIPS 之前，你必须对驱动分区进行碎片整理。在运行 FIPS 之前进行碎片整理是必要的，因为只有当存在连续的未使用空间时，FIPS 才能缩小 Windows 分区。碎片整理会将现有数据推向分区的开头，将所有未使用空间留到末尾，这样 FIPS 就可以将其修剪掉。

你可以按照以下步骤启动 Windows 碎片整理工具：

- 1. 双击 Windows 桌面上的“我的电脑”图标，打开 Windows 资源管理器并显示系统内每个存储设备的图标。
- 2. 右键点击代表你要碎片整理的硬盘的图标；在弹出的右键菜单中选择“属性”。
- 3. 从出现的对话框中选择“工具”选项卡。
- 4. 点击“立即碎片整理”按钮。进度指示器将显示你的硬盘正在进行碎片整理。当 Windows 显示碎片整理完成时，退出碎片整理工具。

### 在重新分区时保护你的数据

FIPS 是一个经过良好测试的程序，在保留数据的同时调整现有分区大小方面表现非常出色。但请不要忘记，你要负责保护自己的数据。在尝试调整你的 Windows 分区大小之前，务必确保已备份了任何重要文件。

大多数用户选择至少将他们的“我的文档”文件夹的内容复制到移动存储介质（如 Zip 或光盘 CD-ROM）上。这样，即使硬盘被意外删除，最重要的文件也会得以保留。

### 创建 FIPS 软盘并启动 FIPS

FIPS 程序位于你的 Fedora 安装光盘上。当你运行 Windows 时，将磁盘插入你的 PC，打开 `dosutils` 文件夹，然后打开 `fips20` 文件夹。双击文件夹中的 `fips doc` 文件并将其打印；在你在使用 FIPS 调整分区大小之前，你需要熟悉这些文档。

你通过 DOS 启动软盘运行 FIPS。虽然软盘只能在 MS-DOS、Windows 95、98 或 Me 系统上创建；但 Windows 2000 和 Windows XP 并不提供创建 DOS 启动软盘的实用程序。不打算使用 FIPS 的 Windows 2000 和 Windows XP 用户可以跳过本小时稍后的“破坏性重新分区”章节。

#### 启动软盘与 Windows 2000/XP

Windows 2000 和 Windows XP 用户需要获得对 MS-DOS、Windows 95、98 或 Me 系统的临时访问，按照这里的指示创建启动软盘。如果你使用 Windows 2000 或 Windows XP 且没有适用于创建启动软盘的计算机系统，那么破坏性重新分区是在现有 Windows 硬件上为 Linux 提供空间的唯一方法。

要在 Windows 95、98 或 Me 中创建包含 FIPS 的 DOS 启动软盘，请遵循以下步骤：

- 将一张空软盘插入你的 PC。
- 双击 Windows 桌面上的“我的电脑”图标；右键点击代表软驱驱动器的图标。会出现右键菜单。
- 从弹出的右键菜单中选择“格式化”选项。对话框将提供软盘格式化选项，如图 1.4 所示。
- 选择“全格式”作为格式类型并勾选“复制”。

![](img/efbfd8c0b79408e6b4551c9993acdb3c_44.png)

图 1.4

格式化对话框允许格式化软盘

### 关于多硬盘用户的 FIPS 更多信息

以下 FIPS 假设你的系统只有一个硬盘。如果你要在其他硬盘上调整分区，请参考 FIPS 文档。

### 使用 FIPS

当你首次启动 FIPS 时，会询问你是否备份根分区。FIPS 在你的软盘上创建一个名为 `.000` 的根分区备份。如果发生任何问题，你可以使用启动软盘恢复系统。

FIPS 提示你插入软盘：

FIPS 然后会显示如下信息：

- Bytes per sector | 512
- Sectors per cluster | 8
- Reserved sectors | 33
- Number of FATs | 2
- Number of sectors | 0
- Media descriptor | F8
- Sectors per FAT | 399
- Sectors per track | 63
- Drive heads | 64
- Hidden sectors | 63
- Number of sectors (long) | 2024
- Physical drive number | 80h
- Checking boot sector | OK
- Checking FAT | OK
- Searching for free space | OK
