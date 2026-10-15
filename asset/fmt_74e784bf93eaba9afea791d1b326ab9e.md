
# 第3章 安装红帽

你可以在附带的 Red Hat `/utils/` 目录下的 `fips.doc` 文档找到使用 FIPS 的完整说明。只有当你的驱动器上留有剩余空间安装 Linux 时，此程序光盘才能提供帮助；否则，你可能需要删除文件或使用所描述的过程对硬盘进行重新分区。

在 Slackware 下（其安装方法将在第 4 章讨论），你可以使用 UMSDOS 在与 DOS 相同的分区上安装 Linux。UMSD 是一个允许 Linux 存在于 DOS 分区上的项目。UMSD 在现有的 DOS 目录下创建一个 Linux 根文件系统。遗憾的是，你无法在 Red Hat 下使用 UMSDOS。

## 删除分区

遗憾的是，`FDISK` 不允许你简单地调整分区大小；你必须先删除该分区，然后按所需的大小将其添加。在 `FDISK Options` 方案中，选择菜单 3，Delete Partition or Logical DOS Drive，这会删除必要的分区。会出现 Delete Partition or Logical DOS 界面（参见图 3.3）。

根据你要删除的分区类型选择相应的选项，作为主 DOS 分区。例如，选项 1，Delete Primary DOS Partition，允许你删除主 DOS 分区。

### 图 3.3

使用 Delete Partition 界面删除特定的分区或逻辑驱动器。

![](img/bffdba228b656a1846f7f38a3801d7f2_85_0.png)

选择选项 1 显示 Delete DOS Partition 界面（参见图 3.4）。`FDISK` 屏幕会询问分区的卷名，然后要求确认，以查看你是否真的要删除该分区。因为分区上的所有信息将被破坏，`FDISK` 想要绝对确定你想要删除主 DOS 分区。

### 图 3.4

当你尝试删除主 DOS 分区时，MS-DOS 会发出警告。

![](img/bffdba228b656a1846f7f38a3801d7f2_86_0.png)

## 添加分区

在你删除所有必要分区后，你必须通过选择 `FDISK Options` 界面上的 Create a DOS Partition 菜单项，为你的 DOS 系统添加适当的分区。图 3.5 显示了 Create a DOS Partition or Logical DOS Drive 界面。

### 图 3.5

大多数操作系统都需要一个主活动分区才能正常启动。

![](img/bffdba228b656a1846f7f38a3801d7f2_86_1.png)

注意 你无法使用 DOS `FDISK` 程序添加 Linux 或 OS/2 分区。Linux 使用的硬盘将在稍后的章节“使用 Linux `fdisk` 命令”中介绍。

为分区提供所有可用空间以及将分区设为活动分区是 `FDISK` 的默认设置，如图 3.6 所示。

### 图 3.6

你可以为分区提供所有可用空间并将磁盘分布在多个分区上。

![](img/bffdba228b656a1846f7f38a3801d7f2_87_0.png)

对 `FDISK` 回答“否”表示该分区是可启动的。要启动，你必须为你的分区指定空间。图 3.6 显示了以兆字节或百分比显示的 Specify Disk Space 界面。

## 格式化分区

在重启电脑后，你需要使用以下命令为 DOS 准备新分区并格式化相应的驱动器：

```
format: /s
```

格式化完成后，你可以恢复备份。记住，如果你缩小了分区，并不是所有文件都能放入新驱动器。将无法放入新驱动器的文件放在其他驱动器或分区。

## 安装 Linux 系统

要开始 Linux 安装，将创建的启动盘放入驱动器并重启电脑。系统显示以下提示符并开始初始化：

```
LILO:boot:
Loading Linux...
```

观察出现的消息，以防 Linux 无法识别你的硬件。如果是，你可能需要在启动时向 Linux 传递一些额外的参数。记录这些参数，在提示符处输入。如果你有彩色显示器，你应该会看到屏幕（参见图 3.7）。

### 图 3.7

Red Hat 安装程序可以利用彩色显示器屏幕上的颜色。

![](img/bffdba228b656a1846f7f38a3801d7f2_88_0.png)

使用 `<Tab>` 键选择选择并按下 `<Return>` 显示欢迎界面（参见图 3.8）。

### 图 3.8

Red Hat Linux 欢迎界面。

![](img/bffdba228b656a1846f7f38a3801d7f2_88_1.png)

### 图 3.9

红帽 Linux 为 PCMCIA 卡提供可选的支持。

![](img/bffdba228b656a1846f7f38a3801d7f2_89_0.png)

### 图 3.10

红帽允许你使用多种方法安装系统，包括 NFS 和 ftp。

![](img/bffdba228b656a1846f7f38a3801d7f2_89_1.png)

注意：本章的剩余部分均假设你正从本地 CD-ROM 驱动器进行安装。如果你选择了其他安装方法，请参阅相应的帮助主题或访问红帽网站 http://www.redhat.com。

接下来，程序会询问你的 CD-ROM 驱动器类型（见图 3.11）。你可以从以下选项中选择：

- IDE (ATAPI)
- SCSI
- 其他 CDROM

### 图 3.11

红帽 Linux 安装程序需要知道系统中使用了什么类型的 CD-ROM。

![](img/bffdba228b656a1846f7f38a3801d7f2_90_0.png)

“其他 CDROM”类别包括由 Creative Labs（SoundBlaster）销售的驱动器以及基于多媒体套件的 CD-ROM，还包括：

- Aztec CD Sanyo
- Goldstar R420 Sony CDU-31A
- Mitsumi Sony CDU-5xx
- Optics Storage 8000 SoundBlaster/Panasonic
- Philips CM206/CM260

根据你的选择，安装程序可能会询问某些参数，例如 IRQs 或 DMA 地址。程序可能会通过探测你的硬件来自动确定这些值。最好在提供参数之前让程序进行探测。

> 注意：当安装程序探测系统硬件时，系统可能会挂起。如果发生这种情况，你必须重启并重新安装。在尝试重新安装之前，务必收集所需的信息，如 IRQs 和 DMA 地址。

在检测到 CD-ROM 类型后，系统开始从 CD-ROM 驱动器进行安装。首先，它询问你是要安装新系统还是升级现有的红帽系统。红帽 4.0 可以轻松升级到 2.0、2.1 或 3.0，但没有任何 Linux 发行版可以轻松升级到不同的发行版版本。因此，如果你有之前的发行版版本（如 Slackware），最好的方法是执行全新安装并删除你之前的系统——当然，要先备份重要数据文件。

接下来，安装程序会显示 SCSI 配置对话框，在其中你告诉系统系统中是否存在任何 SCSI 适配器。选择合适的按钮并继续。

如果你有 SCSI 适配器，程序将显示加载模块对话框，你可以在从中选择以下 SCSI 适配器：

- Iomega PPA3 (并行端口 Zip)
- NCR 5380
- NCR 53c406a
- NCR 53C810/53C820 PCI
- Pro Audio Spectrum/Studio 16
- Qlogic FAS
- Qlogic ISP
- Seagate ST012/02
- Trantor T128/T128F/T228
- UltraStor 14F/34F
- UltraStor 14F/24F/34F
- Western Digital wd7000

接下来，你必须对磁盘进行分区——或者至少选择你已经创建的分区。在“分区磁盘”（Partition Disks）对话框显示的列表框中选择你想要专用的驱动器，然后按 `<Return>` 或选择“编辑”（Edit）按钮。这将让你进入磁盘程序以对选定的硬盘进行分区。

## 使用 Linux `fdisk` 程序

在 `fdisk` 提示符下，输入 `m` 可命令列表。表 3.4 列出了可用的命令。

表 3.4 Linux `fdisk` 命令

| 命令 | 描述 |
| :--- | :--- |
| `a` | 切换启动标记 |
| `c` | 切换 DOS 兼容性标记 |
| `d` | 删除分区 |
| `l` | 列出已知的分区类型 |
| `m` | 显示此菜单 |
| `n` | 添加新分区 |
| `p` | 显示分区表 |
| `q` | 退出不保存更改 |
| `t` | 修改分区的系统 ID |
| `u` | 更改显示/输入单位 |
| `V` | 验证分区表 |
| `W` | 将表写入磁盘并退出 |
| `X` | 仅供专家提供的额外功能 |
