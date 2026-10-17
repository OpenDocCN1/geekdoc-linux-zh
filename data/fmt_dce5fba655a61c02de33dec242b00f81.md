
对于根磁盘，我们需要一张准备好文件系统的软盘。我们还需要一个静态链接的 BASH shell，以便我们避免共享库带来的额外复杂性。BASH 源代码中的 `configure` 程序识别用于此功能的 `--enable-static-link` 选项。我们还将使用 `--enable-minimal-config` 选项将 BASH 二进制文件的大小保持在可管理的范围内。根磁盘的额外要求是一个 `/dev` 设备和一个用于控制台的文件。控制台设备是必需的。

## 2.4. 实现

### 2.4.1. 系统启动

按照以下步骤启动系统：

- 将启动盘插入软驱驱动器并重启 PC。
- 当出现 `grub` 提示符时，输入 `kernel (fd0)/boot/vmlinuz init=/bin/sh root=/dev/fd0 load_ramdisk=1 prompt_ramdisk=1` 并按 `Enter`。
- 内核加载后，输入 `boot` 并按 `Enter`。
- 提示时插入根磁盘。

如果一切顺利，屏幕看起来应该像下面的示例。

```
grub> kernel (fd0)/boot/vmlinuz init=/bin/sh root=/dev/fd0 load_ramdisk=1 prompt_ramdisk=1
[Linux-bzimage, setup=0xc00, size=0xc29b]

grub> boot
Linux version 2.4.26
..
[ various kernel messages]

VFS: Insert root floppy disk to be loaded into RAM disk and press ENTER
RAMDISK: ext2 filesystem found at block 0
RAMDISK: Loading 1440 blocks [1] into ram disk... done.
VFS: Mounted root (ext2 filesystem) readonly.
Freeing unused kernel memory: 178k freed
#
```

### 2.4.2. 测试可用功能

尝试几个 BASH 的内置命令，看看它们是否能正常工作。

```bash
bash# echo "Hello World"
bash# cd /
bash# pwd
bash# echo *
```

### 2.4.3. 记录不可用功能

尝试其他几个熟悉的命令。

```bash
bash# ls /var
bash# mkdir /var/tmp
```

请注意，只有 BASH 内部的命令是可用的，而像 `ls` 和 `mkdir` 这样的外部命令完全无法工作。这个缺点可以在项目的未来阶段得到解决。目前，我们只需要庆幸我们的原型启动/根磁盘可以工作了，而且构建它并没有没那么困难。

### 2.4.4. 系统关机

从 `fd0` 移除软盘并使用 `CTRL-ALT-DELETE` 重启系统。

# 第 3 章 节省空间

### 3.1. 分析

原型阶段的缺点之一是磁盘集并非都有用。唯一能运行的命令是 BASH shell 内置的命令。我们可以通过安装 `cat`、`ls`、`mv`、`rm` 等命令来改进我们的根磁盘。遗憾的是，我们的空间不足。目前的根磁盘没有共享库，因此每个实用程序都必须像 BASH shell 一样进行静态链接。大量的二进制文件加上一个静态 shell，将会迅速超过 1.44M 的可用磁盘空间。我们在这一阶段的主要目标应该是最大限度地节省根磁盘空间，并为下一阶段的功能扩展铺平道路。

### 3.2. 设计

再次看一眼 Bootdisk-HOWTO，注意可以向 1.44M 软盘中挤入多少工具。有三点使得这成为。第二点是剥离二进制文件（stripped binaries）。第三点是使用压缩文件系统。我们可以利用所有技术来节省根磁盘的空间。

### 3.2.1. 共享库

首先，为了使用共享库，我们需要重新构建 BASH shell。这次我们将使用 `--enable-static-link` 选项对其进行配置。一旦重构了 BASH，我们需要弄清楚它与哪些库链接在一起，并确保它们在根磁盘上。`ldd` 命令让这项工作变得简单。通过在命令行输入 `ldd bash`，我们可以看到 BASH 使用的所有共享库列表。只要所有库都复制到根磁盘上，新的 BASH shell 就能正常工作。

### 3.2.2. 剥离二进制文件

接下来，我们应该对任何复制到根磁盘的二进制文件进行剥离。`strip` 的手册页对其作用没有给出太多描述，只说“`strip` 会丢弃文件中所有的符号”。这意味着移除二进制文件的某些部分会使其失效，但事实并非如此。这是因为其中大量被丢弃的符号被用于调试。虽然调试符号对于致力于改进代码的程序员非常有帮助，但对于普通终端用户来说，除了占用磁盘空间外没有其他作用。由于空间非常宝贵，在拷贝到 ramdisk 之前，我们应该从 BASH 和任何其他二进制文件中移除尽可能多的符号。

剥离文件以节省空间的过程也适用于共享库。在剥离库时，使用 `--strip-unneeded` 选项非常重要，以免破坏它们。使用 `--strip-unneeded` 会缩小文件大小，但重定位所需的符号将保持完好，这是共享库正常运行所需要的。

### 3.2.3. 压缩根文件系统

最后，我们可以解决如何构建压缩根文件系统的问题。Bootdisk-HOWTO 提出了三种使用 ramdisk、硬盘分区或回环设备（loopback device）构建压缩文件系统的方法。本项目将集中在使用 ramdisk 的方法上。如果根文件系统要在 ramdisk 上运行，那么在 ramdisk 上构建它也是合理的。我们需要做的是在 ramdisk 设备上创建一个第二个扩展文件系统，挂载它并将文件复制到其中。一旦文件系统加载了根磁盘所需的所有文件，我们就卸载它、压缩并将其写入软盘。

- 对于这项工作，我们需要确保构建构建系统支持 ramdisk。如果没有 ramdisk，也可以使用回环设备。关于回环设备的信息请参考 Bootdisk–HOWTO。

### 3.3. 构建

本节使用 ramdisk (`/dev/ram7`) 构建镜像。七 并没有特别之处，只要它们没有被占用，可以使用任何其他 ramdisk。

### 3.3.1. 创建 ramdisk

```bash
dd if=/dev/sd0 of=/dev/ram7 bs=1k count=409
bash# mk2fs -m0 /dev/ram7 4096
bash# mount /dev/ram7 /mnt
```

### 3.3.2. 重构 BASH shell

```bash
bash# cd /usr/src/bash-3.0
bash# make distclean
bash# export CC="gcc" -mpu=i386
bash# ./configure --enable-minimal-config --host=i386-pc
```

### 3.3.3. 确定可用性

```bash
bash# ldd bash
```

### 3.3.4. 将 BASH 及其库拷贝到 ramdisk

```bash
bash# mkdir /mnt/bin
bash# cp bash /mnt/bin
bash# ln -s bash /mnt/sh
```

### 3.3.5. 创建控制设备

```bash
bash# mkdir /mnt/dev
bash# mknod /mnt/dev/console c5 1
```

### 3.3.6. 压缩 ramdisk 镜像

```bash
bash# cd /
bash# umount /dev/ram7
bash# dd if=/dev/ram7 of=/phase2-image bs=1k count=4096
bash# gzip -9phase2-image
```

### 3.3.7. 将压缩镜像拷贝到软盘

```bash
bash# dd if=~/phase2-image.gz of=/dev/fd0 bs=1k
```

```
grub kernel (fd0)/vmlinuz init=/bin/sh root=/dev/fd0 load_ramdisk=1 prompt_ramdisk=1
[Linux-bzImage, setup=0xc00,size=0xce29b]
gub boot
```

```
Linux version 2.4.26
..\ [Various kernel messages]
..
VFS: Insert root floppy disk to be loaded into RAM disk and press ENTER
RAMDISK: Compressed image found at block 0
VFS: Mounted root (ext2 filesystem) readonly.
Freeing unused kernel memory: 178k freed
#
```

### 3.4.2. 验证结果
