
在内核配置期间，也可以为某些文件系统指定默认 codepage 和 charset 值。相关参数命名为 "Default NLS Option" (`CONFIG_NLS_DEFAULT`)、`"Default Remote NLS Option"` (`CONFIG_SMB_NLS_DEFAULT`)、`"Default codepage for FAT"` (`CONFIG_FAT_DEFAULT_CODEPAGE`) 以及 "Default charset for FAT" (`CONFIG_FAT_DEFAULT_CHARSET`)。在内核编译时，无法为 nfs 文件系统指定这些设置。

对于某些硬盘类型，可以使 ext3 文件系统在断电时保持可靠。要做到这一点，向 `/etc/fstab` 中相应的条目添加 `barrier=1` 挂载选项。要检查磁盘驱动器是否支持此选项，请在相应的磁盘驱动器上运行 `hdparm`。例如：

```
hdparm -I /dev/sda  | grep NCQ
```

如果返回非空输出，则支持该选项。

注意：基于逻辑卷管理 (`LVM`) 的分区无法使用 `barrier` 选项。

## 8.3. Linux-5.2.8

Linux 软件包包含 Linux 内核。

预计构建时间：4.4 - 66.0 SBU（通常约为 6 SBU）

所需的磁盘空间：960 - 4250 MB（通常约为 1100 MB）

### 8.3.1. 内核的安装

构建内核涉及几个步骤——配置、编译和安装。请阅读 `README` 以获取更多信息。

运行以下命令准备内核：

```
makeproper
```

通过菜单驱动的界面配置内核。有关内核的通用信息，请参阅 `linux-5.2.8/Documentation` 目录下的文档。此外，`modprobe.d(5)` 可能对你感兴趣。

编译内核镜像和模块：

```
make
```

如果内核配置使用了模块，则安装模块：

```
make modules_install
```

内核编译完成后，还需要额外的步骤来完成安装。某些文件需要复制到 `/boot` 目录。

#### 注意事项

如果系统具有独立的 `/boot` 分区，则下方复制的文件应该存放在那里。最简单的方法是在继续之前，在主机上（chord 之外）将 `/boot` 绑定挂载到 `/mnt/lfs/boot`。主机系统中的 root 用户执行：

```
mount --bind /boot /mnt/lfs/boot
```

内核镜像的路径可能根据所使用的分区而异。下面的文件名可以根据喜好进行更改，但内核文件的主文件名应为 `vmlinuz`，并按照下一节描述的启动过程进行自动设置。以下命令假设为 x86 架构：

```
cp -iv arch/x86/boot/bzImage /boot/vmlinuz-5.2.8-lfs-9.0
```

`System.map` 是内核的符号文件。它映射了内核 API 中每个函数的入口点，以及运行中内核的内核数据结构的地址。在调查内核问题时，它是一个重要的资源。执行以下命令安装映射文件：

```
cp -iv System.map /boot/System.map-5.2.8
```

由上述 `make menuconfig` 步骤产生的配置文件 `.config` 包含了刚刚编译的内核的所有配置选项。保留此文件以备后用是一个好主意：

```
cp -iv .config /boot/config-5.2.8
```

安装 Linux 内核文档：

```
install -d /usr/share/doc/linux-5.2.8
cp -r Documentation/* /usr/share/doc/linux-5.2.8
```

需要注意的是，内核源码目录中的文件并不属于 root。每当以 root 用户身份解压包时（我们在 root 内部执行了操作），文件的用户 ID 和组 ID 将是它们在打包者计算机上的用户和组 ID。对于任何其他包的安装，除非在安装后删除源码树，否则这不是一个问题。然而，Linux 源码树通常会保留很长时间。由于，软件包使用的任何用户 ID 可能会被分配给机器上的某个人。那个人将拥有内核源码。

#### 警告

系统 `include` 目录（`/usr/include`）中的头文件*应该始终*是编译 Glibc 时使用的那些文件，即第 6.7 节中清理过的“Linux-5.2.8 API 头文件”。因此，它们*绝不能*被内核头文件或任何其他内核清理头文件替换。

### 8.3.2. 配置 Linux 模块加载顺序

大多数情况下 Linux 模块会自动加载，但有时需要特定的指导。加载模块的程序 `modprobe` 或 `insmod` 使用 `/etc/modprobe.d/usb.conf` 实现此目的。需要创建此文件以便 USB 驱动程序按顺序加载；`ehci_hcd`、`ohci_hcd` 和 `uhci_hcd` 已编译为模块，将按正确顺序加载；`ehci_hcd` 需要在 `ohci_hcd` 和 `uhci_hcd` 之前加载，以避免启动时出现警告。

运行以下命令创建一个新文件 `/etc/modprobe.d/usb.conf`：

```
install -v -m755 -d /etc/modprobe.d
cat > /etc/modprobe.d/usb.conf << "EOF"
# Begin /etc/modprobe.d/usb.conf

install ohci_hcd /sbin/modprobe ehci_hcd; /sbin/modprobe ohci_hcd; true
install uhci_hcd /sbin/modprobe ehci_hcd; /sbin/modprobe -i uhci_hcd; true

# End /etc/modprobe.d/usb.conf
EOF
```

### 8.3.3. Linux 的内容

- 安装文件：`config-5.2.8`, `vmlinux-5.2.8-lfs-9.0` 和 `System.map-5.2.8`
- 安装目录：`/lib/modules`, `/usr/share/doc/linux-5.2.8`

#### 概要说明

- `config-5.2.8`：包含内核的所有配置选项
- `vmlinux-5.2.8-lfs-9.0`：Linux 系统的引擎。当电脑启动时，内核是操作系统被加载的第一部分。它检测并初始化计算机硬件的所有组件，然后将这些组件作为文件树提供给软件使用，并运行一个可以同时运行程序的单个 CPU
- `System.map`：地址和符号的列表；它映射了内核中所有函数和数据结构的入口点和地址

## 8.4. 设置启动过程

### 8.4.1. 介绍

错误地使用 GRUB 会导致你的系统在没有 CD-ROM 等备用启动设备的情况下无法运行。本节对于启动你的 LFS 系统并不是必须的。你可能只是想修改当前的启动加载程序，例如 Grub-Legacy、GRUB2 或 LILO。

确保准备好了一个紧急启动盘，以便在计算机无法启动时进行“救援”。如果你没有启动设备，可以创建一个。为了让下面的步骤生效，你需要跳转到 LFS 并从包中安装 `xorriso`。

```
cd /tmp
grub-mkrescue --output=grub-img.iso
xorriso -as cdrecord -v dev=/dev/cdrom blank=as grub-img.iso
```

对于启用了 UEFI 的 LFS 系统，内核需要使用上一节描述的 `CONFIG_EFI_STUB` 能力进行构建。然而，LFS 可以在没有它的情况下使用 GRUB 启动。有了此功能，需要找到系统 BIOS 中的 UEFI 模式和安全启动功能。详情请参阅位于 http://www.linuxfromscratch.org/downloads/lfs-uefi.txt 的 `lfs-uefi.txt`

### 8.4.2. GRUB 命名规范

GRUB 使用自己的命名结构来表示设备和分区，格式为 `(hdn,m)`，其中 n 是硬盘编号，m 是分区号。硬盘从零开始，但普通分区号从一开始，扩展分区从五开始。这与早期从零开始数字的版本不同。例如，分区 `sda1` 是 `(hd0,1)`，`sdb2` 是 `(hd1,2)`。相比之下，GRUB 不认为 CD-ROM 驱动器是硬盘。例如，如果在 hdb 上使用 CD，则为 `(hd1)`。

### 8.4.3. 设置配置

GRUB 通过写入主引导记录来工作，这影响磁盘。GRUB 默认会写入 `/boot/`。一个建议是使用较小的分区（建议大小为 100 MB）作为 boot。

使用上述信息确定分区的标识符（或 boot 分区）。对于示例，假设根分区（或 boot 分区）是 `sda2`。

将 GRUB 文件写入 `/boot/grub` 并设置启动：

#### 警告

以下命令将覆盖当前的引导加载程序。如果不希望这样做（例如你使用第三方引导管理器来管理），请不要运行该命令。

```
grub-install /dev/sda
```

### 注意
