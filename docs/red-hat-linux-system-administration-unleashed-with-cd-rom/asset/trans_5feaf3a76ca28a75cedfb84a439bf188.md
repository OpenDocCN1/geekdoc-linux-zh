
为了构建合适的 ISO 命令行，我们首先使用 -scanbus 选项发出 cdrecord 命令。这为我们提供了要使用的适当设备条目。然后我们指定写入磁盘的写入速度。在本例中，附带的刻录机以 4 倍速写入，因此我们指定速度为 4。如果在刻录图像时机器完全空闲，有时可以将速度设置为高于设备指定的速度。然而，在实际刻录 CD-R 光盘之前，您可能希望使用 -dummy 选项先尝试一下，看看是否可行。-dummy 选项会执行刻录 CD-R 的所有步骤，只是不会激活激光。它是一个非常有用的调试工具，可以帮您避免制造太多金色 coaster。其他选项指定您想要详细输出并使用 ISO9660 文件系统大小作为下一轨道的大小。刻录完成后，您接下来应该做的是验证写入是否成功。为此，您只需挂载创建的 CD 并尝试从中读取即可。

现在您已经知道如何在 Linux 下向 CD-R 和 CD-RW 驱动器写入数据，您可以出于各种目的使用这些知识。其中一个用途可以是创建内核或其他软件构建的备份。其他用途包括专用备份；例如，您必须保留但不足以写入磁带的网站日志文件，或您希望快速访问的文件。另一个变得流行的用途是创建您不经常使用但在需要时希望快速访问的软件包映像。现在我们已经介绍了 CD 的创建，我们可以继续讨论其他可移动媒体设备，从连接到系统并口的设备开始。

## 并口存储设备

最近变得相当流行的其他可移动媒体设备是经由并口连接到计算机的存储设备。这些设备包括 Iomega 的驱动器，如 Zip 和 Jaz 驱动器，它们使用驱动程序使它们在 Linux 中表现为 SCSI 设备，以及 SyQuest 和 MicroSolutions 等其他制造商的 ATAPI/IDE 设备。本节将介绍为这些类型的设备向内核添加支持所需的条件，然后特别介绍 Zip 驱动器，因为它们是这些设备中较为流行的一种。本讨论仅涉及连接到并口的 Zip 驱动器。如果您的 Zip 驱动器连接到 IDE 控制器或 SCSI 控制器，它应作为另一个 SCSI 或 IDE 设备出现在系统中。

## 向内核添加支持

为并口存储设备向内核添加支持的第一步是确定您需要哪个驱动程序。基本上共有三种选择。其中第一个是 ppa 驱动程序，适用于较旧的并口 Zip 驱动器。对于较新的 Zip 驱动器，如 ZIP Plus 和 250 兆字节 Zip 驱动器，请使用 imm 驱动程序（Iomega MatchMaker）。这两个驱动程序都是 Linux SCSI 支持的一部分，并在内核配置中配置为低级 SCSI 驱动程序。对于并口 ATAPI 或 IDE 设备，有一个名为 paride 的驱动程序。该驱动程序适用于通过并口连接的多种外部存储设备，包括以下内容：

- MicroSolutions 背包 CD-ROM
- MicroSolutions 背包 PD/CD
- MicroSolutions 背包硬盘
- MicroSolutions 背包 8000t 磁带驱动器
- SyQuest EZ-135、EZ-230 & SparQ 驱动器
- Avatar Shark
- Imation Superdisk LS-120
- Maxell Superdisk LS-120
- FreeCom Power CD
- Hewlett-Packard 5GB 和 8GB 磁带驱动器
- Hewlett-Packard 7100 和 7200 CD-RW 驱动器

为 ppa 或 imm 驱动程序添加支持的步骤与为任何其他类型的 SCSI 设备添加支持的步骤相同。您必须首先选择 SCSI 设备的支持，然后选择特定类型的 SCSI 设备（磁盘、CD、磁带和通用），最后选择控制器的特定低级驱动程序。在低级驱动程序级别，您选择 ppa 或 imm 驱动程序。这些选项根据它们支持的 Zip 驱动器类型明确标记，如果您对哪个驱动程序合适还有进一步疑问，内核配置帮助包含有价值的信息。

paride 支持配置选项位于内核配置的块设备部分。您必须首先回答并口 IDE 设备支持问题，使用 M 构建为模块或 Y 编译到内核中。然后您将被提示选择要支持的设备类型，与 SCSI 设备配置类似。完成此操作后，您需要根据要支持的设备类型选择一个或多个协议模块。再次强调，配置帮助在这里是您的朋友，如果不确定，您可以启用所有协议作为模块，让驱动程序自行判断。

假设您使用的是 Red Hat 6.1 发行版提供的内核，并且使用的是随附的 2.2.12 内核，则无需执行上述任何步骤。内核已配置好，并将 ppa、imm 和 paride 驱动程序以及相关协议作为模块支持。

## Zip 驱动器

假设您使用的是默认的 Red Hat 内核，或已成功重新构建内核以支持第 35 章所述的您拥有的 Zip 驱动器类型，您实际上如何使用该驱动器？涉及两个基本步骤：

- 1. 加载适当的驱动模块。
- 2. 装入 Zip 磁盘并使用它。

加载模块只需使用 insmod 或 modprobe 并指定正确的驱动程序。为本示例的目的，我们假设使用 imm 驱动程序的现代 ZIP Plus 驱动器。在这种情况下，您将发出的命令和示例输出如下

```
[root@wizard root]# modprobe -a imm
imm: Version 2.0.03 (for Linux 2.0.0)
imm: Found device at ID 6, Attempting to use EPP 32 bit
imm: Communication established with ID 6 using EPP 32 bit
scsi0 : Iomega VP12 (imm) interface
scsi : 1 host.
Vendor: IOMEGA   Model: ZIP 100        Rev: J.67
Type: Direct-Access  ANSI SCSI revision: 02 Detected scsi removable disk sda
at scsi0, channel 0, id 6, lun 0
SCSI device sda: hdwr sector= 512 bytes, Sectors= 196608 [96 MB] [0.1 GB]
sda: Write Protect is off
sda: sda4
```

您可能会注意到驱动器中的 Zip 磁盘被检测为 /dev/sda，并且它有一个单独的分区 sda4。分区编号为 4 的原因存在争议；然而，到目前为止最好的解释是 Macintosh 用于 Zip 驱动器的工具要求如此，并且所有磁盘都以这种方式分区以实现兼容性。

现在驱动程序已加载且磁盘已被识别，是时候开始实际使用磁盘了。这里有三种情况。第一种是您将使用预先格式化为 Windows 的 Zip 磁盘。在这种情况下，您必须创建挂载点，然后使用以下命令挂载磁盘并开始使用：

```
mkdir /mnt/zip; mount -t vfat /dev/sda4 /mnt/zip
```

磁盘上的文件系统现已挂载，您可以像访问任何其他已挂载的 vfat 分区一样访问它，使用标准 Linux 命令如 ls、cp、mv 和 rm。如果您更喜欢在 Zip 磁盘上使用 Linux 文件系统，可以使用以下命令在磁盘上创建 Linux 分区和文件系统：

```
echo ",," | /sbin/sfdisk /dev/sda ; mk2fs /dev/sda1
```

这会在磁盘上创建一个占用整个磁盘的单个 Linux 分区 /dev/sda1，然后在其上创建文件系统。完成此操作后，您可以挂载新创建的 ext2 文件系统，并像对待任何其他磁盘一样对待它。

## 并口 ATAPI/IDE 设备

连接到系统并口的其他设备，例如 Imation SuperDisk LS-120 或任何 MicroSolutions 背包设备，也得到支持。

这些设备使用的是 Linux 2.2.x 内核的一部分的 paride 驱动程序。与 Zip 驱动器支持一样，使用这些设备只需加载适当的模块，然后通过适当的设备名称访问设备，前提是您已配置内核以支持它们。在这种情况下，需要加载的模块分为三类：

- 提供并口的注册表和基本控制的 paride 模块。
- 用于已连接设备的协议模块。
- 用于特定设备类型的上层模块，例如磁盘驱动器、CD 驱动器或软盘驱动器。

例如，如果您将 SyQuest EZ135A 驱动器连接到系统，您需要的模块是 paride 模块、epat 协议模块和 pd 磁盘模块。在这种情况下，安装这些模块后产生的输出可能如下所示：

```
[root@wizard etc] insmod paride
paride: version 1.0 installed

[root@wizard etc] insmod epat
paride: epat registered as protocol 0

[root@wizard etc] insmod pd
```
