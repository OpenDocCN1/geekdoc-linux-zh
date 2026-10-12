
> **注意：** 本节内容与第 4 章中的启动盘部分内容密切相关（并在某种程度上有所重复）。如果你正在使用带有 `PPC` CPU 的计算机，可以使用系统管理服务（System Management Services）菜单将系统设置为从 `CD` 启动。如果你正在使用 `Itanium` 系统，可以通过 `EFI shell` 进行设置。如果你正在使用 `IBM S/390`，可以配置系统从虚拟机 (`VM`) 或逻辑分区 (`LPAR`) 启动，这与标准的 `PC` 硬盘逻辑分区不同。虽然本书书侧重于在 `x86` 或 `AMD64` 上进行安装，但你可以通过 `Red Hat` 安装文档找到更多关于其他架构的信息，可在 `www.redhat.com/doc/manuals/enterprise` 在线。

#### 创建启动盘或驱动盘

`Red Hat Enterprise Linux` 提供了四种工具来帮助你创建启动和驱动软盘。其中两个（`dd` 和 `cat`）在 `Linux` 中运行；另外两个（`WRITE` 和 `RAWWRITE`）在 `Microsoft Windows` 中运行。这些工具是你可以从其他 `Linux` 或 `Unix` 系统运行的标准命令；镜像文件和 `Microsoft` 工具可以在第一张 `Red Hat Enterprise` 安装 `CD` 上找到。

如果你当前正在运行 `Linux` 计算机，请按照以下步骤创建启动盘。记住，正如后续章节所述，你可能需要一张或多张驱动盘。

1. 在命令行界面，找到镜像文件。例如，如果你使用命令：

```
#### mount /mnt/cdrom
```

来挂载第一个 `Red Hat Enterprise Linux` 安装 `CD`，则镜像文件将位于 `/mnt/cdrom/images` 目录。

2. 将一张 `1.44MB` 磁盘插入软盘驱动器。你不需要对该驱动器使用 `mount` 命令。

3. 使用以下命令之一将启动盘镜像 `bootdisk.img` 转换为软盘上的系列文件（`/dev/fd0` 是你计算机上第一个软盘驱动器的关联设备）：

```
#### dd if=/mnt/cdrom/bootdisk.img of=/dev/fd0
#### cat /mnt/cdrom/images/bootdisk.img > /dev/fd0
```

4. 对 `images` 目录中可能需要的任何驱动盘重复这些步骤。

如果你在 `Microsoft Windows` 中并想从命令行界面创建启动盘，请按照以下步骤创建该磁盘。记住，正如后续章节所述，你可能还需要为一个或两个驱动盘重复此过程。

1. 将第一张 `Red Hat` 安装 `CD` 插入驱动器。这些步骤假设它是 `F:` 驱动器，但如果你的驱动器号不同，请相应替换。

2. 进入 `MS-DOS` 提示符。选择“开始” > “运行”。在出现的运行对话框中，在文本框输入 `CMD` 并按回车。这将打开一个命令提示符窗口。

3. 在命令窗口中输入 `F:` 工具并运行以下命令；在提示时将一张 `1.44MB` 磁盘插入软盘驱动器：

```
F:\>DOSUTIL/WRITE.EXE
Enter disk source file name: /IMAGES/BOOTDISK.IMG
Enter target diskette drive: A:
Please insert a formatted diskette into drive A and press -ENTER:-
```

5. 对 `IMAGES` 目录中其他所需的磁盘镜像重复此过程。

你也可以使用 `Microsoft Windows` 通过使用 `RAWWRITEWIN.EXE` 工具创建启动盘，正如后续章节所述，你可能还需要一个或两个驱动盘。

1. 将第一张 `Red Hat` 安装 `CD` 插入驱动器。这些步骤假设 `CD` 使用的是 `H:` 驱动器，但如果你的驱动器号不同，请相应替换。

# 第 3 章：在独立系统上安装 LINUX

2. 进入该工具。打开 `Microsoft Windows` 资源管理器。选择“开始” > “运行”。在出现的对话框中，在文本框输入 `EXPLORER` 并按回车。这将打开 `Microsoft Windows` 资源管理器。

3. 导航到 `H:` 驱动器，然后进入 `DOSUTILS` 文件夹内的 `RAWWRITEIN` 文件夹。然后你可以双击 `RAWWRITEIN.EXE` 工具。（是的，`RAWWRITEIN` 文件夹的拼写与 `RAWWRITEIN.EXE` 工具不同：）

4. 这将打开 `Raw Write` 对话框，如图 3.1 所示。如有必要，创建“Write”选项卡。点击“Image File”框右侧的按钮；你应该能够在“打开”对话框从 `H:IMAGES` 目录访问你选择的镜像文件。

# 图 3.1

使用 `RawWrite` 创建启动软盘

![](img/2feb3b41073cd1ed27e138a1bee4a0f2_85_0.png)

5. 将一张 `1.44MB` 磁盘插入软盘驱动器，并点击 `Write`。对其他所需的磁盘镜像重复此过程。

# 分析 Red 启动软盘

无论你用什么创建它，`Red Hat Enterprise Linux` 软盘的目的和内容保持不变。

> **注意：** 本节内容密切相关（并在某种程度上有所重复）第 4 章中的启动盘部分。如果你正在使用带有 `PPC` CPU 的计算机，可以使用系统管理服务菜单将系统设置为从 `CD` 启动。如果你正在使用 `Itanium` 系统，可以通过 `EFI shell` 进行设置。如果你正在使用 `IBM S/390`，可以配置系统从虚拟机 (`VM`) 或逻辑分区 (`LPAR`) 启动，这与标准的 `PC` 硬盘逻辑分区不同。虽然本书侧重于在 `x86` 或 `AMD64` 上进行安装，但你可以通过 `Red Hat` 安装文档找到更多关于其他架构的信息，可在 `www.redhat.com/doc/manuals/enterprise` 在线。

无论你用什么创建它，`Red Hat Enterprise Linux` 软盘的目的和内容保持不变：`images` 目录下的 `bootdisk.img`。

如图 3.2 所示，`syslinux.cfg` 文件提供了后续操作的路线。表 3.2 描述了关键命令并有助于解释 `syslinux.cfg`。

**提示：** 你可以使用 `Red Hat` 启动软盘或 `CD` 作为救援磁盘。使用第 11 章描述的技术，它可以帮助你从故障中恢复。

# 图 3.2

`Linux` 启动

```
default linux
prompt
timeout 600
display boot.msg
f1 boot.msg
f2 options.msg
f3 general.msg
f4 parse.msg
f5 rescue.msg
f7 snake.msg
label linux
    kernel vmlinux
    append initrd+initrd.img
label text
    kernel vmlinux
    append initrd+initrd.img
label export
    kernel vmlinux
    append initrd+initrd.img
label lowres
    kernel vmlinux
    append initrd+initrd.img
```

# 表 3.2：SYSLINUX.CFG 中的命令

| 命令 | 描述 |
|---|---|
| `default` | 指定默认启动选项，在此情况下为 `linux`。 |
| `prompt` | 设置启动：提示。 |
| `timeout` | 配置启动盘自动启动默认选项之前的延迟时间（单位为秒），通常设置为 `600`，即一分钟。 |
| `display` | 指向显示在屏幕上的初始消息文件。 |
| `option.msg` | 设置与特定消息文件关联的功能键。 |
| `label` | 指定与之关联的操作。 |
| `kernel` | 设置启动磁盘上压缩内核的名称。 |
| `append` | 添加启动磁盘加载内核的参数。 |
| `initrd` | 指定初始 RAM 磁盘。 |
| `text` | 以文本模式启动；见第 4 章。 |
| `expert` | 以专家模式启动，在其中指定硬件驱动程序。 |
| `ks` | 使用 `Kickstart` 文件启动；见第 5 章。 |
| `lowres` | 以低分辨率 ×`640×400` 图形模式和基本 `VESA` (`SVGA`) 驱动程序启动安装。 |

# 分析存储设备驱动器磁盘

如果 `Anaconda` 检测到电脑连接了硬盘，你无法安装红帽企业 Linux（`Red Hat Enterprise Linux`）。标准的启动磁盘（`bootdisk.img`）通常可以识别标准的 `IDE`、`SCSI` 甚至连接到 `PC` 的某些 `USB` 硬盘；所需的驱动程序已集成在压缩后的内核中。

这就是为什么你可能想要从第一张红帽企业 Linux 安装光光盘的 `images` 目录下的 `drvblock.img` 文件创建一个 `1.44MB` 的软盘。使用本章早些描述的任何技术来创建此磁盘。它在软盘上加载 5 个文件，我在表 3.3 中简要描述了它们。
