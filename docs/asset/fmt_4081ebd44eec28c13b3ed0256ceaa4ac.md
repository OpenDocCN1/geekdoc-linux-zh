
# 内核模块

```
[Kernel] [Modules] [Network] [Filesystems] [Previous]
View / Modify Loadable Kernel Configuration

Kernel Modules
Directory: [/lib/modules]           Modules Needed For Boot / Recovery
Detected Modules                                     [ ]
loop                                 /lib/modules/2.2/13/pcnet32.o
dac960                              /lib/modules/2.2/13/scsi/scsi_mod
ide-tape                             /lib/modules/2.2/13/scsi/sd_mod
ide-floppy                           /lib/modules/2.2/13/scsi/aic_prox.o
xd                                   /lib/modules/2.2/13/scsi/ips
cpqarras                             /lib/modules/2.2/13/fs/isofs
[X]Compatible Modules Only (More) [X]Autodetect Modules On Startup (More)
```

```
screen-Boot  date feb 14 as version 2.1.12 12:00
Temp: Recovery  dev:display:0  System#S500 Boot again
root: re-  verify Sec  Booting version 2 |kernel
```

图 226. 模块选项

你定义用于构建恢复系统初始 ramdisk 的模块。在 `Directory` 字段中，你可以指定与你定义的启动内核对应的模块路径。如果你选择 `Autoprobe Modules at Startup`（启动时自动探测模块），`RecoverEDGE` 将加载当前加载的模块。

> **注意**
>
> 不要忘记包含磁带驱动器的模块。

## 网络配置

6. 返回上一个阶段并选择 `Network`（网络）并按回车，你将看到一个与图 227 类似的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_287_0.png)

图 227. 网络选项

在这里定义网络设置，以便从网络上的磁带设备恢复系统。如果你有本地连接的磁带，则不需要此项。

## 文件系统配置

7. 返回上一个阶段并选择 `Filesystems`（文件系统）并按回车，你将看到一个与图 228 类似的窗口。

```
[Kernel] [Modules] [Network] [Filesystems] [Previous]
Select Filesystems For Restore
            Select Auto-Recover Filesystems
Non-Restorable (e. g. CD-ROM)          Restorable Filesystems
/proc                               "swap"
                               --> /boot
                                     /mnt/boot.rh
                                     /mnt/boot turbo
                                     /mnt/cdrom
                                     /mnt/root.rh
                                              (More)
```

![](img/2d69b129b41635ef36a3e6707d34b788_288_0.png)

图 228. 文件系统选项

在这里定义要恢复的挂载文件系统。

## 引导加载程序配置

8. 返回配置面板并选择 `Boot Loader`（引导加载程序）选项并按回车。你将看到一个与图 229 类似的窗口。

```
[Disk Layout] [Boot Loader] [Boot Media] [Previous]
Configure Boot Setup
            Boot Loader Configuration
[X] Boot Floppy with LILO          Configuration File: [/etc/lilo.conf ]
[X] Normal HD Boot Uses LILO
                                     Map File: [ ]
                                     Boot File: [/boot/boot.b ]
```

![](img/2d69b129b41635ef36a3e6707d34b788_288_1.png)

图 229. 引导加载程序选项

在此处定义引导加载程序（`Boot Loader`）的选项。

## 启动媒体配置

9. 返回配置面板，选择启动媒体（`Boot Media`）选项并按回车。你将看到一个与图 230 类似的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_289_0.png)

图 230. 启动媒体选项

在此处定义如何创建启动磁盘。

在制作磁盘之前，你需要修改 `RecoverEDGE` 工具的配置。要执行此操作，请打开 `/usr/lib/edge/recover2/OSFILES` 文件。

在该文件中进行以下更改：

- a. 删除行 `/bin/ash`。
- b. 将行 `/lib/ld.so` 改为 `/lib/ld-linux.so.1.9.9`。

10. 配置所有设置后，返回主窗口并选择制作磁盘（`Make Disks`）。系统将提示你插入三张磁盘。

> **注意事项**
>
> 如果你收到无法创建磁盘的错误，可能的原因是镜像太大。尝试减少加载的模块数量，甚至专门为此目的创建一个特殊的内核，丢弃所有不需要的内容。

*272 Caldera OpenLinux 和 Netfinity 服务器集成指南*

在你创建的磁盘准备好处理系统灾难之后。但在灾难真正发生之前，请尝试从这些磁盘启动并验证你的磁带设备是否被识别。

### 13.2.1.1 验证 RecoverEDGE 启动磁盘

要验证磁盘，从第一张磁盘启动并按照窗口上的说明操作。当系统启动时，你将看到 `RecoverEDGE` 主菜单。选择 `Utilities`（工具）-> `Tape Drive`（磁带驱动）。

在磁带设备节点（`Tape Device Node`）字段中，看到定义的磁带设备。转到 `Test Tape Drive`（测试磁带驱动）字段测试你的磁带设备。如果测试成功，恢复集即可使用。

### 13.2.2 从总崩溃中恢复

要从崩溃故障中恢复，请遵循以下步骤：

1. 解决所有硬件问题。

   > **注意**
   >
   > 在恢复系统之前，请初始化所有磁盘驱动器的主引导记录（`Master Boot Records`）。

2. 从第一张 `RecoverEDGE` 启动磁盘启动服务器。

3. 当提示插入根磁盘时，插入第二张 `RecoverEDGE` 启动磁盘。磁盘加载后，`RecoverEDGE` 将启动。

4. 选择 `Restore`（恢复）-> `One Touch`（一键恢复）。按照窗口上的说明完成恢复。

   > **注意**
   >
   > 恢复时你将使用你的主备份和增量备份。

5. 当所有文件备份完成后，按任意键返回主窗口。所有文件系统将将被同步，并设置并执行 `LILO`。

6. 在重启之前，按 `Alt+F2` 切换到控制台 2，并执行以下命令检查 `fstab` 文件以确保你的系统条目是否正确：

```
mount /dev/sdb6 /mount
cat /mount/etc/fstab
```

![](img/2d69b129b41635ef36a3e6707d34b788_290_0.png)

![](img/2d69b129b41635ef36a3e6707d34b788_290_1.png)

在我们的示例中，`sdb6` 是我们的根分区；你应该在此处使用你的根分区。

就是这些。你恢复的系统已准备就绪。

# 13.3 关于 Microlite 的更多信息

有关高级功能的信息，请参阅 `Microlite` 用户指南或 `Microlite` 网站：

```
http://www.microlite.com/
```

# 13.4 BRU

`BRU` 是一种备份和恢复工具，相比 `tar`、`cpio`、`volcopy` 和 `dump` 等其他常用工具有显著增强。`BRU` 设计用于大多数备份设备，包括带带、`4mm DAT`、`8mm (Exabyte)` 和 `9` 轨磁带机。

`BRU` 包含增量备份、全备份、多卷存档、发行和更新、错误检测与恢复、随机访问能力、文件比较、文件覆盖保护，以及比以前版本更高的速度。

## 13.4.1 安装 BRU

在开始之前，我们需要知道以下信息：

1. 磁带驱动器的设备名称。在 `Caldera OpenLinux` 下，它通常为 `/dev/st0`。

2. 备份介质的大小（单位为 `MB`）。

要使用 `tar` 命令从软盘器安装 `BRU`，请执行以下操作：

```
cd /tmp
tar xvf /dev/fd0
./install
```

按照 `readme` 文件和许可提示操作，直到出现以下窗口：

```
########################### 新 /etc/brutab 文件。此文件将包含
关于你系统中设备的信息。
###########################################
```

请从下列表中选择备份设备，或在完成后输入 `Q`。

- a) 1/4 英制带带驱动器
- b) 4mm DAT 磁带驱动器
- c) 8mm (Exabyte) 磁带驱动器
- d) DLT (数字线性磁带)
- e) 其他
- q) 退出

此设备的类型是：-

图 231 选择你的备份设备

1. 选择所有的备份设备，完成后输入 `Q`。
2. 磁盘加载后，`RecoverEDGE` 将启动。
3. 当提示插入根磁盘时，插入第二张 `RecoverEDGE` 启动磁盘。
4. 选择 `Restore` -> `One Touch`。按照窗口上的说明完成恢复。
5. 当所有文件备份完成后，按任意键返回主窗口。所有文件系统将将被同步，并设置并执行 `LILO`。
6. 在重启之前，按 `Alt+F2` 切换到控制台 2，并执行以下命令检查 `fstab` 文件以确保你的系统条目是否正确：

> **注意**
>
> 在恢复系统之前，请初始化所有磁盘驱动器的主引导记录。
>
> 恢复时你将使用你的主备份和增量备份。

在我们的示例中，`sdb6` 是我们的根分区；你应该在此处使用你的根分区。

就是这些。你恢复的系统已准备就绪。

### 13.2.1.1 验证 RecoverEDGE 启动磁盘

要验证磁盘，从第一张磁盘启动并按照窗口上的说明操作。当系统启动时，你将看到 `RecoverEDGE` 主菜单。选择 `Utilities`（工具）-> `Tape Drive`（磁带驱动）。

在磁带设备节点（`Tape Device Node`）字段中，看到定义的磁带设备。转到 `Test Tape Drive`（测试磁带驱动）字段测试你的磁带设备。如果测试成功，恢复集即可使用。

### 13.2.2 从总崩溃中恢复

要从崩溃故障中恢复，请遵循以下步骤：

1. 解决所有硬件问题。
2. 从第一张 `RecoverEDGE` 启动磁盘启动服务器。
3. 当提示插入根磁盘时，插入第二张 `RecoverEDGE` 启动磁盘。
4. 选择 `Restore` -> `One Touch`。按照窗口上的说明完成恢复。
5. 当所有文件备份完成后，按任意键返回主窗口。所有文件系统将将被同步，并设置并执行 `LILO`。
6. 在重启之前，按 `Alt+F2` 切换到控制台 2，并执行以下命令检查 `fstab` 文件以确保你的系统条目是否正确：

```
mount /dev/sdb6 /mount
cat /mount/etc/fstab
```

# 13.3 关于 Microlite 的更多信息

有关高级功能的信息，请参阅 `Microlite` 用户指南或 `Microlite` 网站：

```
http://www.microlite.com/
```

# 13.4 BRU

`BRU` 是一种备份和恢复工具，相比 `tar`、`cpio`、`volcopy` 和 `dump` 等其他常用工具有显著增强。`BRU` 设计用于大多数备份设备，包括带带、`4mm DAT`、`8mm (Exabyte)` 和 `9` 轨磁带机。

`BRU` 包含增量备份、全备份、多卷存档、发行和更新、错误检测与恢复、随机访问能力、文件比较、文件覆盖保护，以及比以前版本更高的速度。

## 13.4.1 安装 BRU

在开始之前，我们需要知道以下信息：

1. 磁带驱动器的设备名称。在 `Caldera OpenLinux` 下，它通常为 `/dev/st0`。

2. 备份介质的大小（单位为 `MB`）。

要使用 `tar` 命令从软盘器安装 `BRU`，请执行以下操作：

```
cd /tmp
tar xvf /dev/fd0
./install
```

按照 `readme` 文件和许可提示操作，直到出现以下窗口：

```
########################### 新 /etc/brutab 文件。此文件将包含
关于你系统中设备的信息。
###########################################
```

请从下列表中选择备份设备，或在完成后输入 `Q`。

- a) 1/4 英制带带驱动器
- b) 4mm DAT 磁带驱动器
- c) 8mm (Exabyte) 磁带驱动器
- d) DLT (数字线性磁带)
- e) 其他
- q) 退出

存档。备份将通过向您显示预计的完成时间和进度窗口来进行。

## 13.4.4.2 调度

要访问调度功能，请选择 `文件 (File)` -> `调度器 (Scheduler)`。

![](img/2d69b129b41635ef36a3e6707d34b788_296_0.png)

图 234. 调度器

`BRU` 提供了一个调度工具，为忙碌的管理员自动化备份过程。有三种预定义的定义：全量（`Full`）、1级（`Level 1`）和2级（`Level 2`）。这些与 13.4.4 节中定义相同，即第 277 页上的“大按钮”。您可以在创建存档界面中创建自己的定义。

通过 `BRU for X11` 调度器界面，您可以根据每周、每月或特定日期设置调度备份。调度器非常灵活。为了利用调度选项，您必须保存所需的调度配置，并验证调度器正在通过 `cron` 运行。要验证或添加 `cron` 条目，请以 `root` 身份登录并输入：

```
crontab -e
```

插入以下行：

```
0/5 * * * * /usr/local/bin/bruschedup
```

如果您在安装期间为二进制文件选择了不同的路径，请相应更改条目。

保存 `crontab` 条目。您现在可以调度备份了。

## 13.4.4.3 恢复文件

使用 `BRU X` 界面恢复文件非常简单。当您点击 `恢复 (Restore)` 按钮时，`BRU` 将检索存档的内容。扫描存档后，将出现 `恢复文件选择 (Restore File Selection)` 界面（类似于图 233）。

> **注意**
>
> 如果磁带目录不在存档中，`BRU` 必须扫描整个存档以获取列表。这可能非常耗时。创建存档时，请使用 `-G` 选项创建磁带目录。

![](img/2d69b129b41635ef36a3e6707d34b788_297_0.png)

左侧的框显示存储在磁带上的当前目录内容。您可以通过点击窗口右上角并编辑 `CD` 条目来更改当前目录。

您可以通过选择文件和目录并选择相应的按钮来从备份列表中添加或删除它们。

当您选择了所有想要恢复的文件和目录后，点击 `恢复` 按钮。进度窗口将显示每个文件的恢复情况。

## 13.4.4.4 列出和验证存档

要列出存档内容，`BRU` 提供了三个选项：

1. `头 (Header)` - 此选项显示存档头记录，列出标签、创建日期、版本和序列号。关于头的更多信息，请参阅《BRU 用户指南》。

2. `仅文件名 (Filenames only)` - 此选项显示磁带目录。创建存档时没有使用 `-G` 选项，`BRU` 将扫描存档以创建文件列表。在此发生之前您将收到提示，因为这是一个漫长时间的过程。

3. `详细信息 (Full details)` - 此选项扫描整个存档以获取文件名、权限、所有者、大小、修改时间等细节。这可能非常耗时。

对于验证存档，`BRU` 提供了两个选项：

1. `校验和验证 (Checksum Verification)` - 写入存档时，会对每个数据块计算校验和。校验和存储在每个块的头部。校验和验证将读取每个块，重新计算校验和，并将校验和与头部中的值进行比较。每个文件在验证时将分别列出，以及发现的任何错误。如果没有发现错误，您就知道备份是准确的。

2. `差异验证 (Differences Verification)` - `BRU` 将存档中的文件与硬盘上的文件进行比较。记录任何差异，例如修改时间、大小或存档中存在但硬盘上不存在的文件。验证完成后，将列出“差异结束”的通知。

## 13.4.5 总结

有关高级功能的信息，请参阅您的《BRU 用户指南》或访问 `BRU` 网站：

```
http://www.estinc.com/
```

## 附录 A RAID 级别
