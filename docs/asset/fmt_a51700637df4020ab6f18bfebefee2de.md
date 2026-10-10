
如前所述，Kali Linux 已经存在了一段时间了。它以前被称为 BackTrack，发布过版本 1 到 5，Kali Linux 首次于 2015 年面世，并作为 Kali 1.0 版本发布。从 2016 年开始，Kali 根据年份命名。因此，例如在编写此书时，使用的版本是 Kali 2022。

对于使用最新版本的用户，Kali Linux 会定期更新。检查官方网站以确保你拥有最新的补丁和功能是非常重要的。

## 下载所需的工具和镜像

为了能够跟随本章在各种平台上安装 Kali Linux 的操作步骤，你需要下载以下版本的 Kali，以及我在这里列出的一些额外工具：

- Kali Linux 64 位安装程序镜像（此可以作为独立操作系统安装，也可以作为虚拟机 (VM) 安装）:`https://cdimage.kali.org/kali-2022.3/kali-linux-2022.3-installer-amd64.iso`
- 适用于 VirtualBox 的 64 位 Kali Linux：`https://kali.download/virtual-images/kali-linux-2022.3-virtualbox-amd64.7z`
- Kali Everything 种子文件：`https://cdimage.kali.org/kali-2022.3/kali-linux-2022.3-installer-everything-amd64.iso`
- Tixati 种子下载软件（用于下载 Kali ISO 镜像）：`https://www.tixati.com/download/windows64.html`
- 7-Zip 工具（用于解压缩和解压 .7 文件）：`https://www.7-zip.org/download.html`
- Rufus 3.2（用于创建启动盘的工具）：`https://github.com/ptbatard/rufus/releases/v3.20/rufus-3.20.exe`
- VirtualBox 和 VirtualBox Oracle 扩展包：`https://www.virtualbox.org/wiki/Downloads`
- Raspberry Pi Imager（用于在树莓派上下载并安装 Kali）：`https://www.raspberrypi.com/software/`。访问 Imager 页面时，确保选择正确的格式。我将在 Windows 机器上使用 Imager，其下载地址为 `https://downloads.raspberrypi.org/imager/imager_latest.exe`。

## 下载 Kali Everything 种子

Kali Linux 安装程序有一个变体叫做 Kali Everything。Kali Everything 镜像比其他版本要大得多，因为它包含了 Kali Linux 的所有工具。虽然这些工具可以通过存储库（通常称为 repos）的形式手动下载和安装，但如果你不熟悉安装 Kali 工具和存储库，那么下载 Everything 版本并探索这些工具会要简单得多。你可以通过以下步骤下载 Kali Everything ISO：

- 1. Kali Everything 可以直接安装到硬盘上作为独立操作系统 (OS)，也可以如果你倾向于此选项，作为 VirtualBox 中的虚拟机。我们将在接下来的章节中介绍这两种情况。访问 `https://kali.download/base-images/kali-2022.3/kali-linux-2022.3-installer-everything-amd64.iso.torrent` 下载 Kali Everything 种子。

![](img/7489105e357b7dff3e56cd1cbb0de4fa_69_0.png)

图 3.3：Kali Everything 下载按钮镜像

你可以可以使用任的种子应用程序打开该链接。我使用了 Windows 版的 Tixati 软件，它是从 `https://www.tixati.com/download/` 下载并安装在我的 Windows 10 笔记本电脑上的。点击链接后，Kali Everything 种子文件会在 Tixati 客户端中打开。我选择将 Kali Everything 文件保存到我的“下载”文件夹，如下截图所示。选择下载位置后，点击“开始 (Start)”按钮。

![](img/7489105e357b7dff3e56cd1cbb0de4fa_69_1.png)

图 3.4：Tixati 种子界面

- 3. Kali Everything 文件下载将在 Tixati 中开始，并保存到所选文件夹中，名为 `kali-linux-2022.3-installer-everything-amd64.iso`。我们将在接下来的章节中使用这个 ISO 文件。

现在你的系统中至少已经下载了两个版本的 Kali Linux，就像我的下载文件夹中显示的那样。

| 名称 | 大小 | 类型 |
| --- | --- | --- |
| `kali-linux-2022.3-installer-amd64.iso` | 3,060,816 KB | 磁盘镜像文件 |
| `kali-linux-2022.3-installer-everything-amd64.iso` | 10,367,424 KB | 磁盘镜像文件 |
| `kali-linux-2022.3-installer-everything-amd64.torrent` | 792 KB | 种子元文件 |

图 3.5：下载文件夹中已下载的 Kali 镜像

现在让我们如何使用 Rufus 3.2 在闪存盘或其他存储介质上创建这两个 Kali Linux 实例的启动版本。

## 在便携式存储介质上安装 Kali Linux 用于实时 DFIR

如前所述，Kali Linux 可以安装在各种平台上，既可以作为独立操作系统安装，也可以作为虚拟机。我们将首先查看如何使用下载的 Kali ISO 文件创建一个启动版 Kali Linux 闪存盘。如果你还没有下载 ISO 文件，现在可以点击链接并按照上一节的说明进行操作。

这个 `.iso` 文件（或者有时也称为镜像文件）可以使用 Rufus 3.20 创建启动盘，通过启动盘在 PC 或笔记本电脑上安装 Kali Linux。它也可以在 VirtualBox 中作为虚拟机安装，我们将在本节稍后的部分使用 Kali Everything ISO 文件进行介绍。

创建启动闪存盘非常有用，因为它允许你在不安装硬盘的情况下任何电脑上运行 Kali Linux。这对于数字取证和事件响应 (`DFIR`) 特别有用。

Rufus 非常易用且简单。下载 Rufus 后，双击运行它。你会看到以下界面：

- 设备：你想要使用的闪存盘。
- 启动选择：选择镜像。
- 分区方案：`MBR`（旧版系统）或 `GPT`（新版系统）。
- 文件系统：`FAT32`（默认）。

在之前的截图中，你会注意到右侧有一个提示显示“**点击选择镜像**”。点击 SELECT 下拉并浏览到你下载 `-linux-2022.3-installer-amd64.iso` 文件的位置。我将其保存在下载文件夹。

![](img/7489105e357b7dff3e56cd1cbb0de4fa_71_0.png)

图 3.6：Rufus 界面

- 2. 在之前的截图中，你应该注意到启动选择下列出了 `kali-linux-2022.3-installer-amd64.iso`。我还将分区大小设置为 2 GB，这创建了一个空间，以便在需要下载文件或在启动安装中安装工具。
- 3. 此时，你再次可以在分区方案字段中选择 `MBR` 或 `GPT` 选项。我还将卷标签选项更改为 Kali Linux 64 1。在卷标签结尾使用 1 的原因是我已经用 `MBR` 分区方案使用了该驱动器，并且使用 `GPT` 分区方案创建了另一个启动盘，标记为 Kali Linux 64 2。
- 4. 当你配置好所有所需的选项并确保所有设置正确后，点击“开始 (`START`)”按钮。
- 5. 你可能会被提示下载名为 `ldlinux.sys` 和 `lldl...` 的附加文件。点击“是 (`Yes`)”按钮允许 Rufus 自动执行。电脑必须连接互联网以便 下载 下载这些文件。

![](img/7489105e357b7dff3e56cd1cbb0de4fa_73_0.png)

图 3.8：在 Rufus 中选择分区方案

## 安装 Kali Linux

下载所需

![](img/7489105e357b7dff3e56cd1cbb0de4fa_74_0.png)

图 3.9: Syslinux 下载需求确认屏幕

- 6. Rufus 将要求确认并警告所有可移动存储设备上的所有数据都将被删除。如果您确定已选择正确的驱动器，请点击 `OK` 按钮继续。

![](img/7489105e357b7dff3e56cd1cbb0de4fa_74_1.png)

图 3.10: 操作确认屏幕

随后 Rufus 将开始格式化驱动器，如以下截图所示。
