
Linux 使用 NFS 和 SMB 等协议支持网络文件系统。这些文件系统使用 `mount` 命令和服务器名称作为参数进行访问。

`autofs` 服务一旦使用 `/etc/auto.master` 配置好，就可以在用户进入尚未挂载的文件系统的命名目录挂载点时自动挂载文件系统。

交换空间与常规文件系统类似，使用 `mkswap` 和 `swapon` 命令创建，但仅由内核使用。

磁盘配额使用 `edquota` 命令为指定了 `usrquota` 或 `grpquota` 选项的任何文件系统进行配置。这些配额限制用户允许消耗的磁盘空间量。`ulimit` 命令是 bash shell 的一部分，也允许你限制用户可以访问的系统资源。

## 命令摘要

| 命令 | 描述 | 示例 |
|---|---|---|
| `alien` | 安装或转换软件包到不同格式，例如将 rpm 格式包转换为 Debian 格式包 | `alien --to-deb gimp-1.1.7-3.i386.rpm` |
| `chattr` | 更改分配给文件或目录的属性（另请参见 `lsattr`） | `chattr +i timesheet.doc` |
| `debugfs` | 使用交互式 shell 调试 ext2 或 ext3 文件系统的底层文件系统细节 | `debugfs /dev/hdb1` |
| `debugreiserfs` | 使用交互式 shell 调试 ReiserFS 文件系统的底层文件系统细节 | `debugreiserfs /dev/hdb1` |
| `df` | 显示当前已挂载的每个文件系统的空间使用信息 | `df` |
| `dpkg` | 管理使用 Debian 包格式创建的软件包 | `dpkg --install gimp_1.1.7-2_i386.deb` |
| `dpkg-reconfigure` | 更改已安装在系统上的 Debian 格式软件包的配置 | `dpkg-reconfigure gimp` |
| `dselect` | 用于管理 Debian 格式软件包的基于文本的菜单驱动前端；依赖于 `dpkg` 命令行实用程序 | `dselect` |
| `du` | 显示目录及其子目录中所有文件的磁盘空间使用情况 | `du /home` |
| `edquota` | 编辑分配给用户的磁盘空间配额 | `edquota` |
| `fdformat` | 格式化可移动磁盘 | `fdformat /dev/fd0` |
| `fdisk` | 用于查看和更改硬盘分区的交互式实用程序 | `fdisk /dev/hdb` |
| `fsck` | 检查文件系统的完整性，可选择修复发现的错误 | `fsck /dev/hda2` |
| `gfloppy` | 用于格式化可移动磁盘的图形程序 | `gfloppy` |
| `lsattr` | 列出分配给文件或目录的属性 | `lsattr *` |
| `mcopy` | 在 Linux 文件系统和未挂载的 DOS 格式可移动磁盘之间复制文件 | `mcopy ~/my_file A:` |
| `mdel` | 删除位于未挂载的 DOS 格式可移动磁盘上的文件 | `mdel A:my_file.doc` |
| `mdir` | 列出未挂载的 DOS 格式可移动磁盘的内容 | `mdir A:` |
| `mke2fs` | 在标记为类型 83 的现有分区内格式化（创建）ext2 或 ext3 文件系统 | `mke2fs -j /dev/hdb3` |
| `mkfs.jfs` | 在标记为类型 83 的现有分区内格式化（创建）JFS 文件系统 | `mkfs.jfs /dev/hdb3` |
| `mk reiserfs` | 在标记为类型 83 的现有分区内格式化（创建）ReiserFS 文件系统 | `mk reiserfs /dev/hdb3` |
| `mkswap` | 将标记为类型 82 的现有分区（或文件）格式化为交换空间 | `mkswap /dev/hda4` |
| `quotaon` | 使配置了 `usrquota` 或 `grpquota` 选项的文件系统开始跟踪并执行磁盘空间配额 | `quotaon` |
| `system-config-packages` | 用于在 Red Hat Linux 和 Fedora 中管理 rpm 格式软件包的图形实用程序 | `system-config-packages` |
| `repquota` | 报告文件系统上每个用户的磁盘使用情况 | `repquota /dev/hda1` |
| `rpm` | 管理 rpm 格式软件包以及跟踪已安装软件包的系统数据库 | `rpm -q gedit` |
| `swapon` | 激活已格式化的交换分区或交换文件 | `swapon` |
| `tune2fs` | 显示或更改 ext2 或 ext3 文件系统超级块中的参数 | `tune2fs /dev/hda2` |
| `ulimit` | 对在 shell 中工作的用户施加资源限制，限制诸如可运行的进程数或可使用的文件系统存储量等项目 | `ulimit -f 1024` |
| `up2date` | 使用 Red Hat Network 服务下载已升级的操作系统软件包；仅在 Red Hat Linux 或 Fedora 系统上可用 | `up2date` |

## 关键术语

`/etc/fstab` — 包含文件系统表的文件配置，其中包含设备、挂载点、文件系统类型和选项。由 `mount` 命令使用。

`autofs` — 一个系统服务，监视用户进入配置的挂载点，然后自动挂载相应的文件系统。通过 `/etc/rc.d/init.d` 中的 `autofs` 脚本进行管理。使用 `/etc/auto.master` 文件进行配置。

`disk quotas` — 分配给每个用户或组的限制，限制用户或组在文件系统上可消耗的总空间量。

`grpquota` — 可在 `/etc/fstab` 文件中使用的选项，导致文件系统跟踪每个组的磁盘空间配额。与 `quotaon` 和 `edquota` 命令一起使用。

`Journaling File System (JFS)` — 由 IBM 开发的高性能日志文件系统，可在大多数 Linux 系统上使用。

`Management` — Red Hat Network 功能的中级级别（需付费）。允许额外的升级服务，例如比较两个系统以查看它们是否安装了相同的软件包。

`Provisioning` — Red Hat Network 功能的最高级别（需付费）。允许额外的升级服务，例如升级应用程序以及操作系统文件，以及从“裸机”同时升级多个系统。

`Red Hat Network` — 由 Red Hat Software 提供的一项服务，用于自动更新使用 Red Hat Linux 或 Fedora 的系统。两个高级服务级别（Red Hat Software 收费）称为 Management 和 Provisioning。

`Red Hat Package Manager (rpm)` — 由 Red Hat Software 开发的软件包格式，被众多 Linux 发行版使用。

`ReiserFS` — 提供高性能和日志功能的 文件系统类型。默认用于多个 Linux 系统，包括 SUSE 和 Gentoo。

`software package` — 一组多个文件，以及描述信息、安全数据和安装说明。允许用户使用单个命令安装或升级应用程序或一组实用程序。Red Hat Package Manager (rpm) 格式和 Debian 格式是 Linux 上两种广泛使用的软件包格式。

`superblock` — 包含 ext2 或 ext3 文件系统详细状态信息的记录。存储在每个 ext2 或 ext3 文件系统的多个位置。使用 `tune2fs` 查看或更改。

`usrquota` — 可在 `/etc/fstab` 文件中使用的选项，导致文件系统跟踪每个用户的磁盘空间配额。与 `quotaon` 和 `edquota` 命令一起使用。

`virtual file system` — Linux 内核使用的一种方法，将程序对文件数据的访问进行通用化，以便内核可以支持多种模块化文件系统类型。

## 复习问题

1. 名称 Linux 上两种广泛使用的软件包格式，每个类型的使用的文件扩展名以及用于管理每个的命令行实用程序。

2. 在 `system-config-packages` 实用程序中，选择详细信息并检查软件包名称：

   a. 导致该软件包立即被安装

   b. 验证该软件包是否已正确安装

   c. 将软件包标记为将在选择 Update 按钮后安装的软件包，在对其他类别的软件包进行可能的更改审查后

   d. 没有任何效果，因为该实用程序仅反映在自定义安装期间所做的选择。

3. `rpm` 命令的哪个选项用于验证加密签名，以便您确切知道给定 rpm 文件的创建者或组织？

   a. `--checksig` or `-K`

   b. `-V`

   c. `-qa`

   d. `-Uvh`
