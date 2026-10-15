
```
sudo dd if=/tmp/hdambr of=/dev/hda bs=512 count=1
```

To restore only the partition table, skipping the boot loader code, use this:

```
sudo dd if=/tmp/hdambr of=/dev/hda bs=1 skip=446 count=66
```

Of course, it would be prudent to move the copy of the MBR to a floppy or other appropriate storage device. (The file is only 512 bytes in size.) You will need to be able to run `dd` on the system in order to restore it (which means that you will be using the Ubuntu rescue disc as described later, or any equivalent to it).

#### Booting the System from a Generic Boot Floppy

If you failed to make a boot floppy or cannot locate the one you did make, any Linux boot floppy (a slightly older version or one borrowed from a friend) can be pressed into service as long as it has a reasonably similar kernel version. (The major and minor numbers match—for example, `2.6.5` would likely work with any `2.6` system, but not with a `2.4` system.) You would boot your system by manually specifying the root and boot parti-

按前面描述的说明操作。尽管你几乎肯定会遇到一些错误消息，但你至少或许能够让一个基础系统运行起来，足以替换文件并恢复系统。

##### 提示

在上述两种情况下，都假定你不需要任何特殊的文件系统或设备驱动程序即可访问根分区。如果你确实需要，请将 `initrd=` 参数添加到 `LILO` 命令行中，指向你系统上相应的 initrd 文件。如果你不知道 initrd 文件的确切名称，那么 `LILO` 就无能为力了，所以最好也学会使用 `GRUB` 启动软盘。

#### 使用 GRUB 启动软盘

GRand Unified Boot loader（`GRUB`）可以在没有可用的定制启动软盘的情况下，尝试用一张软盘启动系统。该软盘镜像可以从 `ftp://alpha.gnu.org/gnu/grub/grub-0.95-1386-pc.ext2fs` 下载，并使用 `dd` 命令复制到软盘（在 Microsoft 系统上则使用 `rawrite.exe`）。或者，如果你有一张来自使用 `GRUB` 的现有系统的启动软盘，那张也同样可用。

`GRUB` 拥有自己的命令外壳、文件系统驱动程序和搜索功能（很像 `bash shell` 中的命令补全）。可以使用 `GRUB` 软盘启动系统、检查驱动器分区，并搜索内核和 initrd 镜像，然后用它们来启动系统。`GRUB` 的文档非常丰富，值得单独用一章来介绍：除了 `info grub`（info 系统类似于 man 文档系统）之外，`GRUB` 文档中还包含一篇值得阅读的教程。`GRUB` 启动加载程序如图 13.5 所示。

![](img/8f9e74e2b343ff525bebfb720a3d8441_350_0.png)

图 13.5 `GRUB` 启动加载程序让你即使在引导陌生系统时也拥有难以置信的灵活性。

#### 使用恢复功能

当你的计算机启动时，Ubuntu 会显示一条消息，提示你按 `Escape` 键查看 `GRUB` 菜单。如果你这样做，你会看到一个可引导操作系统列表，其中包括你的 Ubuntu 安装的恢复模式选项。如果启动进入恢复模式，你将自动获得机器的 root 访问权限，从而可以安全地修复问题。

或者，你可以插入 Ubuntu 安装光盘，并从中使用恢复模式。请记住，这些恢复模式被设计为仅用于严肃系统恢复的纯文本系统；不要指望它们有逐步指导，也不要期望它们会有多易用！

#### 相关的 Ubuntu 命令

以下命令在 Ubuntu 中执行备份、恢复和还原操作时很有用：

- `amanda`——Amanda 是一个基于网络的备份系统，由 18 个独立命令组成，用于 Linux。
- `ark`——一个 KDE 桌面 GUI 归档工具。
- `cp`——复制命令。
- `scp`——安全外壳（secure shell）复制命令。
- `cpio`——一个数据归档工具。
- `dd`——一个数据复制和转换工具。
- `gzip`——GNU 压缩工具。
- `tar`——GNU 磁带归档工具。

#### 参考

- http://www.tldp.org/LDP/solrhe/Securing-Optimizing-Linux-RH-Edition-v1.3/whywhen.html——一篇使用 dump 和 restore 进行备份的详尽讨论，附示例。
- http://en.tldp.org/LDP/solrhe/Securing-Optimizing-Linux-RH-Edition-v1.3/chap29sec306.html——使用 `cron` 定时执行 `tar` 来自动备份。
- http://kmself.home.netcom.com/Linux/FAQs/backups.html——Linux 备份迷你常见问题（FAQ）包含一些关于备份介质、压缩、加密和安全性的有用（虽然简短）评论。
- http://www.tldp.org/——Linux 文档项目（Linux Documentation Project）提供了多篇讨论备份和磁盘恢复的有用 HOWTO 文档。
- http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/Bootdisk-HOWTO.html#AEN1483——这里列出了 `LILO` 启动错误代码，帮助你调试无法启动的异常系统。
- http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/ftape-HOWTO.html——这是一篇关于软盘磁带设备驱动程序的 HOWTO 文档。
- http://www.linux-usb.org/USB-guide/x498.html——针对大容量存储设备的 USB 指南。如果你有 USB 设备并想知道它是否受支持，请到这里查看。
- http://www.backupcentral.com/amanda.html——这是《Unix Backup and Recovery》（John R. Jackson 撰写，O’Reilly and Associates 出版）中关于 Amanda 的章节。该章节在线提供，涵盖使用 Amanda 的各个方面。该网站还提供针对这一章方便的搜索工具。
- http://twiki.org/cgi-bin/view/Wikilearn/RsyncingALargeFileBeginner——对一个未通过 md5sum 校验的本地 ISO 镜像，使用 rsync 同步大文件来“修复”它。
- http://www.lycoris.org/sections.php?op=viewarticle&artid=8——Lycoris ISO rsync 迷你 HOWTO。一篇使用 rsync 同步文件的分步教程。
- http://www.mikerubel.org/computers/rsync_snapshots/——使用 rsync 的自动快照式备份。
- http://www.mondorescue.org/——Mondo Rescue 是一个独立于 Ubuntu 的裸机备份/救援工具，使用 CD、DVD、磁带或 NFS；它可以生成可引导的 CD 来恢复系统。
- http://www.ccp14.ac.uk/ccp14admin/linux-server/mondorescue/dvd_mondo.html——一篇使用 MondoRescue 备份到 DVD 的 HOWTO 文档。
- http://www.linuxorbit.com/modules.php?op=modload&name=Sections&file=index&req=viewarticle&artid=222&page=1——一篇使用 split 和 mkisofs 手动将大型归档备份到 CD 的 HOWTO 文档。

### 第14章

### 网络
