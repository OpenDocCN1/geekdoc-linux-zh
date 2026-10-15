
`zlilo` 也会安装内核文件，但会运行 `lilo` 来更新 LILO。`zlilo` 选项专为运行 LILO 的系统设计。如果你使用 `loadlin` 从 DOS 启动 Linux，你需要将 `bzImage` 文件复制到启动 Linux 的 DOS 分区的 loadlin 目录。

要手动安装内核 bImage 文件，请将 bImage 文件复制到内核所在的目录，并将其命名为发行版使用的名称，例如 Red Hat 的 `vmlinuz`。记得备份旧的内核文件。在 Red Hat 上，`vmlinuz` 是指向实际内核文件的符号链接，该文件将带有版本名称的 `mlinuz`。因此，为了在 Red Hat 上手动安装 bImage，请将其复制到 `/boot` 目录，并命名为 `vmlinuz` 以及附加版本号，如 `vmlinuz-2.4.7-10`。然后你从 `/boot/mlinuz` 到 `/boot/vmlinuz-2.4.7-10` 创建符号链接。

```bash
make bImage

cp /arch386/boot/bImage /boot/vmlinuz-2.4.7-10

ln -s /vmlinuz /boot/vmlinuz-2.4.7-10
```

bImage 选项以及那些以 b 字母开头的选项（如 `bzlilo`）会创建一个压缩的内核镜像。这在旧系统上可能不起作用。如果不起作用，请尝试使用 `zimage` 选项来创建一个名为 `zImage` 的内核文件。然后手动安装 zimage 文件。请记住 zimage 最终会被淘汰。

```bash
make zImage
```

`bzlilo` 选项既会将内核文件安装到你的系统中，又会运行 LILO。如果你收到内核内核太大的错误，应该使用此选项。以下命令会编译内核、将其安装到你的系统中并为你运行 LILO。要安装和更新 LILO，请使用以下命令：

```bash
make bzlilo
```

如果你收到内核内核太大的错误，尝试使用 b 版本的选项（如 `bzlilo`）来减小其体积。

```bash
make bzdisk
```

```text
initrd/boot/initrd-2.4.12.img

title Red Hat Linux (2.4.7-10)

root (hd0,2)

kernel /boot/vmlinuz-2.4.7-10 ro=/dev/hda3 hdc=ide-scsi

initrd/boot/initrd-2.4.7-10.img

title Windows XP

root (hd0,0)

imeaveactive

chainloader +1
```

## 模块内存磁盘 (Module RAM Disks)

如果你的系统在启动时需要加载模块，你可能需要为它们创建一个 RAM 盘。例如，如果你有 SCSI 驱动器或 CD-ROM，对于它们的 SCSI 驱动程序通常包含在系统启动时加载的模块中。这些模块存储在 RAM 盘中，启动过程会读取它。如果你创建了一个需要在启动时加载模块的新内核，你必须为由于这些模块创建一个新的 RAM 盘。当你创建新内核时，还需要包含模块。你需要将启动所需的模块（如 SCSI 硬盘模块）放在一个新的 RAM 盘中。在 `lilo.conf` 文件为此 RAM 盘添加一个条目。只有当你的内核需要在启动时加载模块时，才需要创建一个新的 RAM 盘。例如，如果你有一个 SCSI 驱动器，但你已将 SCSI 硬盘和 CD-ROM 支持（包括对特定模块的支持）直接整合到内核中，则不需要设置 RAM 盘。IDE 硬盘和 CD-ROM 已经直接整合到内核中。

如果你需要创建 RAM 盘，可以使用 `mkinitrd` 命令创建一个 RAM 盘文件或创建一个 RAM 盘设备。更多详情请参见 `mkinitrd` 的 Man 手页和 RAM 磁盘文档。`mkinitrd` 的参数是磁盘镜像的以及模块的来源。在下面的示例中，将在 `/boot` 目录下创建一个名为 `initrd-2.4.7-10.img` 的 RAM 盘，使用来自 2.4.7-10 内核的模块。你的系统上需要安装 2.4.7-10 内核及其模块。

```bash
# mkinitrd /boot/initrd-2.4.7-10.img 2.4.7-10
```

在新内核的 `lilo.conf` 段中，你会放置一个指定新 RAM 盘的 `initrd` 条目。

```text
image=/boot/vmlinuz-2.4.7-10

label=/dev/hda3

initrd=/boot/initrd-2.4.7-10.img

read-only
```
