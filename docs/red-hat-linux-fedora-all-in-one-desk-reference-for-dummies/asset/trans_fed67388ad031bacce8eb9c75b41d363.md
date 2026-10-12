
## 使用 PartitionMagic 进行重新分区
PartitionMagic 来自 PowerQuest，可以在从 Windows 95/98/Me 到 Windows NT/2000/XP 的所有 Microsoft 操作系统中调整和分割磁盘分区。它是一款商业产品，所以你必须购买才能使用。在我撰写本文时，PartitionMagic 8.0 的标价为 $69.95。你可以在 `www.powerquest.com/partitionmagic` 上阅读相关信息并购买它。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_62_0.png)

调整磁盘分区始终存在丢失硬盘上所有数据的风险。因此，在使用 PartitionMagic 等磁盘分区工具调整硬盘分区之前，你应该 ***备份你的硬盘***。在备份之后——并且在对分区执行 ***任何*** 操作之前——请确保你能从备份中恢复文件。

当你运行 PartitionMagic 时，它会在一个窗口中显示当前分区。如果你正在运行 Windows XP，你的硬盘通常有两个分区：一个包含 Windows XP 安装文件的小型隐藏分区，以及一个用作 C 驱动器的巨大的第二个 NTFS 分区。你必须减小现有 C 驱动器的大小。这样会在该分区之后创建未使用的空间。然后，在 Red Hat Linux 安装期间，安装程序可以在未使用的空间中创建新的 Linux 分区。

要减小 Windows 分区的大小，请按照以下步骤操作：
- 1. **在 PartitionMagic 主窗口的分区映射中，右键单击分区并从菜单中选择 *Resize/Move*。**
  Resize Partition 对话框出现。
- 2. **在 *Resize Partition* 对话框中，单击并拖动分区的右边缘使其变小。**
  对于大型硬盘（超过 10GB 的任何硬盘），将 Windows 分区减小到 5GB，剩余部分留给 Red Hat Linux。
- 3. **单击 *OK* 然后单击 *Apply* 以应用更改。PartitionMagic 完成更改后，单击 *OK*。**
- 4. **重新启动 PC。**
- 5. **选择 Start::Programs::Accessories::System Tools::ScanDisk 以运行 *ScanDisk*。**

在缩小原来是 C 驱动器的分区后，你无需对剩余的磁盘空间做任何处理。在安装期间，Red Hat 安装程序会使用该空闲空间来安装 Red Hat Linux。

## 使用 FIPS 进行重新分区
随附的 DVD 包含一个名为 FIPS 的实用程序 (*the First Nondestructive Interactive Partition Splitting Program*)，它可以将现有磁盘分区拆分为两个分区。FIPS 会圈出硬盘上未使用的部分，并从该未使用部分创建一个新分区，而不会破坏任何现有数据。FIPS 无法拆分使用 NTFS 文件系统的分区，而该文件系统常用于 Windows NT/2000/XP 系统。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_63_0.png)

在使用 FIPS 重新分区硬盘之前请注意以下几点。用 FIPS 作者 Arno Schaaf 的话说，“FIPS 仍然有些实验性，尽管它已被许多人成功使用且没有严重问题。” 这简明扼要地告诉你，使用 FIPS 时你只能自负其责。出版商或我都不能对因使用或误用 FIPS 造成的损坏承担责任或法律责任。FIPS 有可能损坏你的硬盘，使其无法使用。你只有在确保已备份硬盘上的所有内容并且备份可用后才应尝试使用 FIPS。此外，在使用 FIPS 之前，请检查你的硬盘是否已准备就绪：
- 你的硬盘起初应只有 FAT 或 FAT32 分区。
- 驱动器应有足够的可用空间用于有用的 Red Hat Linux 安装——这意味着 3 到 4 GB（3–4GB）的可用空间。
- 驱动器必须在你使用 FIPS 之前进行碎片整理。
- 驱动器必须未在使用中。你不能在使用硬盘的同时对其进行分区，这意味着（除其他事项外）你不能从 Windows 内部运行 FIPS。你必须关闭 Windows，从启动盘启动，并单独运行 FIPS。

当你准备好使用 FIPS 时，请按照以下步骤操作（仅在运行 Windows 95/98/Me 时使用 FIPS）：
- 1. 通过选择 Start→Settings→Control Panel 打开控制面板。
- 2. 在控制面板窗口中双击添加/删除程序图标。
- 3. 单击“启动盘”选项卡，单击“创建磁盘”按钮，然后按照说明操作。
- 4. 将本书的 DVD-ROM 插入 DVD-ROM 驱动器。
- 5. 使用 Explorer 查看 DOSUTILS 文件夹的内容。然后将 FIPS.EXE 和 RESTORRB.EXE 复制到 A 驱动器中的启动盘。FIPS.EXE 是拆分分区的程序。RESTORRB.EXE 是可以从 FIPS 创建的区域的备份中恢复硬盘部分程序的程序（如果出现问题则使用 RESTORRB）。
- 6. 进入 DVD 上 DOSUTILS 文件夹内的 FIPSDOCS 文件夹。将 ERRORS.TXT 文件复制到启动盘。

ERRORS.TXT 是 FIPS 错误消息的列表。请查阅此列表以了解 FIPS 显示的任何错误消息的解释。
- 7. **将启动盘留在 A 驱动器中，并重新启动 PC。**
  PC 从 A 驱动器启动并显示 `A:\>` 提示符。
- 8. **输入 FIPS。**
  FIPS 程序运行，显示有关你的硬盘的信息。FIPS 在你继续之前给你一个机会保存重要磁盘区域的备份副本。之后，FIPS 会显示可以开始新分区的第一个空闲 *cylinder*（磁盘部分）——以及以兆字节为单位的分区大小。忽略柱面号，关注兆字节数。你需要 3 到 4 千个（即 3 到 4 GB）。
- 9. **使用左右箭头键调整新分区的大小——即从现有分区拆分后得到的新分区。**
  按左箭头会缩小现有分区；按右箭头会在现有分区中留下更多空间，但会减小你正在创建的新分区的大小。
- 10. **当你对新分区的大小满意时，按 Enter。**
  FIPS 显示修改后的分区表并提示你按 C 继续或按 R 重新编辑分区表。
- 11. **按 C 继续。**
  FIPS 显示有关磁盘的一些信息并询问你是否要将新的分区信息写入磁盘。
- 12. **按 Y。**
  FIPS 将新的分区表写入硬盘然后退出。
- 13. **从 A 驱动器中取出磁盘并重新启动 PC。**
  系统重新启动后，你的硬盘上的所有内容应保持完好，但 C 驱动器会变小。这是因为你已从旧 C 驱动器的未使用部分创建了一个新分区。
- 14. **选择 Start::Programs:: Accessories::System Tools::ScanDisk 以运行 ScanDisk。**
  运行此程序可确保 Windows 调整为 C 驱动器的新大小。

在 DOS 下你无需对新创建的分区做任何操作。稍后，在 Red Hat Linux 安装期间，你会从这个新分区创建两个或更多 Linux 分区。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_65_0.png)

使用 FIPS 后，Windows 可能会为 PC 上的其他磁盘和 DVD/CD-ROM 驱动器分配不同的驱动器号。（例如，你的 D 驱动器可能变为 E。）不过，FIPS 确实会确保 C 驱动器保持为 C，因此在 FIPS 拆分分区后你应该能够启动系统。记住这些不同的驱动器名称（例如 E 而不是 D），当你想要访问 C 以外的驱动器上的程序和文件时。至少在你习惯之前，保留它们的清单不会有什么坏处。

## 开始 Red Hat Linux 安装
要安装 Linux，请将 DVD 插入 DVD 驱动器，将 Red Hat 安装启动盘放入 A 驱动器，然后重新启动 PC（在 Windows 中选择 Start→ Shutdown 然后从对话框中选择 Restart）。安装启动盘包含 Linux 内核的较小版本和安装程序。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_65_1.png)

如果你的 PC 可以从 DVD 驱动器启动，你就不需要启动盘。大多数新 PC 可以直接从 DVD 驱动器启动，但某些 PC 可能需要你进行干预。要设置 PC 从 DVD 驱动器启动，你必须在 PC 启动时进入 SETUP。进入 SETUP 并设置启动设备的确切步骤因 PC 而异，但通常涉及按 F2 等键。在 PC 启动时，应该会显示一条简短消息，告诉你按哪个键进入 SETUP。在 SETUP 中，你可以将 DVD 驱动器指定为启动设备。设置好 PC 从 DVD 驱动器启动后，只需将 DVD 放入 DVD 驱动器并重新启动 PC 即可。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_65_2.png)

PC 启动后，它会从启动盘加载 Linux 内核，Linux 内核开始运行 Red Hat 安装程序。剩下的安装过程中，你将使用安装程序的 GUI 屏幕。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_65_3.png)

如果你使用的是 Red Hat 安装启动盘，并且在重新启动 PC 时驱动器中没有 DVD，安装程序将以文本模式启动并提示你插入 DVD。只有在那时它才会启动 X Window System 并切换到图形安装屏幕。

经过几秒钟后，文本屏幕会显示欢迎消息和 `boot:` 提示。欢迎消息告诉你可以通过按 F1 到 F5 之间的功能键获得帮助。要立即开始安装 Red Hat Linux，请按 Enter。然后你有机会测试 DVD 媒体是否存在任何问题。按 Enter 执行媒体检查。媒体检查后，你可以继续安装。

在快速（400MHz 或更好）的 Pentium PC 上，从随附 DVD 安装 Red Hat Linux 大约需要一个小时，如果你安装几乎所有软件包的话。
