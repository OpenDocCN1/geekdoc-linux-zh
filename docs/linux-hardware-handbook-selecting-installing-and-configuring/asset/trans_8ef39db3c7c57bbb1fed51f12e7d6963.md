

- **cdrecord** 该程序不再得到维护，但对于一些较老的 CD-R 驱动器仍然有用。它接受一个映像文件，并使用其支持的任意驱动器将其刻录到 CD 上。

- **cdrdao** 该程序执行与 *cdrecord* 相同的功能，但它正在得到维护，并且是 Linux 上最常用的 CD 刻录软件。请阅读其主页了解更多内容，http://www.fokus.gmd.de/research/cc/gclone/employees/joerg.schilling/private/cdrrecord.html。

- **cdrdao** 又一个从文件到 CD 的程序，*cdrdao* 的特点在于它使用 DAO 刻录模式，而 *cdrecord* 仍然偏好 TAO 模式。请阅读其网站了解更多内容，http://www.ping.de/sites/daneb/cdrdao.html。

使用这些工具刻录 CD 是一个两步过程：首先创建一个映像文件，然后将其刻录到 CD 上。每个程序支持的选项数量相当大，因此你应该查阅各自的文档以获取详细信息。不过，作为一个示例，请考虑使用 *mkisofs* 和 *cdrecord* 创建 CD，这是最常见的组合。

为了创建一个在 Linux 下使用的 CD，你可能应该创建一个使用 ISO-9660 及其 Rock Ridge 扩展的映像。可以使用以下命令完成此任务：

```
mkisofs -r -o image.iso ./
```

该程序会输出一些消息，可能包括几行描述其处理过程的文本。结果是称为 *image.iso* 的映像文件，其中包含当前目录及其所有子目录中的文件。你应该检查映像文件的大小，以确保它能够放入标准的 650MB CD-R 或 CD-RW 中。如果它太大，你*可能*需要修剪一些文件或使用一种特殊的高容量空白盘——700MB CD-R 介质比较常见。如果你想检查映像文件是否包含合理的数据，你可以使用 Linux 环回接口将其挂载，如下所示：

```
mount image.iso /mnt/cdrom -o loop
```

然后你可以将文件与原始文件进行对比，验证你包含的任何程序的功能，等等。完成后，使用 *umount* 命令卸载 CD 映像文件，就像你卸载普通 CD 一样。

当你对映像文件的状态感到满意时，你可以使用 *cdrecord* 将其刻录到 CD-R 上：

```
cdrecord dev=6,0 speed=4 image.iso
```

此命令以 4x 速度将 `image.iso` 文件写入 SCSI ID 为 6、逻辑单元号（LUN）为 0 的 CD-R 设备（大多数 SCSI CD-R 驱动器使用 LUN 0）。该程序随后打印有关驱动器和你选择的刻录选项的信息，最后以如下内容结束：

> 最后一次机会退出，将在 1 秒后开始实际写入。

![](img/860d0c38bd76c9ded976e9d1e179ef25_243_0.png)

> 你必须以 root 身份运行 `cdrecord` 或将其运行在 `sudo root` 下。要执行后者，请发出命令 `chmod 4711 cdrecord`（如果你不在 `cdrecord` 的目录中，则需添加适当的路径）。此后，即使普通用户运行 `cdrecord`，它也会获得 root 权限。

写入过程随后开始，但除非你选择了详细报告，否则屏幕上不会显示任何指示此事实的信息。不过，根据你的可刻录驱动器，你应该看到灯光闪烁或改变颜色，以指示正在刻录 CD。当过程完成时，你可以挂载 CD 以检查其是否正确刻录。

![](img/860d0c38bd76c9ded976e9d1e179ef25_243_1.png)

> 你可以使用 Linux 管道将文件系统的创建和 CD 的创建阶段结合在这项操作中。例如，`mkisofs -r ./ | cdrecord dev=6,0 speed=4` - 可以从 `current` 目录的内容创建 CD，而不需要创建中间磁盘文件。缺点是，你需要更多的 RAM，并且由于无法快速向 CD-R 驱动器提供数据而发生写入错误的几率大大增加，特别是如果你以高速刻录时。

## 使用 X-CD-Roast

如果你希望避免使用命令行工具，你可以使用这些程序的图形用户界面前端，例如 X-CD-Roast（[http://www.fh-muenchen.de/home/rz/services/projects/xcdroast/e\_overview.html](http://www.fh-muenchen.de/home/rz/services/projects/xcdroast/e_overview.html)）或 Burnit（[http://sunsite.auc.dk/Burnit/](http://sunsite.auc.dk/Burnit/)）。通过无需记住命令，特别是那些涉及晦涩选项的命令，这些程序可以帮助 CD 创建过程。作为一个示例，请考虑 X-CD-Roast。通过让 X-CD-Roast 检测你的 CD-ROM 和 CD-R 或 CD-RW 设备来为你的系统配置 X-CD-Roast 后，你可以通过以下步骤创建数据 CD：

1. 从主 X-CD-Roast 屏幕，点击 Master CD。这将产生 Master From/To 窗口，如图 7.7 所示。

**7 光学驱动器**

![](img/860d0c38bd76c9ded976e9d1e179ef25_244_0.png)

### 图 7.7

使用 Master From/To 窗口设置你想要制作 CD 的源目录。

2. 在目录选择列表中，找到你想用作 CD 基础的目录。确保它列在 Directory with data to master 字段中。
3. 点击 Set Image-Type 按钮以获取如图 7.8 所示的 Set Image Type 窗口。你可以在此处设置文件系统创建选项，例如是否使用 Rock Ridge、Joliet 或两者。
4. 点击 Master Image 按钮以获取如图 7.9 所示的 Master Image 窗口。你可以更改要创建的映像文件的名称，或者，如果你已配置 X-CD-Roast 使用分区来执行此目的，则告诉它使用该分区。

**注意**

> X-CD-Roast 对 CD 映像文件使用 .raw 文件扩展名。.iso 是一个更常见的扩展名，但如果你期望 X-CD-Roast 能够写入你创建的映像文件，则不应使用此扩展名。如果你下载了一个使用 .iso 扩展名的映像文件，你可以重命名该文件，以便 X-CD-Roast 能够看到它并将其刻录到 CD 上，而无需重新创建文件系统。

### **图 7.8**

> 你可以使用 Set Image-Type 选项按钮从一组预定义选项中进行选择，或者使用 ISO-Filesystem Options 区域选择单个选项。

![](img/860d0c38bd76c9ded976e9d1e179ef25_245_0.png)

![](img/860d0c38bd76c9ded976e9d1e179ef25_245_1.png)

### **图 7.9**

> 使用 Master Image 窗口更改你创建的映像文件的名称。

**光学驱动器 7**

5. 选择文件名后，点击 Start Master Image。该程序显示一个对话框，总结程序创建 CD 映像文件的进度。
6. 在 X-CD-Roast 生成 CD 映像文件后，点击 Write Image 以显示如图 7.10 所示的 Write Image 窗口。如有必要，使用映像文件选择器选择要写入的映像文件。

![](img/860d0c38bd76c9ded976e9d1e179ef25_246_0.png)

### 图 7.10

Write Image 窗口提供了 cdrecord 程序的图形用户界面。

7. 将一张空白 CD-R 或 CD-RW 插入驱动器，然后点击 Start Write Image 以开始该过程。与创建映像文件一样，X-CD-Roast 显示一个进度对话框，如图 7.11 所示。

![](img/860d0c38bd76c9ded976e9d1e179ef25_246_1.png)

### 图 7.11

你可以调整进度对话框的视图，以显示更多或更少的关于写入过程的信息。

8. 当 X-CD-Roast 完成写入磁盘后，你可以使用 Verify burned Img. 按钮将磁盘与硬盘上的映像文件进行核对。如果你除了可刻录驱动器外还有一个 CD-ROM 驱动器，你可以配置 X-CD-Roast 使用 CD-ROM 驱动器作为验证操作的源，因此你*可能*需要将磁盘换到另一个驱动器中。由于现代 CD-ROM 驱动器比现代 CD-R 和 CD-RW 驱动器更快，因此使用 CD-ROM 驱动器通常比使用可刻录驱动器更快。

X-CD-Roast 包含许多我在此未涵盖的额外选项。由于其大多数功能都相当清晰，因此如果你知道你想做什么，浏览其菜单应该能找到相应的选项。不过，截至版本 0.96e，X-CD-Roast 尚*不*支持 DAO 刻录，因此这是你在其菜单上找不到的一项选项。由于底层 cdrrecord 已添加 DAO 支持，X-CD-Roast 最终可能会支持这一功能。X-CD-Roast 也尚未支持创建可引导 CD，尽管 mkisofs 包含此功能。

## 总结

光学介质为 Linux 计算机带来了一些不寻常的特性。它们通常具有只读性质。可刻录技术提供了一种写入数据的手段，尽管不如其他可移动介质那样无缝。然而，由于 CD-ROM 驱动器在现代计算机上几乎是普遍存在的，可刻录 CD 技术提供了一种向少数站点分发大量数据的优秀手段。它们也是备份自己数据的非常有用的手段——无论是应用程序生成的数据文件还是整个系统。

