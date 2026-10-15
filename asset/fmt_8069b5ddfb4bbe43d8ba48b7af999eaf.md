
每个分区的名称（IDE 分区的 `sda1`, `hda2` 等，SCSI 分区的 `sda1`, `sda2` 等，包括 USB 闪存器）显示在代表每个分区的磁盘图标上。将鼠标指针悬停在图标上可以查看有关分区的挂载点和设备名称的信息。有了这些信息，你可以按照以下步骤将任何一个分区变为可写：

- 1. 在 KNOPPIX 桌面上右键点击代表你想写入的硬盘分区的图标。将打开一个菜单，显示该分区可用的功能。
- 2. 选择 `Change read/write mode`（更改读/写模式）选项。系统会询问你是否真的想让该分区可写。选择 `Yes`（是）。
- 此时，你可以打开指向分区 (`hda2`) 的文件夹，或者打开 shell 并写入目录 (`/mnt/hda2` 以及任何子目录)。要使其永久化，你需要更改 `/etc/fstab`，在默认以读/写挂载的分区条目中添加 `rw`。再次以 `/dev/hda2` 为例，`etc/fstab` 中挂载分区为读/写的条目可能如下：

```
/dev/hda2 /mnt/hda2 ext3 noauto,users,rw 0 0
```

进行该更改后，只需输入 `sudo mount /dev/hda2` 即可以读写权限挂载该目录。只要分区被正确检测，Windows 分区与 Linux 分区不同。对于 Windows 文件系统 FAT 和 VFAT，挂载并向其写入应该没有问题。对于 NTFS 文件系统，在向其写入之前有几点需要考虑。较早版本的 KNOPPIX 允许你下载一个名为 Captive NTFS 的功能。通过 Captive NTFS，你可以使用原生 Windows 访问 NTFS 分区而无需担心损坏。当前版本的 KNOPPIX 使用来自 Linux-NTFS 项目 (`www.linux-ntfs.org/`) 的驱动程序，提供了对访问 NTFS 分区的支持。使用 Linux-NTFS 的优势是 NTFS 分区可以像任何其他文件系统一样挂载和使用。换句话说，不需要 Windows 驱动程序。缺点是 Linux-NTFS 被认为不可靠，可能会导致你的 NTFS 分区损坏。因此，我建议如果 NTFS 文件系统包含关键数据，则不要向其写入，但在你的 KNOPPIX 会话期间可以随时从 NTFS 读取。

# 创建持久性目录

如果你打算多次使用带有 KNOPPIX 的电脑（或者你只是想为你的文件提供 RAM 中其他可用的存储空间），你可以将你的 KNOPPIX 主目录 (`/home/knoppix`) 分配到硬盘上的可用空间。这可以通过两种方式之一完成：

- 将整个分区分配给你的主目录。
- 以镜像的形式分配分区的一部分。你也可以将你的主目录持久化到可移动的介质上，例如内存棒。一旦你创建了该区域作为你的主目录，你就可以告诉 KNOPPIX 每次重启时都使用它。以下是操作步骤：
- 1. 点击面板上的小企鹅，然后选择 `Configure Create a Persistent disk image`（配置 创建持久性磁盘镜像）。会出现一个窗口，询问你是否准备好创建一个持久性主目录。
- 2. 点击 `Yes` 继续。
- 3. 询问你想使用哪个分区作为你的持久性主目录。
- 4. 选择你想存储用于持久性桌面的分区并点击 `OK`。系统会询问你是否要以加密格式保存主目录。
- 5. 选择 `No` 以使目录不加密（如果你选择 `Yes`，目录将会被加密）。
- 6. 输入分配给主目录的兆字节数并点击 `OK`。确保空间可用）。分区或镜像文件应该会被创建。

当我为 `hda5` 上创建一个 100MB 镜像时，它创建了文件 `/mnt/hda5/knoppix.img`，空间为97MB。要了解如何使用该目录，请参见本章后续的“重启 KNOPPIX”。

# 保存 KNOPPIX 配置

当你花费精力配置 KNOPPIX 的桌面、打印机、网络和其他偏好后，如果下次重启时丢失所有内容，就太可惜了。KNOPPIX 提供了一种方法，让你可以保存配置并在下次会话中恢复它。保存的信息可以存储在软盘或重启 KNOPPIX 时可以访问的任何介质（如你的硬盘）上。步骤如下：

- 1. 从面板上的图标处点击 `Configuration Save KNOPPIX configuration`（配置 保存 KNOPPIX 配置）。
- 2. 选择要保存的配置文件。你可以选择个人配置 (`/home/knoppix/.kde` 和 `.mozilla` 目录）、桌面文件、网络配置、`X` 配置以及来自 `/etc` 的其他系统文件。
- 3. 选择将配置文件保存到软盘或任何可写的分区。选择软盘使配置具有便携性，而使用硬盘可以让配置在同一台机器上重复使用。
- 4. 如果保存到软盘，插入软盘并点击 `OK`。数据已保存到软盘。此操作的结果是在软盘上创建了 `knoppix.sh` 和 `configs.tbz` 文件。`configs.tbz` 文件包含了来自 `/home` 和 `/etc` 目录的所有保存配置。`knoppix.sh` 是一个告诉 KNOPPIX 在启动时如何安装这些文件的脚本。下次启动 KNOPPIX 时，可以使用这些配置文件，如下一节所示。

> 那些创建了自定义 KNOPPIX 启动盘的人只需将他们的 `knoppix.sh` 和 `config.tbz` 文件添加到 CD 的根目录，这样 KNOPPIX 就能直接启动他们的个性化配置，而无需担心额外的软盘或其他介质。

## 重启 KNOPPIX

你可以随时插入 KNOPPIX CD 或 DVD 并重启电脑来启动 KNOPPIX。如果你想利用你设置的持久性桌面或保存的配置信息，你需要在 KNOPPIX 启动提示符中添加一些选项。

具体如下：

- 将 KNOPPIX CD 或 DVD 插入电脑并重启。你应该能看到 KNOPPIX 启动提示符。
- 在 KNOPPIX 启动之前按下 `F3` 键，查看是否需要额外的启动选项。
- 如果你有软盘启动盘（或其他在早先过程中创建的其他可移动介质），请现在插入该磁盘。
- 在启动提示符处，输入以下命令行之一，这些是加载配置文件的不同方式：

```
boot: knoppix floppyconfig
boot: knoppix myconfig=/dev/hda
boot: knoppix myconfig=/dev/sda
boot: knoppix myconfig=scan
```

这些 KNOPPIX 命令分别从软盘获取配置信息、在第一个 IDE 驱动器分区 (`/dev/hda`) 上查找信息、在第一个 SCSI 分区 (`/dev/sda`) 上查找信息，或扫描所有可用驱动器以找到信息。要启动到持久性桌面（假设你之前已设置过），你可以输入：

```
boot: knoppix home=/dev/hda1/knoppix.img
boot: knoppix home=/dev/sda1/knoppix.img
boot: knoppix home=scan
```

上述命令分别将 KNOPPIX 目录 (`/home/knoppix`) 分配给 `/dev/hda1/knoppix.img` 文件、`/dev/sda1/knoppix.img` 文件，或通过扫描所有可用目录找到该镜像文件。你也可以结合上述两个命令中的每一项来读取你的配置文件并分配持久性桌面，如下：

```
boot: knoppix floppyconfig home=/dev/hda1/knoppix.img
```

现在你已经准备好从上次离开的地方继续 KNOPPIX 会话了，并且可以使用相同的配置和数据文件。

## 总结

KNOPPIX 提供了许多功能，使其成为当今最好的启动 Linux 发行版。它让你在几乎任何可以找到可启动 PC 的地方都能获得一个完全配置好的 Linux 桌面系统。

除了桌面功能外，KNOPPIX 还包含了使用 Linux 的任何服务器、编程和故障排除功能所需的软件。尽管 KNOPPIX 作为 RAM 中的可启动系统运行，但默认情况下，有方法配置它以跨多次启动会话保存数据和配置信息。

KNOPPIX 每次启动时都能进入一致的状态，这是使用 KNOPPIX 的另一个优势。如果你认为你保存的自定义设置已损坏，你可以随时不带这些设置重启 KNOPPIX，以重新开始一个干净的 KNOPPIX 系统。

KNOPPIX 作为访问损坏计算机以进行故障排除的工具特别有价值。在安装了 Microsoft Windows或其他操作系统的电脑上启动 KNOPPIX 磁盘，你可以使用 KNOPPIX 访问并处理该计算机硬盘上的数据。

## 第 12 章

## 运行 Yellow Dog Linux

Yellow Dog Linux 是 PowerPC (`PPC`) 平台领先的 Linux 发行版之一。由 Terra Soft Solutions (`www.terrasoftolutions.com`) 提供，Yellow Dog Linux 为 PowerPC 用户的需求提供了无与伦比的连接。
