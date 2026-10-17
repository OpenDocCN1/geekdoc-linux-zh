
如果你有一个 SCSI 磁盘，设备名称将为 `/dev/sda`；如果你有一个 IDE 磁盘，它将是 `/dev/hda`。如果你追求高性能和稳定性，强烈建议使用 SCSI 磁盘。

Linux 使用磁盘和数字的组合来指代分区。它使用的命名方案比其他操作系统使用的方法更灵活，并能传递更多信息。

以下是摘要：

- **前两个字母** – 分区名称的前两个字母表示分区所所在的设备类型。你通常会看到 `hd`（用于 IDE 磁盘）或 `ed`（用于 SCSI 磁盘）。
- **接下来的字母** - 这表示分区位于哪个设备上。例如：`/dev/hda`（第一个 IDE 硬盘）和 `/dev/hdb`（第二个 IDE 磁盘），以此此类推。

请记住这些信息，当你设置 Linux 所需的分区时，这会让理解变得更加简单。

**现在，举个例子：**

针对你系统中列出的下方分区（这是我们服务器安装示例所需的的分区）；以下命令用于 `Disk Druid`。

### 步骤 1

使用 `Disk Druid` 执行所有以下命令以创建所需的分区。

```
New
Mount Point: /boot
Filesystem Type: ext3
Size (Megs): 24
Ok
```

```
New
Mount Point: /
Filesystem Type: ext3
Size (Megs): 256
Ok
```

```
New
Mount Point: /usr
Filesystem Type: ext3
Size (Megs): 512
Ok
```

```
New
Mount Point: /home
Filesystem Type: ext3
Size (Megs): 4512
Ok
```

```
New
Mount Point: /chroot
Filesystem Type: ext3
Size (Megs): 256
Ok
```

## 安装问题

第 2 章

```
New
Mount Point: /var
Filesystem Type: ext3
Size (Megs): 512
Ok
```

```
New
Mount Point: /var/lib
Filesystem Type: ext3
Size (Megs): 1024
Ok
```

```
New
Mount Point: /tmp
Filesystem Type: ext3
Size (Megs): 256
Ok
```

```
New
Mount Point: swap
Filesystem Type: swap
Size (Megs): 1372
Ok
```

### 步骤 2

在你执行上述命令用 `Disk Druid` 创建并划分驱动器后，按下 `Next` 按钮继续安装，以选择要格式化的分区。

## 使用 fdisk 进行分区

本节仅适用于你选择使用 `fdisk` 对系统进行分区的情况。

你想要做的第一件事是使用 `p` 键检查当前分区信息。你需要添加根分区。使用 `n` 键创建新分区，然后选择 `o` 或 `p` 键来创建扩展分区或主分区。

你可能想要创建一个主分区。系统会询问给它分配哪个分区号，并给出分区起始位置的范围——只需选择最小的数字（1）以及分区的大小。例如，对于一个 5MB 的分区，在被询问大小时，输入 `+5M`。

接下来，你确实需要扩展你的分区。使用 `n` 键创建新分区，并选择 `e` 键创建扩展分区。系统会询问给它分配哪个分区号，并给出分区起始位置的范围——只需选择最小的数字（2）以及分区的大小。在被询问时，输入最后一个数字（或按回车键）。

你现在想要创建交换分区（swap）。你需要使用 `n` 键创建新分区。选择逻辑选项；告诉它第一个磁道将是 (2)。告诉 `fdisk` 你想要交换分区有多大。然后使用 `t` 键更改分区类型并输入交换分区的分区号。输入十六进制代码 `82`。

现在你已经创建了 boot 分区和交换分区，是时候添加任何需要的其他分区了。再次使用 `n` 键创建分区，并按照之前的方法输入信息。重复此过程直到创建所有分区；然后你必须使用 `w` 命令保存并退出。

注意：只有在使用 `w` 命令保存并退出 `fdisk` 后，你的更改才会生效。你可以随时使用 `q` 命令退出而不保存更改。

### fdisk 概览

- `m` 命令显示帮助
- `p` 命令列出分区表
- `n` 命令添加新分区
- `d` 命令删除分区
- `t` 命令设置或更改分区类型
- `l` 命令提供不同类型的列表
- `w` 命令保存信息并退出

现在，作为一个例子：在你的系统中列出下方分区（这些是我们安装所需的的分区）；以下命令用于 `fdisk`：

步骤 1

使用 `fdisk` 执行所有以下命令创建所需的分区。

```
Command (m for help): n
Command action: e extended
p partition (1-4)
Partition number (1-4): 1
First cylinder (1-1116, default 1): 1
Last cylinder +size or +K (1-1116, default 1116): +256M
Command (m for help): n
Command action: e extended
p partition (1-4)
Partition number (1-4): 2
First cylinder (4-1116, default 4): 4
Last cylinder +size or +K (4-1116, default 1116): +512M
Command (m for help): n
Command action: e extended
p partition (1-4)
Partition number (1-4): 3
First cylinder (37-1116, default 37): 37
Last cylinder +size or +K (37-1116, default 1116): +512M
Command (m for help): n
Command action: e extended
p partition (1-4)
Partition number (1-4): 4
First cylinder (103-1116, default 103): 103
Last cylinder +size or +K (103-1116, default 1116): +1024M
Command (m for help): n
Command action: e extended
p partition (1-4)
Partition number (1-4): 5
First cylinder (679-1116, default 679): 679
Last cylinder +size or +K (679-1116, default 1116): +256M
Command (m for help): n
Command action: e extended
p partition (1-4)
Partition number (1-4): 6
First cylinder (712-1116, default 712): 712
Last cylinder +size or +K (712-1116, default 1116): +512M
Command (m for help): n
Command action: e extended
p partition (1-4)
Partition number (1-4): 7
First cylinder (778-1116, default 778): 778
Last cylinder +size or +K (778-1116, default 1116): +1024M
Command (m for help): n
Command action: e extended
p partition (1-4)
Partition number (1-4): 8
First cylinder (909-1116, default 909): 909
Last cylinder +size or +K (909-1116, default 1116): +256M
Command (m for help): n
Command action: e extended
p partition (1-4)
Partition number (1-4): 9
First cylinder (942-1116, default 942): 942
Last cylinder +size or +K (942-1116, default 1116): 1116
Command (m for help): t
Partition number (1-12): 12
Hex code (type L to list codes): 82
Changed system type of partition 12 to 82 (Linux swap)
```

### 步骤 2

现在使用 `p` 命令列出我们创建的分区，你的屏幕上应该看到如下内容。

```
Command (m for help): p

Disk /tmp/sda: 255 heads, 63 sectors, 1116 cylinders

Units = cylinders of 16065 * 512 bytes

| Device | Start | End | Blocks | Id | System |
|---|---|---|---|---|---|
| /tmp/sda1 | 1 | 1116 | 24066 | 83 | Linux |
| /tmp/sda2 | 4 | 26540 | 894172 | 5 | Extended |
| /tmp/sda5 | 37 | 102 | 530113 | 83 | Linux |
| /tmp/sda6 | 103 | 678 | 426688 | 83 | Linux |
| /tmp/sda7 | 679 | 711 | 265041 | 83 | Linux |
| /tmp/sda9 | 712 | 777 | 530113 | 83 | Linux |
| /tmp/sda10 | 778 | 908 | 265041 | 83 | Linux |
| /tmp/sda12 | 909 | 1116 | 1406566 | 82 | Linux Swap |
```

# 引导程序安装

在下一个屏幕上，你将看到引导程序配置界面。为了启动你的 Linux 系统，你通常需要安装一个引导程序。随着 Linux 的新版本发布，你可以选择安装 `GRUB`、`LILO`，或者选择不安装引导程序。

`GRUB` 是启动 Linux 的新且推荐的方法。你仍然可以决定使用 `LILO`，但现在最好使用 `GRUB`。从此界面，你将看到与 `GRUB` 或 `LILO` 相关的不同可配置选项。

第一个选项是：

- 使用 `GRUB` 作为引导程序

此选项允许你使用 `GRUB` 软件作为引导程序，在计算机上启动你的 Linux 操作系统。这是使用 Linux 的推荐方法。`GRUB` 的工作方式与 `LILO` 相同，但提供了许多 `LILO` 无法提供的额外安全和高级功能。在我们的设置中，我们使用此选项启动 Linux 服务器。

第二个选项是：

- 使用 `LILO` 作为引导程序

此选项允许你使用 `LILO` 软件作为引导程序，在计算机上启动你的 Linux 操作系统。记住，`LILO` 现在是启动 Linux 的旧方法，如果你想跟上 Linux 世界最新的技术，我建议你使用 `GRUB`。在我们的设置中，我们不选择此选项。

第三个选项是：

- 不安装引导程序

此选项允许你跳过为 Linux 安装任何类型的可用引导程序（`GRUB` 或 `LILO`）。如果你使用启动引导盘而不是 `GRUB` 或 `LILO` 来启动操作系统，那么此选项将很有用。在某些情况下，如果你需要一个带有内核的可启动 Linux 软盘来启动服务器，这可以极大地提高安全性。另一方面，如果发生故障，你将无法远程重启服务器。在我们的设置中，我们不使用此选项。

第四个选项是：

- 主引导记录 (MBR)
- 分区第一个扇区

通常，如果 Linux 是你机器上唯一的操作系统（这在服务器安装中必须是这种情况），你应该选择“主引导记录 (MBR)”选项。MBR 是硬盘上的一个特殊区域，由计算机的 BIOS 自动加载，是引导程序能够接管引导过程的最早点。

第五个选项是：

- 强制使用 LBA32

此选项（如果勾选）允许你突破 `/boot` 分区超过 1024 柱道的限制。如果你的系统支持 LBA32 扩展来启动位于 1024 柱道限制以上的操作系统，并且你想将 `/boot` 分区放在 1024 柱道之上，则你应该选择此选项，但在大多数情况下你不需要，你的系统将完美运行。在我们的系统设置中，不要使用它。

![](img/62d23c0d98be09825cf9e4c822190362_39_0.png)

## GRUB 密码

此部分仅适用于选择 `GRUB` 作为引导程序的情况。如果你正在安装 `GRUB` 密码，你应该创建一个密码来保护你的系统。如果没有 `GRUB` 密码，访问你系统的用户可以向内核传递选项，从而危及你的系统安全。设置 `GRUB` 密码后，必须输入密码才能选择任何非标准的启动选项。

![](img/62d23c0d98be09825cf9e4c822190362_39_1.png)

## 网络配置

之后，你需要配置网络。如果你有多个以太网设备，每个设备将有自己的配置屏幕。你将被要求输入 IP 地址、网络掩码、广播地址和网关、主 DNS（如果适用还有次级 DNS 和三级 DNS）地址。你应该了解所有信息，或者你可以要求你的系统管理员帮助你获取正确的信息。

![](img/62d23c0d98be09825cf9e4c822190362_40_0.png)

## 防火墙配置

在安装的这部分，我们有机会配置防火墙。这对于普通用户来说可以，但对于专业的防火墙安全来说。这个新添加的功能使用了 Linux 旧的 IPTCHAINS 工具，配合一个名为“lokkit”的小工具来设置你的防火墙。

我强烈建议你现在禁用此功能，并在本书的后部分查看如何使用 IPTTable 安装和配置 IPTables，这是用于 Linux 和内核 2.4 时代的新型防火墙工具。IPTables 仅仅是一个防火墙软件，它可以帮助你以比任何其他防火墙软件提供的更安全、更简单的方式配置 IPTables。

在下一个屏幕，你将看到三个不同的安全级别，选择“无防火墙”选项并点击**下一步**。

## 红帽 Linux

![](img/62d23c0d98be09825cf9e4c822190362_41_0.png)

## 防火墙配置

如果你想在计算机和网络之间启用防火墙保护，请记住，对于网络上的远程用户，配置良好的防火墙可以极大增强系统的安全性。

选择系统的安全级别。

- 高安全性：通过关闭你显式定义之外的所有系统端口，只允许必要的连接。

## 语言支持选择

随着国际化，对语言支持的需求已经出现。从这里开始，安装程序要求你选择在安装完成后在 Linux 系统上使用的默认语言。如果你在系统中只使用一种语言，只选择这种语言将节省大量的磁盘空间。

![](img/62d23c0d98be09825cf9e4c822190362_41_1.png)

## 语言支持选择

选择作为默认的语言。默认语言将用于整个 Linux 系统。如果安装了多种语言，可以随时更改默认语言。你可以选择要安装的特定语言，或系统中所有的可用语言。

使用重置按钮取消你的选择。

## 时区选择

在下一个屏幕，你将有机会设置时区。一旦选择，点击下一步。

![](img/62d23c0d98be09825cf9e4c822190362_42_0.png)

## 账户配置

在时配置之后，你现在需要为系统设置 root 密码账户。

![](img/62d23c0d98be09825cf9e4c822190362_42_1.png)

## 身份验证配置

最后一个阶段是身份验证。

- 启用 MD5
- 影子密码

![](img/62d23c0d98be09825cf9e4c822190362_43_0.png)

## 选择软件包组

在分区完成后，我们准备好选择要安装的组件，在我们的情况下；我们**取消勾选所有已选的软件包组**。

我们不需要也不想安装任何额外的软件包。该 Linux 发行版的默认安装程序已经包含了操作系统基础功能所需的最核心程序。

![](img/62d23c0d98be09825cf9e4c822190362_45_0.png)

## 第 2 步

此时，安装程序将检查所选安装软件包的依赖关系（在我们案例中，没有选择任何软件包），并格式您在系统中选择要格式化的每一个分区。这取决于您机器的速度，可能需要几分钟。一旦所有分区格式化完成，安装程序将开始向您的硬盘安装 Linux。

![](img/62d23c0d98be09825cf9e4c822190362_45_1.png)

## 创建启动盘

在安装的这一部分，我们有机会为新安装的操作系统创建一个创建一个启动盘。如果您不想创建启动盘，应该在点击“下一步”之前勾选“跳过启动盘创建”复选框。如果您决定不在 MBR（主引导记录）上安装 `GRUB` 或 `LILO`，或者根本不安装 `GRUB` 或 `LILO`，则必须创建启动盘。

![](img/62d23c0d98be09825cf9e4c822190362_46_0.png)

## 如何使用 RPM 命令

本节介绍了使用 `RPM` 在 Linux 系统上安装、卸载、升级、查询、列出和检查 `RPM` 软件包。您现在必须熟悉这些 `RPM` 命令，因为我们将在本文中经常使用它们，特别在本章的后期，对于安装服务器后必须卸载的软件。

### 安装 RPM 软件包：

请注意，`RPM` 软件包具有类似于 `foo-1.0-2.i386.rpm` 的文件名，其中包含了包名 (`foo`)、版本 (`1.0`)、发行版本 (`2`) 和架构 (`i386`)。

- 要安装 `RPM` 软件包，使用命令：
