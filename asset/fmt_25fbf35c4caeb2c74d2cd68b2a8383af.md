
```bash
# chroot /mnt/sysimage
```

要返回到救援文件系统，在提示符处输入 `exit`。要重启，在救援系统的提示符处输入 `exit`。

救援功能支持软件 RAID 阵列（RAID 0、1 和 5），以及格式化为 ext2/3 的 IDE 或 SCSI 分区。当恢复设施不确定如何继续时会要求输入，最终你会以 root 身份到达命令 shell；此时无需登录或密码。根据你的配置，你可能会或不会看到额外信息的提示。如果你迷失方向或感到困惑，始终可以重新启动。（练习使用救援模式会很有帮助。）

在救援模式下，提供了多种命令行工具，但没有 GUI 工具。在网络方面，你有 `ifconfig`、`route`、`rsh` 和 `ftp` 命令。在归档（和恢复归档）方面，提供了 `gzip`、`gunzip`、`dd`、`tar` 和 `mksysm` 命令。作为编辑器，`vi` 由 BusyBox 模拟提供，而 `pico`、`jmacs` 和 `joe` 则由 `joe` 编辑器提供。还有其他有用的系统命令。仔细查看这些命令会发现，它们都是指向一个名为 BusyBox 的程序的链接（主页位于 http://www.busybox.net/）。

BusyBox 为任何小型或嵌入式系统提供了相当完整的 POSIX 环境。BusyBox 中的实用程序通常比功能齐全的 GNU 对应工具具有更少的选项；但是，所包含的选项*“提供了预期的功能，其行为非常类似于 GNU 对应工具”*。这意味着你应该首先测试救援模式，看看它是否能恢复你的数据，并检查哪些选项对你可用，因为 BusyBox 版本的行为会与完整的 GNU 版本略有不同。（某些选项缺失；某些选项的行为不完全相同——你需要在*遇到*紧急情况的*之前*知道这会影响哪里。）

使用救援模式时有几个有用的技巧需要了解。如果你的系统功能正常，你可以使用 `chroot` 命令以这种方式将根文件系统从 CD 更改为你的系统：

```bash
# chroot /mnt/sysimage
```

你会发现自己处于一个新的命令提示符，所有旧文件都在——希望——正确的位置。你熟悉的工具——如果完好无损——应该可供你使用。要退出 *chroot* 环境，使用 `exit` 命令返回到救援系统提示符。如果再次使用 `exit` 命令，系统将重新启动。

救援环境提供了一套不错的网络命令和启用网络功能的工具，如 `scp`、`sftp` 以及一些 `tools`。它还提供了 `rpm`，可以通过网络连接获取软件包。安装它们比较棘手，因为你希望将它们安装在挂载于 `/mnt/sysimage` 的文件系统中，而不是 `/`。为了实现这一点，请使用 `--root` 参数设置根目录的替代路径：

```bash
# rpm -ivh --root /mnt/sysimage ftp://location/package.rpm
```

## Fedora 救援光盘的替代方案

Fedora 救援光盘可能无法满足你的系统恢复需求：它可能缺乏特定的以太网设备支持、文件系统支持，或你成功恢复操作所需的全功能实用程序。H. Peter Anvin 创建的 SuperRescue CD 提供了一种替代方案。

基本上，SuperRescue CD 是一个相当完整且稳健的 Red Hat 发行版（基于 Red Hat 7.2 和 `2.4.28-rc1` 内核），完全可以从可引导 CD 运行。SuperRescue CD 最棒的地方在于它附带了*构建脚本*，因此添加新软件（特定的驱动程序或应用程序）并创建新 CD 非常容易。其主页位于 `http://freshmeat.net/projects/superrescue/`，但你也可以直接从 `http://www.kernel.org/pub/dist/superrescue/v2/` 获取副本。

## 相关的 Fedora 命令

以下命令在 Fedora 中执行备份、恢复和还原操作时很有用：

- `andump` — Amanda 是一个基于网络的备份系统，由 18 个独立的命令组成，适用于 Linux。
- `ark` — 一个 KDE 桌面 GUI 归档实用程序。
- `cp` — 复制命令。
- `scp` — 安全 shell 复制命令。
- `cpio` — 一个数据归档实用程序。
- `dd` — 一个数据复制和转换实用程序。
- `gzip` — GNU 压缩实用程序。
- `tar` — GNU 磁带归档实用程序。

## 参考资料

- http://www.tldp.org/LDP/solrhe/Securing-Optimizing-Linux-RH-Edition-v1.3/whywhen.html — 关于使用 `dump` 和 `restore` 进行备份的详细讨论及示例。
- http://en.tldp.org/LDP/solrhe/Securing-Optimizing-Linux-RH-Edition-v1.3/chap29sec306.html — 使用 `cron` 和 `tar` 进行自动备份。
- http://kmself.home.netcom.com/Linux/FAQs/backups.html — Linux 备份迷你 FAQ 包含关于备份介质、压缩、加密和安全性的有用但简略的评论。
- http://www.tldp.org/ — Linux 文档项目提供了几个讨论备份和磁盘恢复的有用 HOWTO 文档。
- http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/Ext2fs-Undeletion.html — 如果你需要从 ext2/3 文件系统中恢复文件，Linux Ext2fs 文件恢复迷你 HOWTO 就是你的文档。多练习会提高成功率。
- http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/Ext2fs-Undeletion-Dir-Struct.html — Ext2fs 目录结构恢复是 Linux Ext2fs 文件恢复迷你 HOWTO 的配套 HOWTO，帮助你处理误操作的 `rm -rf *`。
- http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/Bootdisk-HOWTO.html#AEN1483 — 这里列出了 LILO 启动错误代码，以帮助你调试无法正常启动的问题系统。
- http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/Ftape-HOWTO.html — 这是关于软盘磁带设备驱动的 HOWTO。
- [http://www.linux-usb.org/USB-guide/x498.html](http://www.linux-usb.org/USB-guide/x498.html)—用于大容量存储设备的 USB 指南。如果您有 USB 设备并且需要知道它是否受支持，请在此处查看。
- [http://www.backupcentral.com/amanda.html](http://www.backupcentral.com/amanda.html)—这是《Unix 备份与恢复》一书中关于 Amanda 的章节（由 John R. Jackson 撰写，O’Reilly and Associates 出版）。该章节在线可用，涵盖了使用 Amanda 的方方面面。该网站提供了针对该章节的便捷搜索工具。
- [http://twiki.org/cgi-bin/view/WikiLearn/RsyncingALargeFileBeginner](http://twiki.org/cgi-bin/view/WikiLearn/RsyncingALargeFileBeginner)—使用 rsync 传输一个大文件以“修复”未通过 md5sum 检查的本地 ISO 镜像。
- [http://www.lycoris.org/sections.php?op=viewarticle&artid=8](http://www.lycoris.org/sections.php?op=viewarticle&artid=8)—Lycoris ISO rsync 迷你 HOWTO。使用 rsync 同步文件的分步教程。
- [http://www.mikerubel.org/computers/rsync_snapshots/](http://www.mikerubel.org/computers/rsync_snapshots/)—使用 rsync 进行自动化快照式备份。
- [http://www.mondorescue.org/](http://www.mondorescue.org/)—Mondo Rescue 是一个独立于 Fedora 的裸机备份/救援工具，使用 CD、DVD、磁带或 NFS；它可以生成可启动 CD 来恢复系统。
