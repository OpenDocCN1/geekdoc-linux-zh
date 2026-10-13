
如果没有输出，`rpm` 命令可能已成功导入 GPG 密钥。即使此命令成功，如果重复执行，将会出现“导入失败”消息。此外，GPG 密钥现在包含在 RPM 数据库中，可以通过 `rpm -qa gpg-pubkey` 命令进行验证。

在 `/etc/pki/rpm-gpg` 目录中，通常有五个 GPG 密钥可用，如表 7-1 所述。

本章后面你将看到当安装新软件包时 GPG 密钥如何从远程仓库自动导入。

## 表 7-1

| GPG 密钥 | 描述 |
|---|---|
| RPM-GPG-KEY-redhat-beta | 为 RHEL 6 beta 构建的软件包 |
| RPM-GPG-KEY-redhat-legacy-former | 2006 年 11 月之前的发行版（及更新）的软件包 |
| RPM-GPG-KEY-redhat-legacy-release | 2006 年 11 月之后的发行版的软件包 |
| RPM-GPG-KEY-redhat-legacy-rhx | 与 Red Hat Exchange 相关的软件包 |
| RPM-GPG-KEY-redhat-release | RHEL 6 的发布软件包 |

## 内核的特殊 RPM 流程

内核更新包含新功能，解决安全问题，并通常有助于 Linux 系统更好地工作。然而，内核更新也可能很麻烦，特别是如果安装了依赖于现有内核版本的专用软件包。

无论如何，如果你没有准备好重复为现有内核定制软件所采取的每一步，都不要升级内核，无论是专用驱动程序、重新编译以合并额外的文件系统，还是更多。例如，少数无线网卡和打印机的驱动程序可能与特定版本的内核绑定。一些虚拟机软件组件（不包括 KVM）可能针对特定版本的内核安装。在这些情况下，升级内核可能意味着你还必须重建相关驱动程序，以保持这些网卡、打印机和虚拟机系统运行。

如果你看到内核 RPM 的可用更新，诱惑是运行 `rpm -U newkernel` 命令。不要这样做！它会覆盖你的现有内核，如果更新的内核与系统不兼容，你就倒霉了。（好吧，并不是完全倒霉，但如果你重启并出现问题，你将不得不使用第 5 章中讨论的 Linux rescue 模式来启动系统并重新安装现有内核。在 Red Hat 考试中还有单独的故障排除和系统维护部分的日子里，这可能是一个有趣的测试场景。）

升级到新内核的最佳选项是安装它，具体使用如下命令：

```
# rpm -ivh newkernel
```

如果你连接到适当的仓库，以下命令同样有效：

```
# yum install kernel
```

这会将新内核连同相关文件一起安装，与当前正在工作的内核并排放置。其结果的一个示例显示在图 7-1 中，即 `ls /boot` 命令的输出。

### 图 7-1

`/boot` 目录中的新旧内核文件

```
[root@server1 ~]# ls /boot/
config-2.6.32-71.7.el6.x86_64      lost+found
config-2.6.32-71.el6.x86_64       symvers-2.6.32-71.7.el6.x86_64.gz
efi                              symvers-2.6.32-71.el6.x86_64.gz
grub                             System.map-2.6.32-71.7.el6.x86_64
initramfs-2.6.32-71.7.el6.x86_64.img   System.map-2.6.32-71.el6.x86_64
initramfs-2.6.32-71.el6.x86_64.img     vmlinuz-2.6.32-71.7.el6.x86_64
initrd-2.6.32-71.7.el6.x86_64kdump.img vmlinuz-2.6.32-71.el6.x86_64
[root@server1 ~]#
```

你会注意到 `/boot` 目录中有用于启动过程各个部分的不同文件，在表 7-2 中简要描述。在许多情况下，除非系统有足够的 RAM（数 GB）来支持内核崩溃转储，否则你不会看到新内核的新 initrd 文件。在我的系统上，RHEL 6 在我从 4GB 升级到 8GB RAM 之前不支持崩溃转储。因此，除非你有超过 4GB 的 RAM，否则当新内核安装时，如果你没有看到新的 `initrd.*` 文件，不必担心。

新内核的安装会在引导加载程序菜单中添加启动新内核的选项，如 GRUB 配置文件（`/boot/grub/grub.conf`）所定义，而不会擦除现有选项。修订后的 GRUB 配置文件的一个示例显示在图 7-2 中。

## 表 7-2

`/boot` 目录中的文件

| 文件 | 描述 |
|---|---|
| config-* | 内核配置设置；文本文件 |
| efi/ | 可扩展固件接口（EFI）目录；包含 GRUB 与更新的 UEFI 之间的接口 |
| grub/ | 包含 GRUB 配置文件的目录 |
| initramfs-* | 初始 RAM 磁盘文件系统，在启动过程中调用的根文件系统，用于帮助加载其他组件 |
| initrd-* | 用于内核崩溃转储的根文件系统 |
| symvers-* | 模块列表 |
| System.map-* | 系统名称到变量和函数的映射，以及它们在内存中的位置 |
| vmlinuz | 实际的 Linux 内核 |

## 图 7-2

GRUB 带第二个内核

```
root (hd0,0)
kernel /vmlinuz-version ro root=/dev/vda2
initrd /initramfs-[generic-]version.img
#boot=/dev/vda
default=0
timeout=5
splashimage=(hd0,0)/grub/splash.xpm.gz
hiddenmenu
title Red Hat Enterprise Server (2.6.32-71.7.1.el6.x86_64)
root (hd0,0)
kernel /vmlinuz-2.6.32-71.7.1.el6.x86_64 ro root=UUID=d92ce5c-d3da-40f8-9924-6ebe137560a2 rd_NO_LUKS rd_NO_LVM rd_NO_MD rd_NO_DM LANG=en_US.UTF-8 SYSFONT=latarcyrheb-sun16 KEYBOARDTYPE=pc KEYTABLE=us crashkernel=auto rhgb quiet
initrd /initramfs-2.6.32-71.7.1.el6.x86_64.img
title Red Hat Enterprise Linux (2.6.32-71.1.el6.x86_64)
root (hd0,0)
kernel /vmlinuz-2.6.32-71.1.el6.x86_64 ro root=UUID=d92ce5c-d3da-40f8-9924-6ebe137560a2 rd_NO_LUKS rd_NO_LVM rd_NO_MD rd_NO_DM LANG=en_US.UTF-8 SYSFONT=latarcyrheb-sun16 KEYBOARDTYPE=pc KEYTABLE=us crashkernel=auto rhgb quiet
initrd /initramfs-2.6.32-71.1.el6.x86_64.img
```

仔细阅读这两个段落可知，唯一的区别在于标题中列出的版本号、Linux 内核以及初始 RAM 磁盘文件系统的版本号。此外，默认内核是新安装的内核。因此，如果该内核无法工作，您可以重新启动系统，访问 GRUB 菜单，然后从旧内核启动，据推测该内核仍可工作。

如果由于某种原因，更新的内核没有更新 GRUB 启动加载程序，您所需要做的就是复制一个段落，并修改标题、内核以及初始 RAM 磁盘文件系统文件名的版本号。

## 认证目标 7.02

### 更多 RPM 命令

`rpm` 命令细节丰富。本书所能做的只是介绍 `rpm` 可以帮助您管理 RHEL 的一些基本方法。您已经读到过 `rpm` 可以以各种方式安装和升级软件包。查询可以帮助您详细识别已安装的内容。验证工具可以帮助您检查软件包和单个文件的完整性。您可以使用相关工具来帮助识别不同 RPM 的用途，以及已安装的 RPM 的完整列表。

RHCE 目标包括创建简单 RPM 软件包的要求。源代码的构建以及相关命令将在第 12 章中讨论。

### 软件包查询

最简单的 RPM 查询是验证特定软件包是否已安装。以下命令验证 Upstart 软件包的安装（您看到的版本号可能会有所不同）：

```
# rpm -q upstart
upstart-0.6.5-6.1.el6_0.1.x86_64
```
