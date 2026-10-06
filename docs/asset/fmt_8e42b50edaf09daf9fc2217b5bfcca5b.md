
```
### cd ~/livecd/source
### mkdir usr/portage/distfiles
### mount -o bind /usr/portage/distfiles usr/portage/distfiles
### mkdir -p proc
### mount -o bind /proc proc
### mkdir -p sys
### mount -o bind /sys sys
### mkdir -p dev
### mount -o bind /dev dev
### cp /etc/resolv.conf etc/resolv.conf
```

现在构建目录已就绪，你可以 `chroot` 到该目录并开始安装软件包并配置你的 live CD 了。

# 在 CHROOT 环境中工作

`/root/livecd/source` 目录下的所有内容都代表了构成 Gentoo live CD 的文件。使用 `chroot` 命令，你可以让该目录成为你工作时的根目录。这样，每当你安装软件包或修改配置文件时，这些信息将进入你的 live CD，而不是被应用到你的 Gentoo 系统上。

## 更改根目录

输入以下内容更改你的根目录并使用 `bash` shell 打开一个登录 shell。

> 注意，如果你正在一个带有多个终端窗口的 Gentoo 桌面中工作，请确保将打算用于 `chroot` 环境的命令在运行 `chroot` 命令的那个终端窗口中运行。为了确保我使用了正确的终端，请：

```
chroot /root/livecd/source /bin/bash
```

## 设置环境变量

在 `chroot` 运行之前，你可能需要设置一些环境变量。例如，设置路径：

```bash
export PATH=/usr/sbin:/usr/bin:/sbin:/bin
```

## 编译 Gentoo

在 `chroot` 环境中，你可以开始编译 Gentoo。首先是内核：

```bash
cd /usr/src/linux
make menuconfig
make && make modules_install
cp arch/x86/boot
```

## 安装软件包

内核编译完成后，安装基础系统：

```bash
emerge --ask --askdeps @world
```

## 制作 Live CD

系统安装完成后，制作 live CD 镜像：

```bash
cd /root/livecd/source
squashfs -m rootfs rootfs.squashfs
genisofs livecd.iso ...
```

### 注意

你可以使用 `minimal` 标志来运行最小化构建，这会禁用许多非本质功能。如果你添加了 `minimal` USE 标志，你需要为 `perl` 包添加一个豁免。在切换到 `chroot` 环境之前，请输入以下命令：

```bash
# echo "dev-lang/perl -minimal" >> /livecd/source/etc/portage/package.use
```

- `# emerge -e system`
- `# emerge -e world`

### passwd root

New UNIX Password: ********

Retype UNIX password: ********

`system` 软件包类包含系统正常运行所需的软件包。`world` 软件包类包含系统软件包以及 `/var/lib/portage/world` 中的软件包。

如果在在此过程中升级了 C 编译器（`gcc` 包），你需要指示系统使用新的 C 编译器，然后再次运行 `emerge` 来更新整个系统。关于升级 GCC 的说明请参阅 [GCC 升级指南](www.gentoo.org/doc/en/gcc-upgrading.xml)。

## 修改 /etc 配置文件

你应当手动修改配置文件中的某些功能。请注意，此时 `nano` 可能是唯一的文本编辑器。在调用文本编辑器时，你可以选择安装并使用 `vim` 或 `emacs`。

首先，设置时区。根据你所在地的信息替换 `area/city`。例如，将时区设置为 America/Chicago，请输入以下命令：

```bash
# ln -sf /usr/share/zoneinfo/America/Chicago /etc/localtime
```

另一个建议的配置文件更改是启用 `dmraid`。输入以下命令：

```bash
# echo "sys-fs/dmraid -x86" >> /etc/portage/package.keywords
```

使用任何文本编辑器编辑 `/etc/fstab` 文件，使其仅包含以下信息（在文件末尾添加空行）：

```
# 第 8 章 构建基础 Gentoo CD

/dev/root      squashfs ro,defaults 0 0
none            /proc proc defaults 0 0
none            /dev/shm tmpfs defaults 0 0
none            /dev/pts devpts defaults 0 0
```

关于 `/etc` 目录下其他配置文件的更改将在稍后描述。

你可以通过运行系统管理工具进行许多更改，特别是在你启用 X 应用从 `chroot` 环境运行之后。

例如，重置时区的另一种方法是运行 `time-admin` 工具并从列表中选择时区。

## 添加所需的软件包

为了让你的 `chroot` 环境变成一个可以作为 live CD 使用的镜像，需要一些额外的软件包。以下 `emerge` 命令添加了这些软件包：

```bash
# emerge memtest86+ localpurge kernelgen sys-fs/fuse
# emerge logger coldpig mingetty slocate
# rc-update add addflag default
```

`rc-update` 基本上是开启这些服务并使用每个服务的默认设置。大多数你可以开启的服务都列在 `/etc/init.d` 目录下。

## 添加可选软件包

这是你在 live CD 上添加软件包的地方。在大多数情况下，除了基础系统组件外，你需要选择你希望在 live CD 上的每个组件。你可以通过搜索 `/usr/portage` 目录查找感兴趣软件包来实现。`kde` 和 `gnome` 选项是例外，它们会导致安装大量与这些桌面环境相关的软件包。

第 9 章“定制安全 Live Linux CD”到第 14 章“集群化 Live Linux CD”描述了你可能感兴趣的开源软件。大部分软件你都可以使用 `emerge` 命令在 Gentoo 中安装。

## 创建内核和模块

要创建在 live CD 上使用的内核，请获取 `gentoo-sources` 包。然后你 own按照以下方式制作模块并配置内核：

```bash
# emerge gentoo-sources
# cd /usr/src/linux
# make allmodconfig
# genkernel -menucleconfig -no-clean all
```

在 `genkernel` 步骤中，你可以选择更改哪些内核组件包含或不包含在内核中，以及哪些作为驱动程序或可加载模块包含。请确保编译了以下组件：

- 文件系统——包括 SquashFS、CD-ROM/DVD 文件系统 → ISO 9660 CD-ROM 以及 ext2 文件系统支持。为了将 live CD 作为救援 CD 使用，你可能还需要其他文件系统类型，例如 Reifers、JFS、XFS 和虚拟内存文件系统支持。
- 设备驱动程序——包括回环设备、RAM disk（默认数量为 16，默认大小为 192kb）以及 IDE/ATAPI CD-ROM 支持。包含 Device Drivers → Initial RAM Disk Support。包含 Device Drivers → Loopback Device Support。

如果一切顺利，在经过一段时间后，你的 `boot` 目录中应该会有 `intramfs-genkernel-*`、`kernel-genkernel-*` 和 `System.map-genkernel-*` 文件。

有了新内核和 `initrd`，将它们复制到 `boot` 目录下一个更易操作的名字。这使得设置引导程序变得稍微容易。这是一个示例：

```bash
# /boot
# cp initramfs-genkernel-x86-2.6.17-gentoo-r4 initrd
```

## 设置引导程序

对于本示例，使用了 `grub` 作为

```bash
# emerge grub
```

接下来，创建 `/boot/grub/grub.cfg` 文件。以下是它可能内容的示例：

```
default 0
timeout 30
splash

title LiveCD
root (cd)
kernel vmlinuz
initrd initrd
```

如果你倾向于使用 `isolinux` 引导程序而不是 `GRUB`，你可以在 `target/` 目录下创建一个 `isolinux` 目录。然后编辑 `isolinux/linux.cfg` 文件以匹配你的配置。在 Gentoo 中，`isolinux` 组件位于 `syslinux` 包（`emerge syslinux`）。当你运行 `mkisuffs` 时，务确保确定 `isolinux` 目录中组件的位置，以便使用 `isolinux` 作为引导程序。

## 238 制作 Live Linux CD

接下来，你可以卸载之前挂载的项。要此操作，请输入以下命令：

```
# cd /root/livecd/source
# umount sys proc dev usr/portage/distfiles
```

由于你已经花费了大量时间为你的 live CD 创建文件系统，如果你有磁盘空间，考虑在开始清理之前为你的根目录（`chroot`）文件系统制作一份备份。在 `chroot` 环境之外打开一个终端窗口并输入以下命令：

```
# cd /root/livecd
# cp -ar source/ backup
```

准备好备份副本后，开始从你的 live CD 中删除不需要的文件。以下是移除你不想在 live CD 中保留文件的几种方法：

```
# cd /root/livecd/source/usr/src/linux; make clean
# cd /root/livecd
# find . -type f -name "keep" -print -exec rm {} \
# rm -rf var/tmp/*
# rm -rf var/run/*
# rm -rf var/lock/*
# rm -rf var/cache/*
# rm -rf var/db/*
# rm -rf tmp/*
# rm -rf etc/mtab
# touch etc/mtab
# rm -rf var/log
# mkdir var/log
# rm root/.bash_history
```

> 注意：运行以下命令时请务必小心，注意领先斜杠何时使用何时不使用。例如，如果你在下面的 `rm -rf tmp/*` 中错误地在目录名前加加了斜杠（`/`），你将删除已安装的 Gentoo 系统上 `/tmp` 下的所有内容，而不是你正在构建的 live CD。

你还可以考虑移除的其他文件包括 Portage 树和文档。例如，这里是可以删除的几个目录以进一步节省空间：

```
# rm -rf usr/portage/*
# rm -rf etc/portage/*
# rm -rf usr/share/doc/*
# rm -rf usr/*
```

## 制作 Live CD 镜像

要根据你创建的目录结构制作 live CD 镜像，你需要首先将 `/boot` 目录与 系统的其他部分分离。接下来，你可以将剩余的文件系统转换为 `squashfs` 文件系统，并使用这两个元素通过 `mkisofs` 命令创建 live CD。

```
# cd /root/livecd
# mkdir -p target/files/source
# cp -a source/boot target/
# cp -p -R -d source/ target/files
# cd target/files
```

下一步是将文件系统转换为单个 `squashfs` 归包。要执行此操作，请输入以下命令：

```
# mksquashfs source/ /root/livecd/target/livecd.squashfs
# touch /root/livecd/target/livecd
# cd /root/livecd/target
# rm -rf files/
```

在执行上一组命令后，你现在应该有一个 `/root/livecd/target` 目录，其中包含一个 `/boot` 目录（包含内核和启动电脑所需的文件）以及 `livecd.squashfs` 文件（代表你 live CD 文件系统的压缩镜像）。如果你想让其他任何内容进入 live CD 的根目录（例如许可证文件或 README 文件），你也可以它们放在 target 目录中。

创建 ISO 镜像的最后一步是运行 `mkisofs` 命令。这是一个示例：

```
# cd /root/livecd/target
# mkisofs -R -b boot/grub/stage2_eltorito -no-emul-boot \
--boot-load-size 4 --boot-info-table --hide-rr-moved \
-c boot.catalog -o /root/livecd.iso /root/livecd/target/
```

命令的结果是在 `/root` 目录下生成一个名为 `livecd.iso` 的 live CD 镜像。该 ISO 镜像已准备好进行测试。

## 测试 Live CD 镜像

你可以像测试任何 live CD 一样测试你的 live CD。这里有几点提示：

### 使用 qemu

你可以使用 `qemu` 包来启动你的 live CD。安装 `qemu` 包，然后使用你刚刚构建的 ISO 使用 `qemu` 命令，如下：

```
# emerge qemu
# qemu -cdrom /root/livecd.iso -boot d -m 512
```

`emerge` 命令安装 `qemu` 软件。所示的 `qemu` 命令启动 `livecd.iso` 镜像，告诉命令它是一个 CD-ROM 镜像（`-cdrom`），`qemu` 正在从 CD 镜像启动（`-boot d`），并使用 512MB 的虚拟内存运行启动的镜像（`-m 512`）。

### 刻录到介质

你当然可以将 ISO 刻录到 CD 或 DVD。由于你可能需要重做几次 CD，使用可刻写介质可能会节省费用。要进行快速擦除和刻录，你可以使用以下命令：

```
# cdrecord -v gracime=2 dev/cdrom -tao blank=fast
# cdrecord -v /root/livecd.iso
```

`cdrecord` 还有许多其他选项（尝试 `man cdrecord`）。例如，要彻底擦除 CD，请使用 `blank=all` 代替 `blank=fast`。CD 启动后，将其插入任何电脑的 CD 驱动器并重启。

如果你的 CD 上的所有内容都运行完美，你就大完成了。如果有问题，假设你保留了源目录，你可以返回并进行修正。要对你的 CD 镜像进行修正，请返回你挂载 `sys`、`proc` 等目录的地方。

## 使用 Catalyst 创建 Gentoo Live CD

`Catalyst` 是制作 live CD 的官方工具，它包含了 Gentoo 发布工程元工具（releng）中的功能，用户可以通过它扩展来制作 live CD。

> 注意：使用 `Catalyst` 制作 live CD 并不针对普通用户。本节信息旨在引导更高级的用户使用推荐的方法制作 live CD。

通过 `Catalyst`，你可以创建被称为规格文件（spec files）的各组设置和包。通过这些规格文件，你可以执行命令来制作 live CD。使用 `Catalyst`，你可以创建你自己的 live CD 设置。你可以在此处找到关于 `Catalyst` 的更多信息：

## 第 8 章 制作基础 Gentoo CD

### Catalyst 项目页面

欲获取有关 `Catalyst` 的 FAQ 和参考手册，请参考 Catalyst 项目页面（www.gentoo.org/proj/en/releng/catalyst）。最新版本的 `Catalyst` 在编写时尚未完善。

### Catalyst 邮件列表

`Catalyst` 邮件列表可能是询问构建 Gentoo live CD 问题的最佳场所。可以通过向 `catalyst+subscribe@gentoo.org` 发送邮件来订阅（接收并发送邮件），或向 `gentoo-catalyst+subscribe-digest@gentoo.org` 订阅（每几天发送一次邮件摘要）。

### 命令信息

有关 `catalyst` 命令本身的信息，请输入 `man catalyst` 或 `-help`。创建 live CD 阶段的示例规格文件可以通过安装 `livedcd-specs` 和 `livedcd-configs` 包获得。前者包含构建官方 Gentoo live CD 的文件，后者包含为不同的计算机架构配置 live CD 的文件。查看 `/usr/share/doc/catalyst-2.0*/examples/` 目录下的规格文件，以了解你可以用于创建 live CD 的设置。
