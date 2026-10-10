
现在我们将编辑第一个 `grub.conf`。对于我们在本指南中使用的分区示例，你会发现两个 `grub.conf`。我们只对第一个 `grub.conf` 进行了详尽的注释。请确保使用你的内核文件名缩进，并在适当的情况下，使用你的 `initrd` 镜像文件名。

- 第一个 `grub.conf` 是给那些没有使用 `genkernel` 构建内核的人使用的
- 第二个 `grub.conf` 是给那些使用过 `genkernel` 构建内核的人使用的

> 注意：如果你的文件系统是 `JFS`，则你必须在内核行中添加 `"ro"`，因为 `JFS` 在允许读写挂载之前需要重放其日志（`log`）。

### 代码列表 3. 适用于非 genkernel 用户的 grub.conf

```bash
# 默认启动哪项列表。0 是第一个，1 是第二个，依此类推。

default 0

# 在启动默认列表之前等待多少秒。

timeout 30

# 用于美观的平整启动图像：

# 如果你没有安装显卡，请注释掉它

splashimage=(hd0,0)/boot/splash.xpm

title=center Linux 2.6.12-r10

# 内核镜像（或操作系统）所在的分区

root=(hd0,0)

kernel /kernel-2.6.12-genkernel-r10 root=/dev/hda3

# 仅当你与 Windows 系统进行双启动时需要以下行。

# 在这种情况下，windows 位于 /dev/hdat

title=Windows XP

rootverify=(hd0,5)

makeactive

chaloader +1
```

### 代码列表 4. 适用于 genkernel 用户的 grub.conf

```bash
default 0

timeout 30

splashimage=(hd0,0)/boot/splash.xpm

title=center Linux 2.6.12-r10

kernel /kernel-x86-2.6.12-genkernel-r10 root=/dev/ram0 init=/inituxrd mask=8192 real_root=/dev/hda3

initrd /initramfs-genkernel-x86-2.6.12-genkernel-r10

# 仅在你想进行双启动时

title=Windows XP

rootverify=(hd0,5)

makeactive

chaloader +1
```

> 注意：内核行中提到的 `udev` 是为了在用 `udev` 代替它（这是默认设置）时，绕过某些 `genkernel` 版本中的一个 `bug` 而需要的。

如果你使用了不同的分区方案并相应地更改了内核镜像，请确保所有 `GRUB` 设备（如 `(hd0,0)`）都是相对于挂载点而非根目录。换句话说，`hd0,0)/grub/splash.gz` 位于 `/boot/grub/splash.gz`。如果你选择了...（此处原文后续存在重复及乱码，已根据逻辑翻译并处理）

当然，它也被一些了解 `LILO` 并想要坚持使用它的人使用。无论哪种，`Gentoo` 都支持两者，而且重要的是你选择了使用 `LILO`。

安装 `LILO` 易而举举；只需使用 `emerge` 即可

### 代码列表 9: 安装 LILO

```bash
# emerge lilo
```

## 配置

要配置 `LILO`，你必须创建 `/etc/lilo.conf`。启动你最喜欢的编辑器（在本手册中，为了保持一致，我们使用 `nano`）并创建该文件。

### 代码列表 10: 创建/etc/lilo.conf

```bash
# nano -w /etc/lilo.conf
```

我们要求你记住的一些事情是你创建的内核名称。在接下来的示例 `lilo.conf` 中，我们使用了示例分区方案。它有两个独立的部分：

- 适用于没有使用内核来构建内核的用户
- 适用于使用了内核来构建内核的用户

请确保在每个启动项之后使用你的内核文件名，并在适当的情况下加上你的 `initrd` 行。`JFS` 在允许读写之前需要重放其日志。

> 注意：如果你的根文件系统是 `JFS`，你必须在每个启动项之后添加 `append='ro'` 行，因为 `JFS` 在允许读写之前需要重放其日志。

### 代码列表 11: 示例/etc/lilo

```bash
boot=/dev/hda      # 将 LILO 安装在 MBR 中

prompt            # 给用户选择另一个部分的机会

timeout=50         # 在启动默认部分之前等待 5（五）秒

default=gentoo     # 当超时通过后，启动 "gentoo" 部分

# 对于非通用内核用户

image=/boot/kernel-generic-2.6.12-gentoo-r10

label=gentoo      # 给此部分的内核命名的

read-only=ro      # 以只读根启动。不要修改！

root=/dev/hda3    # 根文件系统的位置

# 对于内核用户

image=/boot/kernel-generic-x86-2.6.12-gentoo-r10

label=gentoo

read-only=n

append="initrd=/linuxux_ramdisk=8192 root=/dev/hda3 udev"

initrd=/boot/initramfs-kernel-generic-2.6.12-gentoo-r10

# 这两行仅适用于你与 Windows 系统双启动的情况。

# 在这种情况下，Windows 托管在 /dev/hda6。

other=/dev/hda6

label=windows
```

> 注意：`append` 行中提到的 `udev` 是为了在最初就使用 `udev`（这是默认行为）时，在某些内核版本中的解决方案解决方案。

如果你需要向内核传递任何额外选项，请在该部分添加 `append` 语句。例如，我们添加了 `video` 语句来启用帧缓冲：

### 代码列表 12: 使用 append 添加内核选项

```bash
image==/kernel-2.6.12-gentoo-r10

label=gentoo

read-only=ro

root=/dev/hda3

append=video:vesafb:mtrr,ywrap,1024x768-32885*
```

如果你正在使用 `2.6.7` 内核，并且因为 `BIOS` 无法处理大硬盘导致你的硬盘卡死，你需要追加 `dx=store`。

`genkernel` 用户应该知道他们的内核使用与安装 `CD` 相同的启动选项。例如，如果你有 `SCSI` 设备，你将 `doskel` 作为内核。

现在保存并退出。要完成操作，你必须运行 `/sbin/lilo`，以便 `LILO` 将 `/etc/lilo.conf` 复制到你的系统（即从磁盘安装）。
请记住，每次安装新内核或对菜单进行任何更改时，都必须运行 `/sbin/lilo`。

### 代码列表 13: 完成 LILO 安装

> 注意：当你重新安装内核时，你不再需要复制文件了。只需在编译内核后运行 `make install` 即可；它会自动复制必要的文件并调整 `LILO` 配置。

你现在可以继续重启系统

## 10. 重启系统

退出环境并卸载所有已挂载分区。然后输入你一直等待的魔法命令：`reboot`。

### 代码列表 14: 卸载所有分区并重启

```bash
# exit

cd /

umount -f /mnt/gentoo/boot /mnt/gentoo/dev /mnt/gentoo/proc /mnt/gentoo

reboot -f
```
