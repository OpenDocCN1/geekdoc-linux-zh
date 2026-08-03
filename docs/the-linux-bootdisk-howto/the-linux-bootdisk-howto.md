# Linux 启动盘指南










本文档描述了如何为 Linux 设计和构建启动/根文件软盘（boot/root diskettes）。这些磁盘可以作为救援盘，也可以用于测试新的系统组件。在尝试构建启动盘之前，你应该相当熟悉系统管理任务。如果你只是想要一个应急救援盘备备之需，请参阅附录 A.1。


















# 1. 前言

本文可能已经过。如果标题页上的日期超过六个月，请检查 Bootdisk-HOWTO 主页查看是否有更新的版本。

虽然本文在文本格式下应该是清晰的，但在 Postscript、PDF 或 HTML 格式下效果会更好，因为使用了相应的排版规范。

## 1.1. 版本说明

Graham Chapman 编写了 Bootdisk-HOWTO 并支持其直到 3.1 版本。Tom Fawcett 在内核 v2 引入期间开始共同编写，他是目前文档的维护者。Chapman 已离开 Linux 社区，目前行迹不明。

此信息针对 Intel 平台上的 Linux。许多内容可能适用于其他处理器，但如果你有这方面的经验或信息，请联系我。

## 1.2. 待办事项

- User-mode-linux（https://user-mode-linux.sourceforge.net）似乎是测试启动盘而无需不断重启的好方法。我还没有时间研究。如果有人一直使用自制启动盘，请告诉我。
- 重新分析发行版启动并更新。找出 init-getty-login 序列可以如何简化，并将其移除。有些人说 init 可以直接链接到 /bin/sh；如果是这样且不产生任何限制，请修改说明以实现。这将消除对 getty、登录以及可能的 PAM 和 NSS 的需求。
- 遍历 2.4 内核源码，详细解释启动过程和内存盘加载过程的工作原理。（如果这样我能理解得更深入。）关于启动设备（例如闪存）的一些问题和限制，我还不清楚。
- 将命令替换为 LILO 关键字。

## 1.3. 反馈与致谢

欢迎对本文内容提供任何反馈（无论好坏）。我已尽力确保这里的指令和信息准确可靠，但我并非无所不知，也不跟踪内核开发。如果你发现错误或遗漏，请告诉我。在写作时，请注明你所引用的文档版本号。请礼貌对待。




我们感谢许多提供纠正和建议的人们。他们的贡献使得文档比我们独立完成的要好得多。

请通过上面的电子邮件地址向作者发送意见和纠正。在提问之前，请先阅读第 7 。不要通过电子邮件发送磁盘镜像。

## 1.4. 分发策略



# 2. 引言

Linux 启动盘在许多情况下都非常有用，例如测试新内核、从磁盘故障中恢复（从丢失引导扇区到磁盘头损坏等）、修复禁用的系统或升级关键系统文件（如 `libc.so`）。

获取启动盘有几种方法：

- 使用来自 Slackware 等发行版的启动盘。这至少让你能够启动系统。
- 使用救援包设置作为救援盘使用的启动盘。
- 学习每种磁盘运行所需的条件，然后构建自己的磁盘。

有些人选择最后一种方案，以便自己动手。这样一来，如果某些地方坏了，他们就能弄清楚如何修复它。此外，这是学习 Linux 系统如何工作的极佳方法。

本文假设读者对 Linux 系统管理概念有些基础了解。例如，您应该了解目录、文件系统和软盘。您应该知道 `/etc/passwd` 和 `fstab` 文件的用途以及它们的外观。您应该知道从头构建的启动盘中的大多数命令可能是复杂的。本 HOWTO 应该以 root 身份运行。

从头构建启动盘可能会很复杂。如果您没有读过 Linux FAQ 及其相关文档（如《Linux 安装 HOWTO》和《Linux 安装指南》），您就不应该尝试构建启动软盘。如果您只需要一个用于紧急情况的可用启动盘，下载一个预制的盘要简单得多。请参见下文附录 A.1 了解如何找到这些磁盘。

# 3. 启动盘与启动过程

启动盘基本上是软盘上的微型、自包含的 Linux 系统。它必须执行许多与完整尺寸 Linux 系统执行的相同功能。在尝试构建一个之前，您应该了解基本的 Linux 启动过程。在这里我们介绍基础知识，这些知识对于理解文档的其他部分已经足够。省略了许多细节和替代方案。

## 3.1. 启动过程

所有 PC 系统通过执行 ROM（具体为 BIOS）中的代码启动启动，以加载启动驱动器 0 柱面 0 扇区。启动驱动器通常是软盘驱动器（在 DOS 中指定为 A:，在 Linux 中指定为 /dev/fd0）。BIOS 随后尝试执行该扇区。在大多数启动盘上，0 柱面 0 扇区包含其他内容：

- 来自如 LILO 等引导加载器的代码，它定位内核并执行它以正式启动系统；
- 操作系统内核（如 Linux）的开头。

如果 Linux 内核被原始拷贝（raw-copied）到软盘上，磁盘的第一个扇区将是 Linux 内核本身的第一个扇区。该扇区将通过从启动设备加载内核的其余部分来继续启动过程。

当内核完全加载后，它会初始化设备及其内部数据结构。一旦完全初始化，它会查询镜像中一个名为 `ramdisk word` 的特殊位置。这个字告诉它如何以及在何处找到其根文件系统。根文件系统是一个挂载为 `/` 的简单文件系统。必须告诉内核去哪里寻找根文件系统；如果它找不到可加载的镜像，它就会停止。

在某些从软盘启动的情况下，根文件系统被加载到 ramdisk（内存磁盘）中，ramdisk 是系统像磁盘一样访问的内存。内存的速度比软盘快几个数量级，因此从 ramdisk 运行系统非常快。此外，内核可以将压缩的文件系统从软盘加载到 ramdisk 中，从而允许更多的文件被挤入磁盘中。

一旦根文件系统被加载并挂载，您将看到类似这样的消息：

```
VFS: Mounted root (ext2 filesystem) readonly.
```

一旦系统加载了根文件系统，它就会尝试执行 `init` 程序（位于 `/bin` 或 `/sbin` 中）。`init` 读取其配置文件 `/etc/initab`，寻找指定标识的行，并执行命名的脚本。`sysinit` 脚本通常类似于 `/etc/rc` 或 `/etc/init.d/boot`。该脚本是一系列命令的 Shell，可以设置系统服务，例如在硬盘上运行 `fck`、加载必要的内核模块、初始化网络以及挂载 `/etc/fstab` 中提到的磁盘。

此脚本调用各种其他服务进行模块化初始化。例如，在常见的 SysInit 中，`/etc/rc` 目录包含一个复杂的子目录结构，其文件指定了如何启用和关闭系统服务。然而，在启动盘上，`sysinit` 脚本通常非常简单。

当 `sysinit` 脚本返回给 `init` 时，`init` 进入 `inittab` 中 `initdefault` 关键字指定的默认运行级别。运行级别通常指定如 `getty` 的程序，它负责处理通过控制台和tty 的通信。是 `getty` 程序打印了熟悉的 `login:` 提示。`getty` 程序随后调用 `login` 程序来处理验证并设置用户会话。

## 3.2. 磁盘类型

回顾基础启动过程后，我们现在可以定义涉及的各种磁盘。我们将磁盘分为四类。此处及整个文档中的讨论除非另有说明，使用的术语 `disk` 指软盘，尽管大部分讨论也同样适用于硬盘。

**boot（启动盘）**
- 包含可以启动的内核的磁盘。该磁盘可用于启动内核，内核可能会在另一个磁盘上加载根文件系统。启动盘上的内核通常必须知道去哪里寻找其根文件系统。
- 启动盘通常从另一块软盘加载根文件系统，但启动盘也可以被设置为硬盘的根文件系统。这通常在测试新内核时完成（事实上，`make disk` 会从内核源码自动创建这样一个启动盘）。

**root（根磁盘）**
- 带有运行 Linux 系统所需文件的文件系统的磁盘。此类磁盘不一定包含内核或引导加载器。
- 一旦内核启动，根磁盘就可以独立于任何其他磁盘来运行系统。通常根磁盘会自动复制到 ramdisk 中。这使得根磁盘的访问快得多，并为工具磁盘释放出驱动器空间。

**boot/root**
- 同时包含内核和根文件系统的磁盘。换句话说，它包含了在没有硬盘的情况下启动和运行 Linux 系统所需的所有内容。这种磁盘的优点是它紧凑，所有所需内容都在单个磁盘上。然而，随着所有内容不断增大，将所有内容都放入单个软盘中变得越来越困难，即使使用了压缩。

**utility（工具磁盘）**
- 包含文件系统的磁盘，但不打算挂载为根文件系统。它是一个额外的数据磁盘。您可以使用此类磁盘来携带由于根磁盘空间不足而无法容纳的额外工具。

总来说，当我们谈论`building a bootdisk` 时，意味着同时创建启动（内核）和根（文件）部分。它们可以合在一起（单个 boot/root 磁盘），也可以分开（启动+根磁盘）。对于救援软盘，最灵活的方法可能是使用分开的启动和根软盘，以及一个或多个工具磁盘来处理溢出部分。




# 4. 构建根文件系统

创建根文件系统涉及选择系统运行所需的文件。在本节中，我们将描述如何构建压缩根文件系统。另一种不常用的选项是在直接挂载为根的磁盘上构建未压缩的文件系统；这种替代方案在第 9.1 节中描述。

## 4.1. 概述

根文件系统必须包含支持完整 Linux 系统所需的所有。为了实现这一点，磁盘必须包含 Linux 系统的最低要求：

- 基础文件系统结构。
- 最小目录集：/dev/.proc, /bin, /etc, /lib, /usr, /tmp。
- 基础工具集：sh, ls, cp, mv 等。
- 最小配置集：rc, initab, fstab 等。
- 设备：/dev/hd*, /dev/tty*, /dev/fd0 等。
- 提供工具程序所用基础运行的运行时库。

当然，任何系统只有在你可以在上面运行程序时才是有用的，而根磁盘只有在你可以执行诸如以下操作时才变得变得用：

- 在另一个驱动器上检查系统，以检查硬盘上的根文件系统，你需要能够从另一个设备启动 Linux，就像你使用根磁盘系统那样。然后你可以在原始根驱动器未挂载时对其运行 `fsck`。
- 使用 cpio、tar、gzip 和 fate 等归档和压缩工具从备份中恢复根驱动器的全部或部分内容。

我们描述如何构建压缩文件系统，是因为它在磁盘上是压缩的，在启动后，它会被解压到内存中。通过压缩文件系统，你可以在磁盘上放置许多文件（约六兆字节）。因为文件系统比磁盘大得多，因此无法在磁盘上构建。我们在其他地方构建它，对其进行压缩，然后将其复制到磁盘上。

## 4.2. 创建文件系统

为了构建这样的根文件系统，你需要一个足够大的能够存放所有备份文件的空闲设备。有几种选择：

- 使用 ramdisk (DEVICE = /dev/ram0)。在这种情况下，内存被模拟磁盘驱动器。ramdisk 必须足够大以容纳适当大小的文件系统。如果你使用 LILO，配置文件 (/etc/lilo.conf) 中类似 `RAMDISK = nnn` 的行决定了可以分配给 ramdisk 的最大内存。默认值为 4096K，应该足够了。你可能不会尝试在内存小于 8MB 的机器上使用此类 ramdisk。检查确保你有类似 /dev/ram0、/dev/ram 或 /dev/ramdisk 的设备。如果没有，使用 `mknode` 创建 /dev/ram0（主设备数 1，次设备 0）。
- 如果你有一个足够大的未使用磁盘分区（几兆字节），这是可以接受的。
- 使用回环设备 (loopback device)，它允许磁盘文件被视为设备。使用回环设备，你可以在硬盘上创建一个三兆字节的文件并在其上构建文件系统。

输入 `man losetup` 获取关于使用回环设备的说明。如果你没有 `losetup`，可以从 `util-linux` 包中连同兼容版本的 `mount` 和 `unmount` 一起获取，目录地址为 http://ftp.win.tue.nl/pub/linux/utils-linux/ 

如果你的系统上没有回环设备 (/dev/loop0, /dev/loop1 等)，你将不得不使用 `mknod /dev/loop0 b 7 0` 创建一个。一旦你安装了这些特殊的挂载和卸载二进制执行文件，在具有足够容量的硬盘上创建一个临时文件（例如 /tmp/fsfile）。你可以使用以下命令：

```
dd if=/dev/zero of=/tmp/fsfile bs=1k count=
```
来创建一个 nn 块文件。

将下方的 `DEVICE` 替换为实际的文件名。当你发布 `mount` 命令时，必须包含 `-o loop` 选项来挂载回环设备。

在选择这些选项之一后，使用以下命令准备 `DEVICE`：

```
dd if=/dev/zero of=DEVICE bs=1k count=4096
```

此命令会将设备清零。

> 清零设备至关重要，因为文件系统将进行压缩，所以所有未分配部分都应该用零填充以达到最大压缩率。每你在文件系统上移动或删除文件时，请记住此点。文件系统会释放数据块，但不会再次将它们清零。如果你进行了大量的删除和复制，你的压缩文件系统最终可能会变得比需要的大得多。

接下来是文件系统。Linux 内核识别两种根磁盘文件类型，以便自动复制到 ramdisk。两者都是 ext2，其中首选 ext2。如果你使用 ext2，发现使用 `-N` 选项来指定比默认更多的 inode 很有用：建议 `-N 2000` 以防你耗尽 inode。或者，你可以通过删除不必要的 /dev 文件来节省 inode。`mke2fs` 默认在 1.44Mb 磁盘上创建 360 个 inode。这对于你的内核根磁盘来说是充裕的，但如果你包含了 /dev 中的所有设备，你将很容易超过 360。使用压缩根允许更大的文件系统，并且默认情况下有更多的 inode，但你可能仍然需要减少文件数量或增加 inode 数量。

所以你将使用的命令类似于：

```
mke2fs -m 0 -N 2000 DEVICE
```

（如果你正在使用回环设备，应提供你正在使用的磁盘文件来替换 `DEVICE`。）

`mke2fs` 命令将自动检测空间并相应进行配置。`-m 0` 参数防止它为根目录保留空间，并在磁盘上提供更多可用空间。

接下来，挂载设备：

```
mount -t ext2 DEVICE /mnt
```

（如果 /mnt 不存在，你必须创建该目录。）在剩余章节中，所有目标目录名称均假定相对于 /mnt。

## 4.3. 填充文件系统

这是一组合理的根文件系统目录设置 [1]：

- /dev -- 设备文件，执行 I/O 所需
- /proc -- proc 系统所需的目录存根
- /etc -- 系统配置文件
- /sbin -- 关键二进制文件
- /bin -- 视为系统组成的基础二进制文件
- /lib -- 提供运行支持的共享库
- /mnt -- 用于在其他磁盘维护的挂载点
- /usr -- 额外的工具和应用程序

这三个目录在根文件系统中是空的，因此它们只需要用 `mkdir` 创建。/proc 目录在 proc 挂载之前基本上是一个占位符。/mnt 和 /usr 目录仅是启动/根系统运行后使用的挂载点。因此，这些目录也只需要创建。

其余四个目录将在后续章节中描述：

### 4.3.1. /dev

对于任何 Linux 系统，一个包含系统使用的所有设备文件的 /dev 目录是强制性的。该目录本身是一个普通目录，可以使用 `mkdir` 以普通方式创建。然而，设备文件必须以特殊方式创建，即使用 `mknod` 命令。

不过有一个快捷方法，即从你硬盘的 /dev 目录拷贝设备文件。唯一的要求是使用 `-R` 选项复制设备特殊文件。这将复制目录而不复制文件内容。务必使用大写的 `R`。例如：

```
cp -dPR /dev/[0-9]* /mnt
cp -dPR /dev/tty[0-6] /mnt
```

假设设备已挂载到 /mnt。`-d` 确保链接作为链接复制，而不是目标文件，从而保留所有权。

### 4.3.2. /etc

/etc 目录包含配置文件。它包含的内容取决于你打算运行的程序。在大多数系统中，这些文件可以分为三类：

1. 始终需要的，例如 rc、fstab、passwd。
2. 可能需要的，但谁也不太确定。
3. 溜入的垃圾文件（Junk）。

通常可以通过命令识别出不是必必需的文件：

```
ls -ltru
```

这将按最后访问时间的倒序列出文件，因此如果任何文件未被访问，它们可以从根磁盘中省略。





# Linux 启动盘指南 (HOWTO)

请确保 `passwd` 文件中包含 `root` 用户。如果你打算让其他用户登录，请确保他们的家目录和 shell 存在。

`termcap`（终端数据库）通常有几百 KB。你启动盘/根目录软磁盘上的 `termcap` 版本应该经过精简，只包含你所使用的终端，这通常只是 `linux` 或 `linux-console` 条目。

3. 其余部分。它们目前可以工作，所以我就不管它们了。

在此基础上，我实际上需要配置两个文件，而它们的内容小得惊人。

-   *rc* 应该包含：
```bash
#!/bin/sh
/bin/mount -av
/bin/hostname Kangaroo
```
确保它是安全的，确保顶部有一行 `"#1"`，并确保任何绝对路径都是正确的。你不需要运行 `hostname`，只是这样做看起来更好看。
-   *fstab* 应该包含：
```
/dev/ram0      ext2 defaults
/dev/td0       ext2 defaults
/proc           proc defaults
```

你可以从现有的 `fstab` 复制条目，但不应该自动挂载你的任何硬盘分区；对这些分区使用 `noauto` 关键字。在使用启动盘时，你的硬盘可能已经损坏或损坏。

你应该修改你的 `initab`，使 `sysinit` 行指向 `rc` 或任何将使用的基础脚本。此外，如果你想确保串口上的用户可以登录，请注释掉所有结尾带有 `ttyS0tty` 设备的 `getty` 条目。保留 `tty` 端口，以便你可以在控制台进行登录。

一个极简的 `initab` 如下所示：
```
id2:initdefault:
si:sysinit:/etc/rc
1:2345:respawn:/sbin/getty 9600 tty1
2:23:respawn:/sbin/getty 9600 tty2
```

`initab` 定义了在各种状态下运行的内容；如果 `init` 找不到程序，启动盘将挂起，可能无法进入多用户模式。请仔细检查 `initab` 中提到的文件；你可能甚至得不到错误消息。

注意，某些程序无法移动到其他地方，因为其他程序有硬编码的路径。例如，在我的系统上，`/etc/shutdown` 在 `/etc/reboot` 中是硬编码的。如果你将 `reboot` 移动到 `/bin/reboot`，然后执行 `shutdown` 命令，它将失败，并提示找不到 `reboot` 文件。

对于其余部分，只需复制 `/etc` 目录下的所有文件，以及你不确定的 `/etc` 目录下的所有可执行文件。作为参考，附录 C 中的示例列表可能足够你只复制文件，但不同系统之间的差异很大，因此请确保你系统上的同一组文件与列表是等的。唯一可靠的方法是从 `initab` 开始，推导出需要的内容。

大多数系统现在使用 `/etc/rc.d/` 目录，其中包含用于运行级别（run levels）的 shell 脚本。

## 4.3.1 /etc

`termcap`（终端数据库）通常有几百 KB。你启动盘/根目录软磁盘上的 `termcap` 版本应该经过精简，只包含你所使用的终端，这通常只是 `linux` 或 `linux-console` 条目。

## 4.3.2 /bin

`/bin` 目录是存放基本命令的地方。

## 4.3.3 /lib

`/lib` 目录包含共享库。





# Linux 启动盘 HOWTO

## 4.4.2. NSS (名称服务切换器)

如果你使用 glibc，则必须为名称服务做好准备，否则你将无法登录。`/etc/nsswitch.conf` 文件控制各种服务的数据库查找。如果你不计划从网络访问服务（例如 DNS 或 NIS 查询），你只需要准备一个所示的简单 `nsswitch.conf` 文件：

```
passwd    files
shadow    files
group     files
hosts      files
services  files
networks   files
protocols files
rpc       files
ethers    files
netmasks  files
bootparms files
automount  files
alases    files
netgroup  files
publickey files
```

这指定了仅由本地文件提供的每个服务。你还需要包含 `/lib/libnss_files.so.X`，其中 X 对于 glibc 2.0 为 1，对于 glibc 2.1 为 2。该库将被动态加载以处理文件查找。

如果你计划从你的启动盘访问网络，你可能想要创建一个更复杂的 `nsswitch.conf` 文件。详情请参阅 `nsswitch` 手页。你必须为你指定的每个服务包含一个 `/lib/libnss_service.so.1` 文件。

## 4.5. 模块

如果你有一个模块化内核，必须考虑在启动后想从启动盘加载哪些模块。如果你的备份在软盘上，你可能想要包含 `flute` 和 `ztape`；如果你想加载 SCSI 设备，则需要这些设备的模块；如果你想在紧急情况下访问网络，可能需要 PPP 或 SLIP 的模块。

这些模块可以放置在 `/lib/modules`。你还应该包含 `insmod`、`rmmod` 和 `lsmod`。取决于你是否想要自动加载模块，你可能包含 `modprobe`、`depmod` 和 `swapout`。当你使用内核时，将其连同 `/etc/conf.modules` 一起包含。

然而，使用模块的主要优势是可以非关键模块移动到实用磁盘并在需要时加载它们，从而减少根磁盘的空间。如果你可能需要处理不同的设备，这种方法比构建一个内置许多驱动程序的庞大内核要优得多。

> 为了启动压缩的 ext2 文件系统，你必须内置 ramdisk 和 ext2 支持。它们不能作为模块提供。

## 4.6. 最后的细节

某些系统程序（如 `login`）如果 `/var/run/utmp` 文件和 `/var/log` 目录不存在，将会报错。

```
mkdir -p /mnt/var/{log,run}
touch /mnt/var/run/utmp
```

最后，在你设置好所有需要的库后，运行 `ldconfig` 来重新生成根文件系统上的 `/etc/ld.so.cache`。缓存告诉加载器去哪里寻找库。你可以通过以下命令执行：

```
ldconfig -r /mnt
```

## 4.7. 总结

当你完成根文件系统的构建后，卸载它，将其拷贝到文件中并进行压缩：

```
umount /mnt
diff if=DEVICE bs=1k gzip -v9 > rootfs.gz
```

完成后，你将得到一个 `rootfs.gz` 文件。这就是你的压缩根文件系统。你应该检查它的大小，以确保它能放入软盘；否则你必须返回并移除一些文件。关于减小根文件系统大小的建议出现在第 8 节。

# 5. 选择内核

此时，你已经有了一个完整的压缩根目录。下一步是构建或选择一个内核。在大多数情况下，可以拷贝当前的内核并从该软盘启动。然而，在某些情况下，你可能希望启动一个单独的内核。

原因是大小。如果你正在制作单张启动/根软盘，内核将是软盘上最大的文件之一，因此你必须尽可能减小内核尺寸。为了减小内核尺寸，请使用支持所需系统所需的最小功能来构建它。这意味着忽略所有你不需要的内容。网络功能是一个可以省掉的，还包括在运行启动/根系统时不需要任何磁盘驱动器和其他设备的支持。如前所述，你的内核必须内置 ramdisk 和 ext2 支持。

在确定了包含在内核中的最小功能集后，你还需要确定加回哪些内容。启动/根软盘最常见的用途可能是检查和恢复损坏的根文件系统，这将内核的支持。例如，如果你的所有备份都使用 `Ftape` 访问磁带存储在磁带上，那么如果你丢失了当前的根驱动和包含 `Ftape` 的驱动，你将无法从备份磁带恢复。你必须重新安装 Linux，下载并重新安装 `fltape`，然后尝试读取你的备份。

这里的点在于，无论你为备份向内核添加了什么 I/O 支持，都应该将其添加到你的启动/根内核中。

实际构建内核的步骤在内核自带的文档中描述。它非常容易遵循，请从查看 `/usr/src/linux` 开始。如果你在构建内核时遇到困难，你可能就不应该尝试构建启动/根系统。记得使用 `makeImage` 压缩内核。

# 6. 将它们整合在一起：制作软盘

此时，你有了一个内核和一个压缩的根文件系统。如果你正在制作启动/根磁盘，请检查它们的大小，以确保它们都能放入单块磁盘中。如果你正在制作磁盘启动+根组合集，请检查根文件系统以确保它能放入单张软盘。

你应该决定是否使用 LILO 来读取启动盘内核。另一种方案是将内核直接拷贝到磁盘且不使用 LILO。使用 LILO 的优势是它允许向内核提供一些参数，这些参数对于初始化你的硬件可能是必要的（检查你系统上的 `/etc/lilo.conf` 文件。如果它存在且有一行 `append=...`，你可能需要这个功能）。使用 LILO 的劣势是构建启动盘更加复杂且占用稍多空间。你将需要建立一个小文件系统（我们称为内核文件系统），在其中传输内核以及 LILO 需要的其他几个东西。

如果你打算使用 LILO，请继续阅读；如果你打算直接传输内核，请跳到第 6.2 节。

## 6.1. 使用 LILO 传输内核

首先，确保你有最新版本的 LILO。

你必须为 LILO 创建一个小型配置文件。它看起来像这样：

```
boot      =/dev/fd0
image     /boot
map       /map
root      /
```

行的顺序并不重要，但每行都必须存在。`boot` 行指定引导程序所在的设备。`image` 行指定内核的位置。`map` 行指定 LILO 表的位置。`root` 行指定根分区。

创建该文件后，你必须运行 LILO 将其安装到启动盘：

```
lilo -c /dev/fd0
```

这将在软盘的第一扇区创建 LILO 表。该表看起来类似于所示：

| total | | | |
|---|---|---|---|
| 3 | | | |
| 1-rw---- | 1 root | root | 176 Jan 10 22 | lilo.conf |
| 1 drwxr-xx | 2 root | root | 1024 Jan 10 23 | boot/ |
| 1 drwxr-xx | 2 root | root | 1024 Jan 10 23 | dev/ |
| 3-rw---- | 1 root | root | 36270 Jan 10 23 | vmlinux |
| boot: | | | |
| total 8 | | | |
| 4-rw---- | 1 root | root | 3708 Jan 10 22 | boot.b |
| 4-rw---- | 1 root | root | 3584 Jan 10 23 | map |
| dev: | | | |
| total 0 | | | |
| 0 br-r---- | 1 root | root | 2, | 0 Jan 10 22 | fd0 |
| 0 cr-r---- | 1 root | root | 1, | 3 Jan 10 22 | null |

此表只是一个示例。数字和日期将根据你的系统而变化。

一旦运行了 LILO，你就可以从软盘启动。LILO 将读取内核和配置文件指定的参数。





```
rdev /dev/fd0 /dev/fd0
rdev -R /dev/fd0 0
```

注意在第二个 `rdev` 命令中使用大写的 `-R`。

## 6.3. 设置内存磁盘字 (ramdisk word)

内核镜像内部包含一个内存磁盘字，它指定了根文件系统所在的位置以及其他选项。可以通过 `rdev` 命令访问并设置它，其内容的解释如下：

| 位域 | 说明 |
|---|---|
| 0–10 | 内存磁盘起始偏移量，单位为 1024 字节块 |
| 11–13 | 未用 |
| 14 | 表示要加载内存磁盘的标志 |
| 15 | 表示在加载根文件系统之前提示的标志 |

如果位 15 被设置为1，在启动时你将会被提示在驱动器中加载新的软盘。这对于双盘启动集是必要的。

这里有两种情况，取决于你构建的是单块启动/根磁盘片，还是双盘 `boot-root` 磁盘集。

- 1. 如果你构建的是单个块，压缩后的文件系统将放置在内核之后（即 `KERNEL_BLOCKS`）。位 14将被设置为1，位 15将被设置为15。例如，如果你正在构建单个磁盘，且根文件系统将从块 253（十进制）开始。内存磁盘字应为 253（十进制），且位 14 设置为1，位 15 设置为0。要计算该值，你可以简单地相加十进制值：253 + (2*14) = 253+16384 =16637。如果你不知道这个数字从哪里来，可以将其输入科学计算器并转换为二进制。
- 2. 如果你构建的是双盘集，根文件系统将从第二个磁盘的零号块开始，因此偏移量为零。在这种情况下，位 14将被设置为1，位 15将被设置为1。此时的值将为 2^14+ 49152。

在计算出内存磁盘字的值后，使用 `rdev -R` 设置它。请使用十进制值。如果你使用了 LILO，此处的参数应该是挂载的内核路径，例如 `/mnt/vmlinuz`；如果你用 `dd` 拷贝的内核，请使用软盘设备名称（例如 `/dev/fd0`）。

```
rdev -R KERNEL_OFFSET_FLOPPY_DRIVE VALUE
```

如果你使用了 LILO，解锁磁盘片

> 不要相信 rdev/size 手页关于内存磁盘大小的描述。手册已经过时。从内核 2.0 版本左右，内存磁盘字不再决定内存磁盘的大小；该字根据第 6.3 节开头的表格进行解释。详细的解释请参见文档文件 ramdisk.txt 或 http://www.linuxhq.com/kernel/v2.4/doc/ramdisk.txt.html。

## 6.4. 传输根文件系统

最后一步是传输根文件系统。

- 如果根文件系统将存放在与内核相同的磁盘上，请使用 `dd` 的 `seek` 选项进行传输，该选项指定了跳过多少块：
```
dd if=rootfs.gz of=/dev/fd0 bs=1k seek=KERNEL_BLOCKS
```
- 如果根文件系统将存放在第二个磁盘上，移除第一块磁盘片，将第二个磁盘片放入驱动器，然后将其传输到根文件系统：
```
dd if=rootfs.gz of=/dev/fd0 bs=1k
```

恭喜，你完成了！

> 在将启动磁盘留作应急之前，你应该始终对其进行测试。如果启动失败，请继续阅读。

# 7. 故障排除，或失败的痛苦

在构建启动磁盘时，前几次尝试无法启动。构建根磁盘的通用方法是从现有系统中组装组件，并尝试让基于磁盘的系统达到能够在控制台上显示信息的程度。一旦它开始与你交流，战斗就成功了一半，因为你可以看到它在抱怨什么，你可以修复问题直到系统顺利运行。如果系统只是没有任何解释地挂起，找到原因可能会困难。调查系统不与你交流问题的推荐步骤如下：

- 你可能会看到这样的消息：

```
Kernel panic: VFS: Unable to mount root fs on XX:YY
```

这是一个常见问题，只有几种情况。首先，根据 `/usr/src/linux/Documentation/devices.txt` 中的设备代码列表检查设备 XX:YY。如果不正确，你可能没有使用 `dev-R`，或者你在错误的镜像上进行了操作。如果设备代码正确，检查编译到内核中的设备驱动程序。确保它内置了软磁盘、内存磁盘和 ext2 文件系统。

- 如果你看到许多类似错误：

```
end_request: I/O error, dev 01: (ramdisk, sector NNN)
```

这是来自内存磁盘的 I/O 错误，通常是因为内核尝试写入设备末之外。内存磁盘太小，无法容纳根文件系统。检查启动初始化消息中是否有如下行：

```
Ramdisk driver initialized : 16 ramdisk of 4096K size
```

再次检查此根文件系统的解压缩后大小。如果内存磁盘不够大，请增大它们。

- 检查根目录确实包含了你认为包含的目录。很容易拷贝错误的层级，导致你在根磁盘片上得到的是类似 `/root/bin` 而不是 `/bin` 的结构。

- 检查是否存在与你硬盘上 `/lib` 目录中相同的链接 `lib/libc.so`。

- 检查你现有系统中 `/dev` 目录下的任何符号链接在你的根文件系统中也存在，这些链接指向你包含在根设备中的设备。特别是 `/dev/console` 链接在许多情况下是至关重要的。

- 检查你是否包含了 `/dev/tty`、`/dev/null`、`/dev/zero`、`/dev/mem`。登录点的所有资源必须内置而不是模块。因此，内存磁盘和 ext2 支持必须内置。

- 检查你的根设备和内存磁盘设置是否正确。

涵盖这些通用情况后，还有一些特定文件需要检查：

1. 确保 `/sbin/init` 被包含在内。确保它是可执行的。
2. 对 `init` 运行 `ldd` 查看它需要什么，并确保包含了必要的库。
3. 确保包含了正确的 ELF 加载器。
4. 检查 `initstab` 中对 `getty` 的调用。
5. 确保 `/etc/initab` 有系统初始化，且它必须存在。
6. 确保你安装了能够运行所有 rc 脚本的 shell 程序（例如 **bash** 或 **ash**）。
7. 如果你在救援磁盘上有一个 `/etc/ld.so.cache` 文件，请重新制作它。





# 8. 缩小根文件系统大小

构建启动盘的主要问题之一是将所有内容都放入一张（甚至两张）软盘中。即使对文件进行压缩，这仍然非常困难，因为 Linux 系统组件在不断增长。这里是一些用于使所有内容恰容的常用技术。

## 8.1 增加软盘密度

默认情况下，软盘格式化为 1440K，但支持更高密度的格式。能否从高密度磁盘启动主要取决于你的 BIOS。**fdformat** 可以将磁盘格式化为以下大小：1600K、1680K、1722K、1743K、1760K、1840K 和 1920K。请参阅 **fdformat** 手页和 `/usr/src/linux/Documentation/devices.txt`。

但你的机器支持什么种密度呢？以下是来自 idutils 作者 Alain Knaff 的一些（经过编辑的）回答。

> 这是一个 BIOS 读取器的问题，而不是磁盘的物理格式问题。如果 BIOS 认为任何大于 18 的扇区都是坏的，那么我们也无为力。相反，与其拆解 BIOS，不如通过试错来发现。然而，如果 BIOS 支持 ED 磁盘（额外密度：每道 36 个扇区，2.88MB），那么也有可能支持 1722K 磁盘。

每道 21 个扇区的超格式化磁盘可能无法启动；这些磁盘使用了非标准的扇区大小（例如每个扇区为 1024 字节而不是 512 字节），很可能无法启动。编写一个特殊的引导扇区程序来绕过这个问题。如果我没记错，DOS 2m 工具就有这样一个怪物，OS/2 的 XDF 工具也是如此。

某些 BIOS 会人为地声称任何大于 18 的扇区号必须是无效（be-in）。这些磁盘将无法启动。最好的测试方法是将 DOS 或 linux 磁盘作为 1722K 进行测试并使其启动。如果使用 LILO，请使用 `linear` 选项（否则 LILO 将假设磁盘是每道 18 个扇区，即使 BIOS 支持，磁盘也将无法启动）。

## 8.2 使用 BusyBox 替换常用工具

根文件系统空间被 GNU 系统工具消耗，如 **cat**、**chmod**、**cp**、**dd**、**etc**。**BusyBox** 项目旨在为这些常用系统工具提供最小化替代方案。BusyBox 使用一个名为 `/bin/busybox` 的单个150K可执行文件，实现了这些工具的功能。你从不同的工具到该可执行文件创建符号链接；busybox 会识别它是如何被调用的并调用相应的代码。BusyBox 还包含一个基础 shell。许多发行版的二进制包中都提供了 BusyBox，可以在 [BusyBox 网站] 获取源码。

## 8.3 使用备用 shell

Linux 中一些流行的 shell（如 bash 和 tsh）体积很大且需要许多库。如果你不使用 BusyBox shell，仍然应该考虑替换你的 shell。一些轻量级的替代方案是 ash、lsh、kiss 和 smash，它们要小得多，且需要的库很少（或没有）。大多数此类替代 shell 都可以从 http://www.ibiblio.org/pub/Linux/system/shells/ 获取。确保你使用的任何 shell 都能在你的启动盘上包含的所有 rc 文件中运行命令。

## 8.4 剥离库和二进制文件

许多库和二进制文件在发布时带有调试信息。在这些文件上运行 `file` 命令，会显示 `not stripped`。在将二进制文件拷贝到根文件系统时，良好的做法是使用：

```
objcopy --strip-all FROM TO
```

> 拷贝库时，务必使用 `strip-debug` 而不是 `strip-all`。

## 8.5 将文件移动到工具磁盘

如果某些二进制文件启动或登录时不需要，可以将它们移动到工具磁盘。详见第 9.2 节。你也可以考虑将模块移动到工具磁盘。

# 9. 其他主题

## 9.1 非 ramdisk 根文件系统

第 4 节提供了构建压缩根文件系统的说明，它在系统启动时加载到 ramdisk 中。然而，这种方法有许多优点，因此被广泛使用。但内存不足的系统无法负担所需的 RAM，必须使用直接从软盘挂载的根文件系统。

此类系统的构建实际上比压缩根文件系统更容易，因为它们可以在软盘上而不是其他设备上构建，而且不需要压缩。我们将概述该步骤，因为它与上面的说明有所不同。如果你选择这样做，请记住你将拥有大量空间。

1. 计算根文件将有多少可用空间。如果你正在构建单盘启动/根磁盘，你必须将所有内核加上所有根文件系统都放入磁盘。
2. 使用 `mkefs` 在适当大小的软盘上创建根文件系统。
3. 按照描述填充文件系统。
4. 完成后，卸载文件系统并将其传输到数据文件中，但不要对其压缩。
5. 如上所述将内核传输到软盘。在计算 ramdisk 单词时，将第 14 位设为0，以指示根文件系统不加载到 ramdisk 中。按照描述运行 `rdev`。
6. 像以前一样传输根文件系统。

你有几种选择可以采取。如果你正在构建双盘系统，可以直接在第二块磁盘上构建完整的根文件系统，而不需要将其传输到硬盘再传回来。此外，如果你正在构建单盘启动/根磁盘并使用 LILO，你可以在整个磁盘上构建单个文件系统，包含内核、LILO 文件和根文件，只需在最后一步运行 LILO 即可。

## 9.2 构建工具磁盘

工具磁盘相对简单——只需在格式化后的磁盘上创建文件系统并将文件拷贝到其中。使用此类启动盘，在系统启动后手动挂载它。

在上面的说明中，我们提到工具磁盘可以挂载为 `/usr`。在这种情况下，二进制文件可以放在工具磁盘的 `/bin` 目录，因此将 `/usr/bin` 放入你的路径中即可访问它们。二进制文件所需的额外库放在工具磁盘的 `/lib` 中。

设计工具磁盘时有几个重要点需要注意：

1. 不要将系统二进制文件或库放在工具磁盘上，因为在系统启动之前无法挂载。
2. 在系统启动之前你无法访问工具磁盘。
3. 如果使用工具磁盘，请确保它包含应急恢复所需的工具。

# 10. 专业人士是如何做的

你可能会发现 Slackware、RedHat 或 Debian 等主流发行版的启动盘似乎比描述的要复杂。专业发行版的启动盘基于相同的原理，但采用了各种技巧。首先，它们必须能够处理各种硬件，必须能够与用户交互。其次，它们必须准备好处理许多选项，且自动化程度不一。最后，发行版启动盘通常结合了安装和救援能力。





# 11. 创建可启动 CD-ROM

> 本节由 Rizwan Mohammed Darwe 贡献
(rizwan AT clovertechnologies dot com)

本节假设你已经熟悉在 Linux 中写入 CD 的过程和原理。请将本节视为关于如何包含你将刻录的 CD 的启动能力的快速参考。《CD-Writing-HOWTO》应该为你提供更深入的参考。

## 11.1. 什么是 El Torino？

对于 x86 平台，许多 BIOS 已开始支持可启动 CD。`mkisofs` 的补丁是基于名为“El Torino”的标准。简单来说，El Torino 是一项规范，规定了如何格式化 CDROM 以便直接从中启动。

“El Torino”规范规定，只要 BIOS 支持 El Torino，任何 CDROM 驱动器（SCSI 或 EIDE）都可以工作。到目前为止，这仅在 EIDE 驱动器上经过测试，因为目前测试的所有 SCSI 控制器似乎都不支持 El Torino。主板必须支持 El Torino。你怎么知道你的主板是否支持“El Torino”呢？嗯，就是那些允许你选择从硬盘、软磁盘、网络或 CDROM 的主板。

## 11.2. 工作原理

El Torino 标准的工作原理是通过 BIOS 让 CD 看起来像是一个普通的软磁盘驱动器。简单来说，就是将任何尺寸的软磁盘镜像（1.42MB 磁盘恰好为 1440k）放在 ISO 文件系统的某处。在 ISO 文件系统的头中放置一个指向该处的指针。然后，BIOS 将从 CD 中获取此镜像，在所有用途中，它的表现就像你从软磁盘驱动器启动一样。这允许使用 LILO 启动磁盘等，仅供使用。

大致来说

## 11.3. 如何制作

创建一个名为 "boot.img" 的文件，它是你想通过 CD-ROM 启动的可启动软磁盘的镜像。这是一个 1.44 MB 的可启动软磁盘。该命令将执行此操作：

```bash
dd if=/dev/fd0 of=boot.img bs=10 count=144
```

假设软磁盘在 A: 盘。

将此镜像放置在 iso9660 文件系统的源的层级结构中。将所有与启动相关的文件放在自己的目录中是一个好主意（例如，在 iso9660 文件系统的根目录下的 "boot/" 中）。

有一个警告——你的启动软磁盘必须使用 LILO 加载任何初始内存磁盘（ramdisk），而不是内核内存磁盘驱动程序！一旦内核启动，BIOS 对 CD 作为软磁盘的仿真就会被绕过并失败。LILO 将使用 BIOS 磁盘卡加载初始内存磁盘，因此仿真会按设计工作。

El Torito 规范要求创建一个“启动目录”（boot catalog）。这是一个 2048 字节的文件，除了是必须的之外，它没有其他意义。`mkisofs` 作者完成的补丁将自动创建启动目录，你必须指定启动目录在 iso9660 文件系统中的位置。通常像以前一样将其放在启动镜像中是一个好主意，像 `boot.catalog` 这样的名字似乎是合适的。

所以我们已经在 boot.img 文件中有了镜像，并将其放在了 iso9660 文件系统根目录下的 boot/ 目录下。我们将在与 boot.catalog 相同的目录中拥有启动目录。随后用于在文件 bootcd.iso 中创建 iso9660 文件系统的命令即是：

```bash
mkisofs -r b boot.img -c boot/catalog -o bootcd.iso
```

-b 选项指定要使用的启动镜像（注意相对于 iso9660 磁盘根目录的路径），-c 选项用于启动目录文件。-r 选项将创建适当的文件所有权和模式（参阅 `mkisofs` 手册）。末尾的 `.` 表示从当前目录获取源。

现在使用通常的 `cdrecord` 命令刻录 CD，它就可以启动了。

## 11.4. 创建 Win9x 可启动 CD-ROMs

第一步是获取源 CD 使用的启动镜像。但你不能简单地在 Linux 下挂载 CD 并 `dd` 之前的 1440k 到软磁盘或文件 boot.img 中。相反，只需直接用源 CD-ROM 启动。

当你启动 Win98 CD 时，会掉入 A: 提示符符实际的内存磁盘。而 D: 或 Z: 是所有安装程序所在的地方。使用 `diskcopy` 命令将 A: 镜像复制到实际的软磁盘驱动器（现在是 B:）。该命令将执行此操作：

```bash
diskcopy A: B:
```

它的工作方式就像 `dd` 一样。你可以从这个新创建的磁盘启动，测试该过程是否与源 CD 类似。然后通常将此软磁盘通常 `dd` 到文件 boot.img，剩下的照常进行即可。

# 12. 常见问题 (FAQ) 列表

- Q: 我从我的 boot/root 磁盘启动，但什么都没有发生。我该怎么办？
- Q: Slack/Debian/RedHat 启动磁盘是如何工作的？
- Q: 我如何使用高密度（>1440K）软磁盘？我如何判断哪些密度适用于我的软磁盘？
- Q: 我如何增加我的内存磁盘的大小？
- Q: 我如何制作可启动的 CD-ROM？
- Q: 我如何制作可启动的 LS-120 磁盘？
- Q: 我可以用 XYZ 驱动程序制作启动磁盘吗？
- Q: 我如何用新文件更新我的根磁盘？
- Q: 我如何删除它们以便我使用 DOS 启动？
- Q: 如果我丢失了内核和启动磁盘，我该怎么办？
- Q: 我可以制作 boot/root 软磁盘的额外副本吗？
- Q: 能不能不需要都输入 abxxxx=nn,nn,nn 就能启动？
- Q: 启动时，我得到错误 A:无法执行 B。为什么？
- Q: 我的内核支持内存磁盘，但初始化的 0K 内存磁盘。为什么？

Q: 我从我的 boot/root 磁盘启动，但什么都没有发生。我该怎么办？

A: 见上文第 7 节。

Q: Slack/Debian/RedHat 启动磁盘是如何工作的？

A: 见上文第 10 节。

Q: 我如何使用高密度（>1440K）软磁盘？我如何判断哪些密度适用于我的软磁盘？

A: 关于此主题，请见上文中 Alain Knaff 的评论。这是我知道的最权威的答案。

Q: 我如何增加我的内存磁盘的大小？

A: 这应该在文中解释，但是……





# Linux 启动盘 HOWTO

## 参考文献 

标题为 `References`。

问：我如何用新文件更新我的根磁盘软？

答：最简单的方法是从根备份（rootback）将文件系统复制到你所使用的 DEVICE（见第 4.2 节）。然后挂载该文件系统并进行更改。你需要记住你的根文件系统在哪里，以及它占用了多少个块。

```
dd if=/dev/fd0 bs=lk skip=ROOTBEGIN count=BLOCKS | gunzip > DEVICE
mount -t ext2 device /mnt
```

进行更改后，按照第 4.7 节的方法继续，将根文件系统传输到磁盘。如果你没有更改新根文件系统的起始位置，则不需要重新传输内核或重新编译内存盘（ramdisk）。

问：我如何移除 LILO 以便我再次使用 DOS 启动？

答：这实际上不是一个启动的话题，但经常被问到。在 Linux 中，你可以运行：

```
/sbin/lilo -u
```

你也可以使用 `dd` 命令将 LILO 保存的备份复制到引导扇。如果需要，请参考 LILO 文档。

在 DOS 和 Windows 中，你可以使用 DOS 命令：

```
FDISK /MBR
```

MBR 代表主引导记录（Master Boot Record）。该命令用干净的 DOS 引导扇区替换引导扇区，而不影响分区表。一些纯主义者不同意此观点，尽管 LILO 的作者 Werner Almesberger 建议这样做。这种方法简单且有效。

问：如果我丢失了内核和启动磁盘，我该如何启动？

答：如果你没有启动磁盘，可能简单的方法如如所述，获取适用于你控制器类型（IDE 或 SCSI）的 Slackware 内核，即“如何制作带有 XXX 驱动程序的启动磁盘”。然后你可以使用此内核启动计算机，修复任何损坏。

内核可能没有包含你想要的磁盘类型和分区的根设备。例如，Slackware 的通用内核根设备是 `/dev/sda2`，而你的根 Linux 分区是 `/dev/sda8`。在这种情况下，必须更改内核中的根设备。

即使你已经有了内核以及其他操作系统（如 DOS），你也可以更改内核中的根和内存盘设置。

`rdev` 通过更改内核文件中偏移量处的值来更改内核设置，因此如果你在运行的任何系统上都有十六编辑器，你也可以执行相同的操作——例如 DOS 下的 Norton Disk Editor。然后你需要检查并在必要时更改内核中以下位置的值：

| HEX | DEC | DESCRIPTION |
| :--- | :--- | :--- |
| 0x1F8 | 504 | RAMDISK 字的低字节 |
| 0x1F9 | 505 | RAMDISK 字的高字节 |
| 0x1FC | 508 | 根主设备号 - 见下文 |
| 0x1FD | 509 | 根主设备号 - 见下文 |

# 12. 常见问题 (FAQ) 列表

主字的解释已见上文第 6.3 节。

次要设备号必须设置为你想挂载根文件系统的设备。以下是一些可选的有用值：

| DEVICE | MAJOR | MINOR | DESCRIPTION |
| :--- | :--- | :--- | :--- |
| /dev/fd0 | 2 | 0 | 第一个软盘驱动 |
| /dev/hd1 | 3 | 1 | 第一个 IDE 驱动器上的分区 1 |
| /dev/sda | 8 | 1 | 第一个 SCSI 驱动器上的分区 1 |
| /dev/sdb8 | 8 | 8 | 第一个 SCSI 驱动器上的分区 8 |

获取这些值后，可以使用 Norton Utilities Disk Editor 或名为 `rawwrite.exe` 的程序将文件写入磁盘。该程序包含在所有发行版中。这是一个 DOS 程序，它将文件写入“原始”磁盘（从引导扇区开始），而不是将其写入系统文件。如果你使用 Norton Utilities，你必须将文件挂载到物理磁盘的开头。

**问：我如何为启动/根磁盘制作额外副本？**

**答：因为磁介质可能会随着时间的推移而退化，你应该保留多个磁盘的多个副本，以防原盘无法使用。**

制作任何软盘（包括可启动盘和工具盘）副本的最简单方法是使用 `dd` 命令将原始磁盘的内容复制到硬盘上的一个文件中，然后使用相同的命令将文件复制回新软盘。注意，你不需要也不应该在 `dd` 时挂载软盘，因为 `dd` 使用原始设备接口。

要复制原始文件，输入命令：

```
dd if=DEVICEENAME of=FILENAME
```

其中 DEVICEENAME 是软盘名称，FILENAME 是（硬盘）输出文件的名称。省略 `count` 参数会导致 `dd` 复制整个软盘（如果是高密度则为 2880 个块）。

要将结果复制回新软盘，插入新软盘并输入反向命令：

```
dd if=FILENAME of=DEVICEENAME
```

注意，上述讨论假设你只有一个软盘。如果你有两个相同的软盘，可以使用类似命令复制磁盘：

```
dd if=/dev/fd0 of=/dev/fd1
```

**问：我如何不需要每次都输入 ahxxxx=nn,nn,nn？**

**答：在设备无法自动检测的情况下，必须为内核提供一个命令行设备参数字符串，例如：**

```
aha152x=0x340,11,3,1
```

使用 LILO 可以通过几种方式提供此参数字符串：

- 在每次由 LILO 启动系统时在命令行中输入。尽管这很无聊。
- 使用 LILO 的 `lock` 关键字将命令行设为默认命令行，这样 LILO 每次启动时都会使用相同的选项。
- 在 LILO 配置文件中使用 `append` 语句。注意，参数字符串必须包含引号。

例如，使用上述参数字符串的示例命令行：

```
aha152x=0x340,11,3,1 root=/dev/sda lock
```

这将传递参数字符串并设置根为 `/dev/sda`。此外，要让参数字符串生效，内核必须包含该磁盘类型的驱动程序。如果没有，你必须重新编译内核。一个 `append` 语句示例：

```
APPEND = aha152x=0x340,11,3,1
```

注意，参数字符串在命令行中不需要包含引号，但在 `append` 语句中必须包含。

如果你尝试使用大小为 0 的内存盘，行为可能是不可预测的，并导致内核崩溃（kernel panic）。





## A. 资源与链接

在获取包时，除非有充分理由，否则请始终获取最新版本。

### A.1. 预制启动盘

这些资源用于发行版启动盘。请使用其中一个镜像站点以减少这些机器的负载。

- Slackware 启动盘、发行版和 Slack 镜像站点
- RedHat 启动盘和 Red Hat 镜像站点
- Debian 启动盘和 Debian 镜像站点
- Mandrake 下载

除了发行版启动盘，还提供以下救援磁盘镜像。除非另有说明，它们位于目录

http://www.biblio.org/pub/Linux/system/recovery/!INDEX.html

- RIP 是一个救援/启动系统，有多个版本：一个适用于 1.44 英制软盘的版本，另一个适用于 CD-ROM。它支持大文件，并包含许多用于磁盘维护和救援的实用程序。它支持 ext2, ext3, iso9660, mdsfs, nfs, reisers, ufs 和 vfat。RIP 可 http://www.jux.org/pub/people/kernel-robototti/linux/rip/index.html 获取。
- tomsrbt，由 Tom Oeser 开发，是一个基于内核 2.0 的单磁盘/启动根，具有大量功能和支持程序。它支持 IDE、SCSI 带、网络适配器、PCMCIA 等。包含了约 100 个修复和恢复磁盘的实用程序和工具。该包包含了拆解和重建镜像的脚本，必要可以添加。
- rescue02，由 John Comyns 开发，是一个基于内核 1.84 的救援磁盘，支持 IDE 以及 Adapt 1542 和 NCR53C7x。它使用 ELF 二进制文件，但提供了足够的命令以便在任何系统中使用。启动后可以加载适用于所有其他 SCSI 卡的模块。在 4 mb 内存的系统上可能无法工作，除非使用 3 mb 内存磁盘。
- rescue_disk-2.0.22，由 Sergey Viznyuk 开发，是一个基于内核 2.0.22 的全功能启动/根磁盘，内置支持 IDE、多种 SCSI 控制器以及 ELF/AOUT。还包含了用于修复和恢复硬盘的模块和实用程序。
- cramdisk 镜像基于 2.0.23 内核，适用于 4MB 和 8MB 机器。它们包含了数学仿真和网络（PPP 和拨号脚本，NE2000，3C509），或对并行端口 ZIP 驱动器的支持。这些磁盘镜像可以在带有 4MB RAM 的机器上启动。包含了 MSDOS 支持，你可以从网络下载到 DOS 分区。

### A.2. 救援包

www.ibiblio.org 上提供了几个创建救援磁盘的包。通过这些包，你可以指定一组要包含的文件，软件将自动（在不同程度上）完成启动盘的创建。更多信息请参见 http://www.ibiblio.org/pub/Linux/system/recovery/!INDEX.html。*请仔细检查文件日期。*这些包中的某些已多年未更新，将不支持创建加载到内存磁盘的压缩根文件系统。据我们所知，Yard 是唯一可以做到的包。

### A.3. LILO --- Linux 加载器

由 Werner Almesberger 编写。优秀的启动加载器，文档包含了启动扇区内容和启动过程早期阶段的信息。

从 ftp://tsx-11.mit.edu/pub/linux/packages/lilo/ 获取。它在 Metalab 和镜像站也可用。

### A.4. 内存磁盘使用

在 Linux 内核提供的文档中可以找到关于内存磁盘如何工作的极佳描述。参见 /usr/src/linux/Documentation/ramdisk.txt。它由 Paul Gortmaker 编写，包含一个创建压缩内存磁盘的章节。

### A.5. Linux 启动过程

关于 Linux 启动过程的更多细节，这里是一些链接：

- 《Linux 系统管理员指南》（Linux System Administrators' Guide）有一个关于启动的章节。
- LILO 的 `Technical overview`（技术概述）提供了关于启动过程的权威技术、底层描述，直到内核启动为止。
- 源代码是终极指南。下面是与启动过程相关的内核文件。如果你有 Linux 内核源码，可以在机器的 /usr/src/linux 下找到它们；或者，Shigio Yamaguchi (shigio at tamacom.com) 有一个非常好的超文本内核浏览器，这里是一些值得查看的文件：

```
arch/i386/boot/bootsect.S and setup.S
```
包含启动扇本身的汇编代码。

```
arch/i386/boot/compressed/misc.c
```
包含解压内核的代码。

```
arch/i386/kernel/
```
包含内核初始化代码的目录。setup.c 定义了内存磁盘字。

```
drivers/block/rd.c
```
包含内存磁盘驱动程序。rd_load 和 rd_load_image 程序将块从设备加载到内存磁盘。identify_ramdisk_image 程序确定找到的是什么类型的文件系统以及它是否被压缩。

## B. LILO 启动错误代码

Usenet 上经常有人询问这些代码的问题，因此我们将其列在此处作为一项公共服务。此摘要摘自 Werner Almsberger 的 LILO 用户文档。

当 LILO 加载自身时，它会显示 LILO 字样。每个字母会在某些特定操作之前或之后打印。如果 LILO 在某处失败，可以使用目前已打印的字母来识别问题。

| 输出 | 问题 |
| --- | --- |
| (nothing) | LILO 的部分未被加载。LITITHER 要不是未安装，就是其启动扇所在的分区不是激活状态。 |
| L | 第一阶段启动加载器已加载并启动，但它无法加载第二阶段启动加载器。两位数字错误代码指示问题。（另见 `Disk codes`。）这种情况通常表示介质故障或几何不匹配（例如，磁盘参数错误）。 |
| LI | 第一阶段启动加载器能够加载第二阶段启动加载器，但未能执行它。这可能是由几何不匹配或在未运行 map 安装程序的情况下移动了 /boot/boot.b 引起的。 |
| LIL | 第二阶段启动加载器已启动，但它无法通过 map 文件加载描述表。这通常是由介质故障或几何不匹配引起的。 |
| LIL? | 第二阶段启动加载器被加载到了错误的地址。这通常是由细微的几何不匹配或在未运行 map 安装程序的情况下移动了 /boot/boot.b 引起的。 |
| LIL- | 描述表损坏。这可能是几何不匹配或在未运行 map 安装程序的情况下移动了 /boot/map 引起的。 |
| LILO | LILO 的所有部分已成功加载。 |

如果 LILO 在尝试加载启动镜像时 BIOS 信号错误，将显示相应的错误代码。这些代码范围从 0x00 到 0xb。请参见 LILO 用户指南的解释。

## C. 根文件系统列表示例

```
//
drwx--x_ 1 root 1024 Nov 1 15:39 bin
drwx--x_ 1 root 4096 Nov 1 15:39 dev
drwx--x_ 1 root 1024 Nov 1 15:39 etc
drwx--x_ 1 root 1024 Nov 1 15:39 lib
drwx--x_ 1 root 1024 Nov 1 15:39 mnt
drwx--x_ 1 root 1024 Nov 1 15:39 root
drwx--x_ 1 root 1024 Nov 1 15:39 tmp
drwx--x_ 1 root 1024 Nov 1 15:39 usr
drwx--x_ 1 root 1024 Nov 1 15:39 var
bin/
drwx--x_ 1 root 6266 Nov 1 15:39 ash
drwx--x_ 1 root 9032 Nov 1 15:39 cat
drwx--x_ 1 root 5076 Nov 1 15:39 chmod
drwx--x_ 1 root 9592 Nov 1 15:39 chown
drwx--x_ 1 root 2312 Nov 1 15:39 cp
drwx--x_ 1 root 3072 Nov 1 15:39 date
drwx--x_ 1 root 4444 Nov 1 15:39 dd
drwx--x_ 1 root 4144 Nov 1 15:39 df
drwx--x_ 1 root 6944 Nov 1 15:39 egrep
drwx--x_ 1 root 3952 Nov 1 15:39 false
drwx--x_ 1 root 6944 Nov 1 15:39 grep
drwx--x_ 1 root 45436 Nov 1 15:39 gzip
drwx--x_ 1 root 45436 Nov 1 15:39 gzip
drwx--x_ 1 root 8008 Nov 1 15:39 hostname
drwx--x_ 1 root 15284 Nov 1 15:39 ls
drwx--x_ 1 root 29308 Nov 1 15:39 ls -s
drwx--x_ 1 root 8268 Nov 1 15:39 mkdir
drwx--x_ 1 root 8920 Nov 1 15:39 mknod
drwx--x_ 1 root 37640 Nov 1 15:39 more
drwx--x_ 1 root 12240 Nov 1 15:39 mount
drwx--x_ 1 root 12932 Nov 1 15:39 mt
drwx--x_ 1 root 13324 Nov 1 15:39 mv
drwx--x_ 1 root 5388 Nov 1 15:39 ps
drwx--x_ 1 root 10092 Nov 1 15:39 rm
lrwxrkwwx 1 root 25286 Nov 1 15:39 sh -
drwx--x_ 1 root 5264 Nov 1 15:39 su
drwx--x_ 1 root 4444 Nov 1 15:39 sync
drwx--x_ 1 root 19712 Nov 1 15:39 touch
drwx--x_ 1 root 395 Nov 1 15:39 true
drwa--x_ 1 root 19084 Nov 1 15:39 ummount
drwx--x_ 1 root 5368 Nov 1 15:39 uname
/dev/
lrwxrkwwx 1 root 6 Nov 1 15:39 cdrom -> cdu31
bw-rw-rw- 1 root root 15, 0 May 5 1998 cdu31
cr--- 1 root root 4, 0 1952 console
cr-rw-rw- 1 root uucp 5, 64 Sep 9 1946 cua0
cr-rw-rw- 1 root uucp 5, 65 May 5 1998 cua1
cr-rw-rw- 1 root uucp 5, 66 May 5 1998 cua2
```





# Linux 启动指南 (HOWTO)

```
crw-rw---- 1 root uuc 5, 67 May 5 1998 cua3
brw-rw---- 1 root floppy 2, 0 Aug 8 13:54 fdd
brw-rw---- 1 root floppy 2, 36 Aug 8 13:54 fddComQ
brw-rw---- 1 root floppy 2, 84 Aug 8 13:55 fdd0104
brw-rw---- 1 root floppy 2, 88 Aug 8 13:55 fdd0112
brw-rw---- 1 root floppy 2, 12 Aug 8 13:54 fdd0360
brw-rw---- 1 root floppy 2, 120 Aug 8 13:55 fdd0720
brw-rw---- 1 root floppy 2, 32 Aug 8 13:54 fdd0880
brw-rw---- 1 root floppy 2, 104 Aug 8 13:55 fdd0200
brw-rw---- 1 root floppy 2, 208 Aug 8 13:55 fdd0352
brw-rw---- 1 root floppy 2, 212 Aug 8 13:55 fdd0384
brw-rw---- 1 root floppy 2, 228 Aug 8 13:54 fdh0140
brw-rw---- 1 root floppy 2, 124 Aug 8 13:55 fdh0168
brw-rw---- 1 root floppy 2, 44 Aug 8 13:55 fdh1722
brw-rw---- 1 root floppy 2, 76 Aug 8 13:55 fdh1743
brw-rw---- 1 root floppy 2, 96 Aug 8 13:55 fdh1760
brw-rw---- 1 root floppy 2, 114 Aug 8 13:54 fdh1840
brw-rw---- 1 root floppy 2, 200 Aug 8 13:55 fdh1920
lrwxwxrwx 1 root 7 Nov 1 15:39 fdh0360 -> fdd0360
lrwxwxrwx 1 root 52 Nov 1 15:39 fdh0720 -> fd0727
brw-rw---- 1 root floppy 68 Aug 8 13:54 fdd0830
brw-rw---- 1 root floppy 4 Aug 8 13:54 fdd1200
brw-rw---- 1 root floppy 40 Aug 8 13:54 fdd1460
brw-rw---- 1 root floppy 56 Aug 8 13:55 fdd1494
brw-rw---- 1 root floppy 72 Aug 8 13:55 fdd1494
brw-rw---- 1 root floppy 92 Aug 8 13:54 fdd1600
brw-rw---- 1 root floppy 20 Aug 8 13:54 fdd2030
brw-rw---- 1 root floppy 48 Aug 8 13:55 fdd4010
brw-rw---- 1 root floppy 64 Aug 8 13:55 fdd6420
brw-rw---- 1 root floppy 24 Aug 8 13:54 fdd0720
brw-rw---- 1 root floppy 80 Aug 8 13:55 fdd0880
brw-rw---- 1 root disk 0, 3 May 5 1998 hda
brw-rw---- 1 root disk 3, 1 May 1998 h1
brw-rw---- 1 root disk 3, 2 May 1998 hda2
brw-rw---- 1 root disk 3, 3 May 1998 hda3
brw-rw---- 1 root disk 3, 4 May 1998 hda4
brw-rw---- 1 root disk 3, 5 May 1998 hda5
brw-rw---- 1 root disk 3, 6 May 1998 hda6
brw-rw---- 1 root disk 3, 64 May 1998 hdb8
brw-rw---- 1 root disk 3, 65 May 1998 hdb9
brw-rw---- 1 root disk 3, 66 May 1998 hdb2
brw-rw---- 1 root disk 3, 67 May 1998 hdb3
brw-rw---- 1 root disk 3, 68 May 1998 hdb4
brw-rw---- 1 root disk 3, 69 May 1998 hdb5
brw-rw---- 1 root disk 3, 70 May 5 1998 hdb6
crw-rw---- 1 root knem 1, 2 May 5 1998 knem
lrwxwxrwx 1 root 12 Nov 1 15:39 modem -> ttyS1
lrwxwxrwx 1 root 12 Nov 1 15:39 mouse -> psaux
crw-rw---- 1 root root 10, 3 May 5 1998 null
crw-rw---- 1 root root 10, 1 Oct 1 20:22 peaux
brw-rw---- 1 root disk 1, 0 May 5 1998 ram0
brw-rw---- 1 root disk 1, 1 May 5 1998 ram1
brw-rw---- 1 root disk 1, 2 May 5 1998 ram2
brw-rw---- 1 root disk 1, 3 May 5 1998 ram3
brw-rw---- 1 root disk 1, 4 May 5 1998 ram4
brw-rw---- 1 root disk 1, 5 May 5 1998 ram5
brw-rw---- 1 root disk 1, 6 May 5 1998 ram6
brw-rw---- 1 root disk 1, 7 May 5 1998 ram7
brw-rw---- 1 root disk 1, 8 May 5 1998 ram8
brw-rw---- 1 root disk 1, 9 May 5 1998 ram9
我已包含了 IDE 分区。如果你使用 SCSI，请使用 `/dev/sdx` 设备。

crw-rw---- 1 root disk 4, 0 May 5 1998 tty0
brw-rw---- 1 root disk 4, 1 Nov 1 15:29 tty1
brw-rw---- 1 root disk 4, 2 Nov 1 15:29 tty2
brw-rw---- 1 root disk 4, 3 Nov 1 15:29 tty3
brw-rw---- 1 root disk 4, 4 Nov 1 15:29 tty4
brw-rw---- 1 root disk 4, 5 Nov 1 15:29 tty5
brw-rw---- 1 root disk 4, 6 Nov 1 15:29 tty6
brw-rw---- 1 root disk 4, 7 May 5 1998 tty7
brw-rw---- 1 root disk 4, 8 May 5 1998 tty8
brw-rw---- 1 root disk 4, 9 May 8:15:57 tty9
brw-rw-rw- 1 root 4, 65 May 12:27 tty1
rw-rw----- 1 root 4, 5 May 1998 zero

/etc:
rw-rw-r-- 1 root 164 Nov 15:29 conf
rw-rw-rw- 1 root 668 Nov 15:29 fstab
rw-rw-rw- 1 root 71 Nov 15:29 defs
rw-rw-rw- 1 root 389 Nov 15:29 group
rw-rw-rw- 1 root 413 Nov 15:29 initab
rw-rw-r-- 1 root 746 Nov 15:29 issue
rw-rw----- 1 root 32 Nov 15:29 cache
rw-rw----- 1 root 949 Nov 15:29 motd
drwx-x-x-2 root 1024 Nov 15:29 switch.conf
rw-rw----- 1 root 139 Nov 15:29 pam.d
rw-rw----- 1 root 516 Nov 15:29 password
drwx-x-x-2 root 387 Nov 15:29 profile
rw-rw----- 1 root 55 Nov 15:29 rc
rw-rw----- 1 root 774 Nov 15:29 shells
rw-rw----- 1 root 784 Nov 15:29 termcap
rw-rw----- 1 root Nov 15:29 ttype
lrw-xr-wx-1 root 15 Nov 15:29 utmp -> /var/run/utmp
lrw-xr-wx-1 root 15 Nov 15:29 wtmp -> /var/log/wtmp

/etc/pam.d:
/lib:
rwx-xr-xr-1 root 45415 Nov 15:29 libd-2.0.so
lrwx-xr-xr-1 root root 11 Nov 15:29 ld-linux.so.2 -> ld-2.0.so
lrwx-xr-xr-1 root root 731548 Nov 13 libc-2.0.so
lrwx-xr-xr-1 root root 13 Nov 15:29 libc.so.6 -> libc-2.0.so
lrwx-xr-xr-1 root root 17 Nov 15:29 libcm_err.so.2 -> libcm_err.so.2
lwx-xr-xr-1 root 6209 Nov 15:29 libcm_err.so.2
lrwx-xr-xr-1 root 153881 Nov 15:29 libcrypt-2.0.so
lrwx-xr-xr-1 root root 12962 Nov 15:29 libdb1-2.0.so
lrwx-xr-xr-1 root root 14 Nov 15:29 libintl-2.0.so
lrwx-xr-xr-1 root root 16 Nov 15:29 libx2fs.so.2 -> libx2fs.so.2.4
lrwx-xr-xr-1 root root 81382 Nov 15:29 libx2fs.so.2.4
lrwx-xr-xr-1 root root 25222 Nov 15:29 libnsl-2.0.so
rw-rw-x--1 root 15 Nov 15:29 libnsl.so.1 -> libnsl-2.0.so
rw-rw-x--1 root 178395 Nov 21 Nov 15:29 libfuse-2.0.so
lrwx-xr-xr-1 root root 15 Nov 15:29 libnss_files.so.1 -> libnss_files.so.2.0
lrwx-xr-xr-1 root root 14 Nov 15:29 libpam.so.0 -> libpam.so.0.64
-rw-xr-xr-1 root root 26906 Nov 15:29 libpam.so.0.64
```

# C. 根文件系统列表

```

lrw-rwwx root root 19 Nov 11:39 libpam_misc.so.64
-r-xr-xr- root root 7086 Nov 11:39 libpam_misc.so.64
-rw-rw-x- root root 35615 Nov 11:39 libpam_proc.so.1.2.6
-rw-rw-x- root root 15 Nov 11:39 libpwb.so.0 -> libpwb.so.54
-r-xr-xr-x root root 12188 Nov 11:39 libpwb.so.54
-rw-rw-x- root root 19 Nov Nov 11:39 libtcerm.so.2.0
-r-xr-xr-x root root 12041 Nov 11:39 libtcerm.so.2.8
-r-xr-xr-x root root 12874 Nov 11:39 libutil-2.7
-rw-rw-x- root root 16 Nov 11:39 libutil.so.1 -> libutil-2.7
-rw-rw-x- root root 14 Nov 11:39 libuud.so.1
-r-xr-xr-x root root 8039 Nov 11:39 libuud.so.1.1
drwx-x-x root root 1024 Nov 11:39 modules
drwx-x-x root root 1024 Nov 11:39 security

```
/lib/modules:
-drwx-x-x root root 1024 Nov 11:39 2.0.35

```
/lib/modules/2.0.35:
-drwx-x-x root root 1024 Nov 11:39 block
-drwx-x-x root root 1024 Nov 11:39 cdrom

```
/lib/modules/2.0.35/cdrom:
-drwx------ root 24108 Nov 11:39 du1.o

```
/lib/security:
-rw-r---- root 8771 Nov 11:39 permit.so

```
挂载点 (mounting):
drwx-x-x root root 1024 Nov 11:39 cd
drwx-x-x root root 1024 Nov 11:39 floppy

```
/proc:
-rwx-xr-x root root 176 Nov 11:39 .bashrc
-rwx-xr-x root root 182 Nov 11:39 .ahrc
-rwx-xr-x root root 455 Nov 11:39 .profile
-rwx-xr-x root root 4014 Nov 11:39 .tcshrc

```
/tmp/

```
/usr:
drwx-xr-x 2 root root 1024 Nov 11:39 bin
drwx-xr-x 2 root root 1024 Nov 11:39 lib
drwx-xr-x 2 root root 1024 Nov 11:39 man
drwx-xr-x 2 root root 1024 Nov 11:39 du
drwx-xr-x 1 root root 1024 Nov 11:39 share
lrwxrxr-x 1 root root 10 Nov 11:59 tmp -> ../var

```
/usr/bin:
-rw-x--x 1 root root 37164 Nov 11:59 afio
-rw-x--x 1 root root 5044 Nov 11:59 chroot
-rw-x--x 1 root root 63652 Nov 11:59 cut
-rw-x--x 1 root root 12972 Nov 11:59 diff
-rw-x--x 1 root root 56552 Nov 11:59 dun
-rw-x--x 1 root root 11552 Nov 11:59 find
-r-xr--x 1 root root 6280 Nov 11:59 free
-rw-xr--x 1 root root 7680 Nov 11:59 head
-rwx-xr--x 1 root root 8504 Nov 11:59 id
-r-sr-xr-x 1 root 4200 Nov 11:59 passwd
-rw-x--x 1 root root 14856 Nov 11:59 tail
-rw-x--x 1 root root 19008 Nov 11:59 tr
-rw-x--x 1 root root 7160 Nov 11:59 wc
-rw-x--x 1 root root 4412 Nov 11:59 whoami

```
/sbin:
-rw-xr--x 1 root root 23976 Nov 11:59 demod
-rwx-xr--x 1 root root 27460 Nov 11:59 e2fs
-rwx-xr--x 1 root root 41268 Nov 11:59 fdisk
-rw-xr--x 1 root root 9396 Nov 11:59 fsck
-rwx-xr--x 1 root root 27460 Nov 11:59 fsck_ext2
-rwx-xr--x 1 root root 29556 Nov 11:59 getty
-rwx-xr--x 1 root root 6620 Nov 11:59 halt
-rwx-xr--x 1 root root 23111 Nov 11:59 init
-rwx-xr--x 1 root root 25612 Nov 11:59 insmod
-rwx-xr--x 1 root root 10368 Nov 11:59 kernel
-rwx-xr--x 1 root root 11040 Nov 11:59 ldconfig
-rwx-xr--x 1 root root 6108 Nov 11:59 lsmod
-rwx-xr--x 1 root root 17400 Nov 11:59 mke2fs
-rwx-xr--x 1 root root 4072 Nov 11:59 mkrfs.ext2
-rwx-xr--x 1 root root 17400 Nov 11:59 mkrfs
-rwx-xr--x 1 root root 5664 Nov 11:59 mkswap
lrw-rwwx 1 root root 22032 Nov 11:59 modprobe
lrw-rwwx 1 root root 4 Nov 11:59 reboot - halt

## C. 根文件系统列表

```
-rw-x--x 1 root root 7492 Nov 1:59 rmmod
-rw-x--x 1 root root 12932 Nov 1:59 shutdown
lrwx-xr-x 1 root root 6 Nov 1:59 swapoff -> swapon
-rw-x--x 1 root root 5124 Nov 1:59 swap
-drwx-xr-x 1 root root 4 Nov 1:59 telinit -> init
-rw-x--x 1 root root 6944 Nov 1:59 update

```




# Linux 启动盘 HOWTO

| /var/log/ |
| :--- |
| -rw------ 1 root root 0 Nov 1 15:39 wtmp |
| /var/run/ |
| :--- |
| -rw----- 1 root root 0 Nov 1 15:39 utmp |
| /var/tmp/ |

## C. 根文件系统列表示例

## D. 实用工具目录列表示例

```
total 579
-rwxr-xr-x root root 42333 Jul 28 19:05 cpio
-rwxr-xr-x root root 32844 Aug 28 19:50 debuggs
-rwxr-xr-x root root 103560 Jul 29 21:31 elvis
-rwxr-xr-x root root 29536 Jul 28 19:04 fdisk
-rw-r--r root root 128254 Jul 28 19:03 ftape.o
-rwxr-xr-x root root 175764 Jul 25 03:21 ftmt
-rwxr-xr-x root root 64161 Jul 29 00:47 grpy
-rwxr-xr-x root root 45309 Jul 28 19:04 gzip
-rwxr-xr-x root root 23560 Jul 28 19:04 insmod
lrwxr-xrwx root root 118 Jul 28 19:04 lsmod
lrwxr-xrwx root root 5 Jul 28 19:00 mt -> mt-st
lrwxr-xrwx root root 9573 Jul 28 19:03 mt-st
l-rwxr-xr-x root root 6 Jul 28 19:05 rmmod -> insmod
-rwxr-xr-x root root 104085 Jul 28 19:05 tar
lrwxr-xrwx root root 5 Jul 29 21:35 vi -> elvis
```

## 注意事项

+ [1]

此处展示的目录结构仅根软盘使用。真实的 Linux 系统有一套复杂且规范的策略，被称为文件系统层次结构标准（Filesystem Hierarchy Standard），用于确定文件应该存放的位置。

