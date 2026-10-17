
```bash
[root@HostA linux-2.4.5]# make dep;make clean > /tmp/depclean
```

TEAM LinG - 活跃、信息丰富、免费且真实的！

# 通过构建新源码树安装新内核 267

你会发现输出的内容比我们列出的要多。

```
make [2]: Leaving directory '/usr/src/linux-2.4.5/arch/i386/mm'
make -C arch/i386/lib fastdep
make [2]: Entering directory '/usr/src/linux-2.4.5/arch/i386/lib'
/usr/src/linux-2.4.5/scripts/mkdep -D_KERNEL -I/usr/src/linux-
2.4.5/include -Wall -Wstruct-prototypes -O2 -fomit-frame-pointer -fno-
struct-aliasing -pipe -mpreferred-stack-boundary=2 -march=i686
checksum.s dec_and_lock.c delay getuser.c iodebug.c mempy myc.c
old-checksum.c putser.s strtr. usercopy.c - .depend
make [2]: Leaving directory '/usr/src/linux-2.4.5/arch/i386/lib'
make [1]: Leaving directory '/usr/src/linux-2.4.5'
make update-modverfile
make [1]: Entering directory '/usr/src/linux-2.4.5'
/usr/src/linux-2.4.5/include/linux/module.h was updated
make [1]: Leaving directory '/usr/src/linux-2.4.5'
bash: /tmp/de.out: No such file or directory
```

# 步骤 11. 编译内核：make bzImage

此步骤编译内核，根据系统的处理能力，可能需要一段时间。我们见过这个过程花费一个小时。请耐心等待并做好准备。

后续是使用 `make` 和 `bzImage` 的命令。注意，你必须在 `/usr/src/linux` 目录下执行这些命令，否则它们无法工作。

```
[root@HostA linux-2.4.5] # make bzImage
gcc -Wall -Wstruct-prototypes -O2 -fomit-frame-pointer -o scripts/split-
include scripts/split-include.c
scripts/split-include include/linux/autoconf.h include/config
gcc -D_KERNEL -I/usr/src/linux-2.4.5/include -Wall -Wstruct-
prototypes -O2 -fomit-frame-pointer -fno-aliasing -pipe
mpreferred-stack-boundary=2 -march=i686 -c -o init/main.c main.c
```

```
[root@HostA linux-2.4.5] # make bzImage
```

两者之间的区别仅仅在于用于压缩文件的压缩算法。不存在配置问题，只是在启动期间解压一个 `bzImage` 文件可能比解压普通的 `bzImage` 文件稍微慢一点。`bzImage` 工具相比 `bzImage` 的改进仅在于压缩率。这个比例不会覆盖现有的内核。新内核将放置在 `/usr/src/linux-2.4.5/arch/i386/boot` 目录下，并命名为 `bzImage`，如下：

TEAM Ling - Live, Informative, Non-cost and Genuine!

# 268 Linux 的定制化与升级

```
[root@HostA]$ ls -l | grep bz
-rw-r--r-- 1 root root 967412 Jul 2 09:39 bImage
```

新内核文件 `bImage` 被添加到该目录中已有的内核文件中。

Intel 机器的一个限制是内核在启动时必须在 600-700KB 的内存内进行解压缩。否则，你可能会收到指示内核过大的错误。如果你收到那样的消息，请使用 `bImage` 代替 `zImage` 来编译一个较小的内核，以此绕过此限制。

# 步骤 12. make modules 和 make modules_install

假设你通过 `make xconfig` 过程（见本章开头）选择了所需的模块，用于 `make modules` 和 `make modules_install`。如果你不重命名目录，在此步骤中执行这些命令将覆盖你现有的信息。模块位于 `/lib/modules` 目录下，路径为 `/lib/modules/<kernel_release>`。我们建议使用较早的 Linux 版本，并在执行这些命令之前对其进行重命名。你必须在 `/usr/src/linux` 目录下执行 `make modules` 和 `make modules_install` 命令，否则它们无法工作。

```
[root@HostA 2.4.5]# cd /usr/src/linux-2.4.5
[root@HostA 2.4.5]# make modules
[root@HostA 2.4.5]# make modules_install
[root@HostA src]$ ls -l /lib/modules
total 2
drwx-xr-x 4 root root 1024 Jun 18 07:09 2.4.2-2
drwx-xr-x 4 root root 1024 Jul 2 09:49 2.4.5
```

> 提示 如果你想制作一个启动盘（不包含根文件系统或 LILO），请在 A 盘中插入软磁盘并执行 `make disk` 命令。现在，你有一个带有内核的磁盘，可以在不改变系统的情况下对其进行测试。当内核是你想要的时候，再将此新内核放入你的机器中供以后使用。`make modules` 命令创建模块。`make modules_install` 将模块安装到目录。新模块应该位于你刚刚编译的内核版本目录中。如果发生错误，可能是由于某些冲突模块。要解决这些问题，回到 `oldconfig` 或 `xconfig` 阶段，反复处理内核选项。在此过程中，你可能需要使用纸笔记录一个不产生冲突的目标。你应该使用内核配置中的 `Help` 选项来研究你正在添加或删除的项。我们假设你仍然拥有对应内核版本的 `.config` 文件。这种方法在这里有效。每次只更改一点以找出问题。

# 步骤 13. 将 bzimage 内核和 System.map 复制

`/usr/src/linux/arch/i386/boot` 中的新 `bzimage` 内核文件应该复制到 `/boot` 目录。我们建议重命名此文件以免覆盖旧内核。

```
[root@Host]# cd /usr/src/linux-2.4.5/arch/i386/boot
[root@Host]# ls *
bzImage
[root@Host]# cp bzImage /boot/vmlinuz-2.4.5
[root@Host]# ls -l /boot/vm*
-rwxr-xr-x 1 root root 2208306 Apr 8 18:57 vmlinuz-2.4.2
lrwx-xr-x 1 root root 13 Jun 18 07:09 vmlinuz -> vmlinuz-2.4.5
-rw-r--r-- 1 root root 781806 Apr 8 18:57.map (Wait, 这里显示的是 2.4.2，让我们重新检查逻辑)
```

注意前面的列表中的第二个命令同时完成了复制和重命名，这样旧版本就不会被破坏。此外，链接命令给出了 LILO 将使用的通用名称 `vmlinuz`。

```
[root@Host]# rm vmlinuz
rm: remove 'vmlinuz'
[root@Host]# ln -s vmlinuz-2.4.5 vmlinuz
[root@Host]# ls -l /boot/vm*
-rwxr-xr-x 1 root root 2208306 Apr 8 18:57 vmlinuz-2.4.2
lrwx-xr-x 1 root root 13 Jun 18 07:09 vmlinuz -> vmlinuz-2.4.5
-rw-r--r-- 1 root root 781806 Apr 8 18:57 map-2.4.2
-rw-r--r-- 1 root root 967412 Jul 2 10:17 vmlinuz-2.4.5
```

你还必须替换 `System.map`，尽管某些系统有一个静态的 `System.map` 或名为 `System.map` 的符号链接需要修改和复制。内核编译时会创建一个新的 `System.map` 文件并将其到位。否则，当你重启时，内核会提示“missing System.map”错误。新的 `System.map` 将位于顶级目录 `/usr/src/linux/`。该文件的创建时间和与 `bzImage` 文件相同。再次，我们建议重命名 `System.map` 文件并创建一个链接，以免覆盖旧的 `System.map`。

```
[root@Host-linux-2.4.5] # pwd
/usr/src/linux-2.4.5
[root@Host-linux-2.4.5] # ls -l *
-rw-r--r-- 1 root root 4588 Jul 2 09:39 System.map
[root@Host-linux-2.4.5] # cp System.map /boot/System.map-2.4.5
[root@Host-linux-2.4.5] # cd /boot
[root@Host-linux-2.4.5] # ls -l Sys*
lrwxr-xr-x 1 root root 410990 Apr 8 18:57 System.map-2.4.2
-rw-r--r-- 1 root root 456588 Jul 2 10:32 System.map-2.4.5
[root@Host-linux-2.4.5] # rm System.map
rm: remove "System.map"
[root@Host-linux-2.4.5] # ln -s System.map-2.4.5 System.map
[root@Host-linux-2.4.5] # ls -l Sys*
lrwxr-xr-x 1 root root 410990 Apr 8 18:57 System.map-2.4.2
-rw-r--r-- 1 root root 456588 Jul 2 10:32 System.map-2.4.5
[root@Host-linux-2.4.5] # ls -l *module*
lrwxr-xr-x 1 root root 19 Jun 18 07:09 module-info -> module-info-2.4.2
lrwxr-xr-x 1 root root 135598 Apr 8 18:57 module-info-2.4.2
-rw-r--r-- 1 root root 135598 Jul 2 10:49 module-info-2.4.5
[root@Host-linux--2.4.5] # cp module-info-2.4.2 module-info-2.4.5
[root@Host-linux-2.4.5] # cd module-info
rm: remove "module-info*"
[root@Host-linux-2.4.5] # ln -s module-info-2.4.5 module-info
[root@Host-linux-2.4.5] # ls -l *module*
lrwxr-xr-x 1 root root 17 Jul 2 10:50 module-info -> module-info-2.4.5
-rw-r--r-- 1 root root 135598 Apr 8 18:57 module-info-2.4.2
-rw-r--r-- 1 root root 135598 Jul 2 10:49 module-info-2.4.5
```

# 步骤 14：可选：创建 RAM磁盘文件

使用初始 RAM 磁盘文件的目的是让内核能够从内核访问可能需要的模块。

# 通过构建新源码树安装新内核 27

拥有对 `modules` 目录的访问。并不是所有系统都要求你制作 `initrd` 或 RAM 磁盘，对于旧版本的内核，此操作至关重要。例如，我们希望你有更好的 SCSI 控制器。为了制作 RAM 磁盘，即你将称之为 `initrd-2.4.5` 的文件，你需要使用 `mkinitrd` 命令并将新内核作为参数，如下：

```bash
# cd /boot
# mkinitrd /boot/initrd-2.4.5 20 min
# ls -l init*
-rw-r-- 1 root root 78 Jul 15 20 initrd.img
```

完成后，在 `/boot` 目录下将有一个名为 `initrd-2.5.img` 的 RAM 磁盘文件，它将指向 `/etc/lilo.conf`。

## 15. 修改 /etc/lilo.conf 指向新内核无需 RAM 磁盘

使用你喜欢的文本编辑器对 `lilo.conf` 文件进行以下更改，如果你使用的是 RAM 磁盘：

```bash
[root@HostA /boot]# cat /etc/lilo.conf
boot=/dev/hda
map=/boot/map
install=/boot/boot.b
prompt
timeout=50
message=/boot/message
linear
default=linux
image=/boot/vmlinux-2.4.5
label=linux
read-only
root=/dev/hda
```

在你退出此部分之前，请确保 `image=` 语句指向的文件位于 `boot` 目录。`lilo -v` 命令应该告诉你，但只有你自己知道你是否拷贝了正确的文件。

## 272. 定化和升级 Linux

```bash
prompt
timeout=50
message=/boot/message
linear
default=linux
```

```bash
image=/boot/vmlinux-2.4.5
initrd=/initrd-2.5.img
label=linux
read-only
root=/dev/hda
```

## 16. 更新 MBR

现在运行 `lilo -v` 以用新的 LILO 信息更新 MBR。如果你对 `/etc/lilo.conf` 了任何更改，必须重新运行 `lilo -v` 来更新主引导记录。

```bash
# lilo -v
LILO version 21, Copyright 1992-1998 Werner Almesberger Reading boot
sector from /dev/boot Merging with /boot/boot.b
Boot image: /boot/vmlinux-2.4.5
Added linux *
/boot.boot exists - no backup copy made.
Writing boot sector.
```

## 17. 关机并测试系统：必要时救援

使用以下命令关闭并重启系统：

```bash
# shutdown -r now
```

要启动一个与 Red Hat Linux 6.1 或 6.2 等版本的系统，你可能需要两个磁盘：一个启动磁盘和一个救援磁盘。如果你有 Red Hat Linux 6.1 或 6 且系统可以从 CD-ROM 启动，你只需要 Linux CD。当从 CD-ROM 驱动器启动不是一个选项时，你需要启动磁盘。

由于 b 步骤必须快速执行，请在开始前阅读此过程。

# 通过构建新源码树安装新内核 273

1. 从启动磁盘启动 Linux（即带有启动镜像的磁盘），除非你的系统能够从 CD 启动。

2. 当 `boot :` 提示符出现时，快速输入 `rescue`——这将从磁盘或 CD-ROM 加载内核，取决于这种情况下哪种适用。

3. 按照提示操作。根据你的配置，在提示时你可能需要将启动磁盘替换为救援磁盘。

4. 当获得 shell 提示符时，你可以尝试挂载你的驱动器。

5. 创建一个空挂载点。

```bash
# mkdir /mnt/linux
# mount -t ext2 /dev/sda1 /mnt/linux
```

祝运。

如果你急于启动，也可以尝试从 Linux 安装 CD-ROM 启动。

如果你极其急于启动，可以尝试通过 DOS 访问 CD-ROM 并使用 `dosutils` 下的 `autoboot` 选项来实现。

# 索引 277

- 显示器设置 in, 64–65, 95–96

- 鼠标选择 in, 54–55, 86–88

- 多媒体支持 in, 91

- 网网卡问题 in, 43–44

- 网络配置 in, 51–53, 85–86

- 网络化工作站 in, 91

- 网络化和, 100

- FS 服务器 in, 91

- 非根用户版 in, 57–58, 88

- 软件包选择 in, 58–61, 91–92

- 分区 in, 40–50, 71–83

- PCMSIA 安装 in, 和 36

- 打印机 in, 91

- 选中项目的场景与安装 in, 62–64, 93–94

- RAID 阵列 in, 6, 74–83

- 系统重配置 in, 101

- 根救援 for, 45–46
