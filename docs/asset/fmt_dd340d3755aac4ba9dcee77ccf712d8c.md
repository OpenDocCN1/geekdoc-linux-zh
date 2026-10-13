
```
install=/boot/boot.b

prompt

timeout=50

image=/vmlinux

label=linux

root=/dev/sdal

initrd=/initrd

read-only

image=/boot/vmlinuz-2.2.5-15smp

label=linuxold

root=/dev/sdal

initrd=/boot/initrd-2.2.5-15smp.img

read-only

image=/boot/vmlinuz-2.2.5-15

label=linux-up

root=/dev/sdal

image=/boot/initrd-2.2.5-15.img

read-only
```

如果你不想费自己编译内核的麻烦，可以使用 Red Hat 发布的补丁内核。在本文发布时，Red Hat 希望你使用的最新内核版本是 2.2.5 build 22。该版本取代了 2.2.5 build 15，后者有一个会导致崩溃的错误。

在之前的 Linux 发行版中，Red Hat 只包含为 80386 编译的内核。从 Red Hat Linux 6.0 开始，Red Hat 现在包含了适用于不同类型的内核。以下是补丁包：

- `kernel-2.2.5-22.i386.rpm`：适用于 i386、i486 等非 Pentium 系统
- `kernel-2.2.5-22.i586.rpm`：适用于大多数 Pentium 类 CPU
- `kernel-smp-2.2.5-22.i586.rpm`：适用于 Pentium SMP
- `kernel-2.2.5-22.i686.rpm`：适用于 i686 (Pentium II, Celeron)
- `kernel-smp-2.2.5-22.i686.rpm`：适用于 i686 SMP

Red Hat 提供了许多升级内核的步骤，但并不困难。在本练习中，假设要升级 Pentium 系统。输入以下命令：

```
/sbin/modprobe loop.o

rpm -iv kernel-2.2.5-22.i586.rpm

/sbin/mkinitrd /boot/initrd-2.2.5-22.img 2.25
```

如果你足够勇敢（或者很疯狂），可以使用 RPM 的 "Uvh" 选项。它会破坏当前的内核，并在重新配置 LILO 之前防止系统启动：

```
/sbin/modprobe loop.o

rpm -Uvh kernel-2.2.5-22.i586.rpm

/sbin/mkinitrd /boot/initrd-2.2.5-22.img 2.25
```

对于 IDE 用户来说，“Uvh”选项可能比 SCSI 用户更现实。如果由于某些原因回环设备可用，`mkinitrd` 将失败。

在哪种情况下，尝试这些命令集时，请确保你有启动盘。丢失了启动盘？可以在升级*之前*使用以下命令创建一个：

```
mkbootdisk --device /dev/fd0 2.2-5-15
```

如果我必须告诉你 `/dev/fd0` 是你电脑上的 A: 盘，那你可能还没有准备好进行内核升级。还要提醒你，如果你在 RPM 内核升级命令中使用 "Uvh" 选项，启动盘将没有 `loop.o` 模块（如果系统崩溃的话）。你可以从旧的 RPM 中获取它，不要使用 "Uvh" 选项，除非你*确定*第一次就能搞定。在开始之前，你可能会备份旧内核。（它位于 `/lib/modules` 目录。）

## 使用补丁内核

上面的 `mkinitrd` 命令在 IDE 系统上并不重要，但在 SCSI 系统上至关重要。没有 initrd 中的内核模块，系统将无法启动。

一旦安装了新内核，系统处于危险状态。在内核升级和 LILO 重新配置之间进行重启可能会从不便变成灾难。IDE 系统的升级通常只需要更改 `/etc/lilo.conf` 中的内核镜像名称，如列表 10.2 所示。

### 列表 10.2 为补丁内核修改 `/etc/lilo.conf`

```
boot=/dev/hda

map=/boot/map

install=/boot/boot.b

prompt

timeout=50

image=/boot/vmlinuz-2.2.5-22

label=linux

root=/dev/hda5

read-only

other=/dev/hda1

label=dos

table=/dev/hda
```

或者，如果未使用 "Uvh" 选项，可以将旧内核设置为备份：

```
boot=/dev/hda

map=/boot/map

install=/boot/boot.b

prompt

timeout=50

image=/boot/vmlinuz-2.2.5-22

label=linux

root=/dev/hda5

read-only

image=/boot/vmlinuz-2.2.5-15

label=linuxold

root=/dev/hda5

read-only

other=/dev/hda1

label=dos

table=/dev/hda
```

这种备用配置允许在输入 `linux` 时让 LILO 启动新内核，在输入 `linuxold` 时启动旧内核。SCSI 系统要复杂一点，因为还必须设置 `initrd`：

```
boot=/dev/sda

map=/boot/map

install=/boot/boot.b

prompt

timeout=50

image=/boot/vmlinux-2.2.5-22

label=linux

root=/dev/sdal

initrd=/boot/initrd-2.2.5-22.img

read-only

image=/boot/vmlinux-2.2.5-15

label=linuxold

root=/dev/sdal

initrd=/boot/initrd-2.2.5-15.img

read-only
```
