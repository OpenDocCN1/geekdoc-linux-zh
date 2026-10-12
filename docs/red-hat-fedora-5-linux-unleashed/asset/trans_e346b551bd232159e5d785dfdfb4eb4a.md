

例如，首先启动光盘并按下 F1 键。在 LILO 提示符处，输入类似以下示例的内容。请注意，你只是在告诉引导加载程序你的根分区是什么。

```
boot: linux rescue root=/dev/hda1
```

## 从通用引导软盘启动系统

如果你未能制作引导软盘，或无法找到你制作的那张软盘，只要任何 Linux 引导软盘（稍旧一点的版本或从朋友那里借来的）拥有大致相似的内核版本，就可以将其投入使用。（主要版本号和次要版本号必须匹配——例如，2.6.5 可能适用于任何 2.6 系统，但不适用于 2.4 系统。）你需要像之前描述的那样，通过手动指定根分区和引导分区来启动你的系统。虽然你几乎肯定会收到一些错误消息，但你至少应该能够运行一个基础系统，足以替换文件并恢复系统。

> **提示**
> 在上述两种情况下，都假设你访问根分区时不需要任何特殊的文件系统或设备驱动程序。如果你需要，请在指向系统中相应 initrd 文件的 LILO 行中添加 `initrd=` 参数。如果你不知道 initrd 文件的确切名称，那么使用 LILO 会很麻烦，因此最好也学习使用 GRUB 引导软盘。

## 使用 GRUB 引导软盘

GRand Unified Boot（GRUB）加载器可以尝试在没有可用的定制引导软盘的情况下，从软盘启动系统。软盘镜像可以从 ftp://alpha.gnu.org/gnu/grub/grub-0.95-1386-pc_ext2fs 下载，并使用 dd 复制到软盘（在 Microsoft 系统上会使用 `rawrite.exe`）。或者，如果你有一张来自使用 GRUB 的现有系统的引导软盘，那也可以使用。

GRUB 拥有自己的命令 shell、文件系统驱动程序和搜索功能（类似 bash shell 中的命令补全）。可以使用 GRUB 软盘启动，检查驱动器分区，并搜索内核和 initrd 镜像，并使用它们来启动系统。GRUB 文档非常详尽，足以单独成一章。除了 `info grub`（info 系统与用于文档的 man 系统类似）之外，GRUB 文档还包含一份值得阅读的教程。正是 GRUB 的灵活性和强大功能促使 Red Hat 将其作为 Fedora 的默认引导加载程序。GRUB 加载程序如图 17.5 所示。

![](img/2045828cf45e5632bf056f9ca99d6755_486_0.png)

**图 17.5** GRUB 加载器为你提供了极大的灵活性，甚至可以启动陌生的系统。

### 从安装光盘使用恢复设施

与前面的示例一样，在 LILO 引导提示符（`:`）处使用 `linux rescue` 命令以救援模式启动 DVD。救援模式从 DVD 运行一个独立于你系统的 Fedora 版本。它允许你挂载根分区以进行维护。当你的根分区因某种故障而无法引导时，这种替代方案非常有用。Fedora 正在不断改进恢复设施的功能。

在启动救援模式时，你可以选择语言和键盘布局。你有机会在救援模式下配置网络，并会看到一个基于 ncsurses 的表单以填写信息。该应用程序会尝试查找你现有的分区，并提供选择：以读写方式挂载、只读挂载（首次使用通常是明智的选择），或者跳过任何挂载并直接落入命令提示符。如果有多个分区，你还需要指示哪一个是根分区。然后该分区将被挂载到 `/mnt/sysimage`。当你最终看到命令提示符时，就可以将你的系统设置为根文件系统：

```
# chroot /mnt/sysimage
```

要返回救援文件系统，请在提示符处键入 **exit**。要重启，请在救援系统的提示符处键入 **exit**。

救援功能确实支持软件 RAID 阵列（RAID 0、1 和 5），以及格式化为 ext2/3 的 IDE 或 SCSI 分区。如果程序不确定如何继续，它会请求输入，最终你将进入 root 命令 shell；没有登录或密码。根据你的配置，你可能会出现或不出现额外信息的提示。如果你迷路或困惑了，你总是可以重启。（有助于练习使用救援模式。）

在救援模式下，提供了一些命令行工具供你使用，但未提供 GUI 工具。对于网络，你有 `ifconfig`、`route`、`rcp`、`rlogin`、`rsh` 和 `ftp` 命令。对于归档（以及恢复归档），有 `gzip`、`gunzip`、`dd`、`zcat` 和 `md5sum` 命令。至于编辑器，`vi` 由 BusyBox 模拟，而 `pico`、`jjacs` 和 `joe` 由 joe 编辑器提供。还有其他有用的系统命令。仔细查看这些命令可以发现，它们都是指向一个名为 BusyBox 的程序的链接（主页位于 http://www.busybox.net/）。

BusyBox 为任何小型或嵌入式系统提供了相当完整的 POSIX 环境。BusyBox 中的实用程序通常没有其功能齐全的 GNU 对应程序那么多选项；但是，包含的选项“提供了预期的功能，并且行为与其 GNU 对应程序非常相似。”这意味着你应该先测试救援模式，看看它是否能够恢复你的数据，并检查哪些选项对你可用，因为 BusyBox 版本的行为将与完整的 GNU 版本略有不同。（某些选项缺失；某些选项的行为不完全相同——你需要知道这是否会影响你，以便在紧急情况下做好准备。）

使用救援模式时，有一些有用的小技巧需要了解。如果你的系统运行正常，你可以使用 `chroot` 命令以这种方式将根文件系统从 CD 更改为你的系统：

```
$ chroot /mnt/sysimage
```

你会发现自己在一个新的命令提示符下，所有旧文件——希望——都在正确的位置。你熟悉的工具——如果完好无损——应该可供你使用。要退出 chroot 环境，请使用 `exit` 命令返回到救援系统提示符。如果你再次使用 `exit` 命令，系统将重启。

救援环境提供了一套不错的网络命令和启用网络的工具，例如 `scp`、`sftp` 以及一些 rtools。它还提供了 `rpm`，可以通过网络连接获取软件包。安装它们很棘手，因为你希望它们安装在挂载到 `/mnt/sysimage` 的文件系统中，而不是 `/`。要做到这一点，请使用 `--root` 参数设置替代的根路径：

```
# rpm -ivh --root /mnt/sysimage ftp://location/package.rpm
```

# FEDORA 救援光盘的替代方案

Fedora 救援光盘可能无法满足你的系统恢复需求；它可能缺乏特定的以太网设备支持、文件系统支持，或者你进行成功恢复操作所需的全功能实用程序功能。由 H. Peter Anvin 创建的 SuperRescue CD 提供了一种替代方案。

基本上，SuperRescue CD 是一个相当完整和健壮的 Red Hat 发行版（基于 Red Hat 7.2 和 2.4.20-rc1 内核），它完全从可引导 CD 运行。SuperRescue CD 最好的地方在于它附带了构建脚本，因此添加新软件（那个特殊的驱动程序或应用程序）并创建新的 CD 非常容易。主页位于 http://freshmeat.net/superrescue/，但你也可以直接在 http://www.kernel.org/pub/dist/superrescue/v2/ 获取副本。

# 相关的 FEDORA 命令

以下命令在 Fedora 中执行备份、恢复和还原操作时有用：

- `amdump`——Amanda 是一个基于网络的备份系统，由 18 个独立的命令组成，用于 Linux。
- `ark`——一个 KDE 桌面 GUI 归档实用程序。
- `cp`——复制命令。
- `scp`——安全 shell 复制命令。
- `cpio`——一个数据归档实用程序。
- `dd`——一个数据复制和转换实用程序。
- `gzip`——GNU 压缩实用程序。
- `tar`——GNU 磁带归档实用程序。

# 参考

- http://www.tldp.org/LDP/solrhe/Securing-Optimizing-Linux-RH-Edition-v1.3/whywhen.html——对使用 dump 和 restore 进行备份的全面讨论及示例。
- http://en.tldp.org/LDP/solrhe/Securing-Optimizing-Linux-RH-Edition-v1.3/chap29sec306.html——使用 cron 和 tar 进行自动备份。
- http://kmsel.home.netcorn.com/Linux/FAQs/backups.html——Linux 备份迷你 FAQ 包含一些有用但简短的关于备份介质、压缩、加密和安全性的评论。
- http://www.tldp.org/——Linux 文档项目提供了一些有用的 HOWTO 文档，讨论备份和磁盘恢复。
- http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/Ext2fs-Undeletion.html——如果你需要从 ext2/3 文件系统中恢复误删的文件，Linux Ext2fs Undeletion 迷你 HOWTO 就是为你准备的文档。如果你进行练习，成功的可能性会更大。
- http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/Ext2fs-Undeletion-Dir-Struct.html——ext2fs 目录结构恢复是 Linux Ext2fs Undeletion 迷你 HOWTO 的配套 HOWTO，帮助你应对误用的 `rm -rf *`。
- http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/Bootdisk-HOWTO.html#AEN1483——这里列出了 LILO 引导错误代码，以帮助调试无法正常启动的故障系统。
- http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/Tape-HOWTO.html——这是软盘磁带设备驱动的 HOWTO。

