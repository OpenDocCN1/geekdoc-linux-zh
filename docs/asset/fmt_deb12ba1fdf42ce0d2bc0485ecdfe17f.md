
- `leaflet.png`: 一个便携网络图形 (PNG) 格式的示例文档。双击此项将在 Ubuntu 的 GIMP 中打开它，在 Kubuntu 8.04 及早版本的系统上使用 Dolphin 在 Gwenview 中打开，在 Kubuntu 8.10 及更高版本的系统上使用 Konqueror 在 Konqueror 中打开，以及在 Kubuntu 8.10 及更高版本的系统上使用 Okular 打开。

- `Logos`: 一个包含 PNG 格式的 Ubuntu 和 Kubuntu 图标的示例。双击这些项中的任何一个将在 Ubuntu 上的 GIMP 中打开它。

- `00-about-these-files.odt`: 一个示例 OpenOffice 文档，提供了关于目录目录文件中文件的信息。双击此项将在 OpenOffice Writer 中打开它。

- `about-ubuntu-rtf.rt`: 一个富文本格式 (RTF) 的俄语文档。双击此项将在 OpenOffice Writer 中打开它。

- `derivatives.doc`: 一个 Microsoft Word 格式的示例文档，描述了 Ubuntu Linux 发行版的变体，例如 Edubuntu、Kubuntu 和 Ubuntu。双击此项将在 OpenOffice Writer 中打开它。

- `maxwell1.odt`: 一个示例 OpenOffice 文档，通过绘制麦克斯韦方程展示 OpenOffice Writer 的数学能力。双击此项将在 OpenOffice Writer 中打开它。

- `payment-schedule.odt`: 一个示例 OpenOffice 表格，显示了计算和其他功能。双击此项将在 OpenOffice Calc 中打开它。

- `presenting-kubuntu.odt`: 一个示例 OpenOffice 演示，讨论了 Kubuntu。双击此项将在 OpenOffice Impress 中打开它。

- `presenting-ubuntu.odt`: 一个示例 OpenOffice 演示，讨论了 Ubuntu。双击此项将在 OpenOffice Impress 中打开它。

- `triag.xlsx`: 一个示例 Microsoft Office/Excel 文档，显示了计算和结果的图形显示。双击此项将在 OpenOffice Calc 中打开它。

- `welcome.odt`: 一个示例 OpenOffice 文档，包含嵌入图形并提供了 Ubuntu Linux 的介绍。双击此项将在 OpenOffice Writer 中打开它。

- `Ubuntu_Free_Culture_Showcase`: 文件夹，包含了 Ubuntu 8.10 自由文化展示 (`https://wiki.ubuntu.com/UbuntuFreeCultureShowcase`) 的获奖音频和视频文件，这些媒体文件根据知识共享署名相同相同许可 (`https://wiki.ubuntu.com/ShareAlike`) 下发布，以便在演示（即展示）新 Ubuntu 系统时使用。双击此目录下的 OGA 文件将在 Ubuntu 上的 Totem 中播放，在 Kubuntu 系统上的 Amarok 中播放。双击此目录下的 OGV 文件将在 Ubuntu 上的 Totem 中打开，在 Kubuntu 8.10 或更新系统上的 Dragon player 中打开，或在 Kubuntu 8.04 或更早系统上的 Kaffeine 中打开。

# 开始使用 Ubuntu 和 Kubuntu

双击这些示例文档和文件（在默认 Kubuntu 系统上单击）将让你有机会尝试关联的软件包，而无需从零开始。你无法直接在原处修改这些文档，因为它们是从 CD 加载的。如果需要修改其中任何一个，请将文档或文件复制到登录目录并将其设置为可写。有关更改 Linux 文件权限的信息，请参阅第 4 章名为“理解 Linux 权限”的部分。

## 从桌面 CD 访问硬盘

在 Windows 或其他 Linux 系统上启动 Ubuntu 或 Kubuntu 的桌面版本是可以的，但如果你进行任何实际工作，可能希望保存以便以后使用。由于 Ubuntu 和 Kubuntu CD 从内存文件系统（称为 RAM 磁盘）运行，因此在从 CD 运行 Ubuntu 或 Kubuntu 时创建数据的关键在于，能够访问硬盘上的现有文件并将数据保存到那里，或者像本章稍后“使用持久化”部分中解释的那样使用外部持久存储设备。要访问你的驱动器，你必须在运行 Ubuntu 或 Kubuntu 时显式地使其可用（挂载），这需要你使用一些特殊的工具——你可以选择图形或命令行工具。

接下来的部分将解释如何从不同类型的桌面 CD 挂载并访问你的文件系统，以便你可以保留从桌面运行 Ubuntu 或 Kubuntu 时创建的文件。

## 从桌面 CD 访问分区

Windows 系统使用 NTFS（新建文件系统）或旧的 FAT32（32 位文件分配表）文件系统。幸运的是，Linux 对这两种文件系统提供完全支持，一旦你从 Ubuntu 或 Kubuntu CD 启动，就可以轻松挂载系统硬盘上存在的文件系统，以便你可以访问现有文件或保存从 CD 运行期间创建的任何文件。

## 使用 Nautilus 从 Ubuntu 桌面 CD 访问现有分区

如果你从 Ubuntu CD 启动，可以执行以下操作：

- 1. 从桌面 CD 启动后，选择“位置”(Places)菜单。显示 Nautilus 窗口，在左侧面板显示所有分区，如图 19 所示。

- 2. 要挂载硬盘上的任何分区，点击位置列表中的分区名称。右侧格中显示该分区的图标，如图 20 所示。

你可以通过检查其包含的文件来识别分区的类型。例如，图 20 所示的分区包含“Program Files”和“My Music”，这显然是一个 Windows 分区。

### 安装 Ubuntu 和 Kubuntu

图 19

Nautilus 中的可用分区

![](img/e3248f69da6474405a34229df5_86_0

图 20

在 Nautilus 中查看 Windows 分区

![](img/e3248f69da6474405a34229df5_86_1

# 开始使用 Ubuntu 和 Kubuntu

一旦你挂载了分区，位置列表中的名称右侧会显示一个图形箭头，表示它当前已挂载。在将从 Live CD 要保存的任何文件或目录拖到 Nautilus 中的该分区后，你可以点击该箭头来卸载分区。根据一般原则，在从 Live CD 关机或重启之前，卸载挂载的硬盘分区是个好习惯。

### 使用 Dolphin 从 Kubuntu 桌面访问现有分区

如果你启动了 Ubuntu 8.04 或更高版本的桌面 CD，可以执行以下操作访问系统硬盘上的现有文件系统：

- 1. 从桌面 CD 启动后，右键点击桌面并选择“运行命令”。输入 `dolphin` 并按键盘上的 Enter/Return。显示 Dolphin 窗口。

- 2. 如果你使用的是 Kubuntu 8.04 桌面，选择 Dolphin 窗口左侧面板中的“存储媒体”(Storage Media)。每个可用分区的图标在中间面板显示，如图 21 所示，显示了大小为 6.3GB、20GB 和 60GB 的可挂载分区。

- 3. 如果你使用的是 Kubuntu 8.10 或更高版本的桌面 CD，可用分区将列在 Dolphin 窗口左侧面板的卷中，如图 22 所示，列出了三个可用卷。虽然 8.10 提供的 Dolphin 版本没有标识每个卷包含的文件系统类型，但这使得定位 Windows 分区变得容易。

### 图 2-22

在 Kubuntu 8.04 系统上的 Dolphin 中可用的卷

![](img/e3248f698da647444405a34229bd9df5_88_0.png)

- 4. 如果你正在使用 Kubuntu 8.04 系统，左键点击 Dolphin 中央面板格中的媒体图标以挂载该分区并显示其内容，其看起来将类似于图 2-23。

### 图 2-23

Kubuntu 8.04 上的 Dolphin 中的 Windows 分区

![](img/e3248f698da647444405a34229bd9df5_88_1.png)

### 开始使用 Ubuntu Kubuntu

5. 如果你正在使用 Kubuntu 8.10 或更高系统，左键点击 Dolphin 左侧面板格中的任何卷图标来挂载卷，并在 Dolphin 中央面板格中显示其内容，其看起来类似于图 2-24。

图 2-24

在 Ubuntu 8.10 或更高版本上的 Dolphin 中的 Windows 分区

![](img/e3248f698da647444405a34229bd9df5_89_0.png)

现在你可以将文件从桌面拖动到已挂载的 Windows 或 Linux 分区。完成后，你可以重启系统，你将发现你在分区中创建的文件和目录，就像你从系统的原生 Windows 或 Linux 操作系统创建它们的一样。

### 从命令行访问分区
