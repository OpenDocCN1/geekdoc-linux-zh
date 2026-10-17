
- 确保你已将`/mnt/sysimage`目录的内容制作到你的当前工作环境中。

- 使用`grub2-install`命令，后跟想要重新安装 GRUB 2 的设备名称。因此，在 KVM 虚拟机上，使用的命令是`grub2-install /dev/vda`；而在物理服务器或 VMware 或 VirtualBox 虚拟机上，则是`grub2-install /dev/sda`。

## 使用救援盘重新创建 initramfs

偶尔 initramfs 镜像也会损坏。如果发生这种情况，你将无法让服务器进入正常运行模式。要修复进入救援环境的 initramfs 镜像，你可以使用`dracut`命令。如果不带任何参数使用，该命令将为当前加载的内核创建一个新的 initramfs。

或者，你可以使用带有多个选项的`dracut`命令为特定的内核环境创建 initramfs。还有一个名为`/etc/dracut.conf`的配置文件，你可以使用它在重新创建 initramfs 时包含特定选项。dracut 的配置分布在不同的位置：

- `/usr/lib/dracut/conf.d/*.conf`包含系统默认配置文件。
- `/etc/dracut.conf`包含自定义的 dracut 文件。
- `/etc/dracut.conf`被用作主配置文件。

列表 19.1 显示了`dracut.conf`配置文件的示例。

### 列表 19.1 /etc/dracut.conf 默认内容

```
[root@server1 ~]# cat /etc/dracut.conf
# 将你的配置写在这里或单独的文件 *.conf 中
# 在 /etc/dracut.conf
# 参见 man dracut.conf(5)
```

```
# Sample dracut 配置文件

#logfile=/var/log/dracut.log
#fileloglvl=6

# 要使用的 dracut 模块精确列表。此处未列出的模块将# 不会被包含。如果你只想添加某些可选模块
# 请使用 add_dracutmodules 选项。
#dracutmodules+=""

# 要省略的 dracut 模块
#omit_dracutmodules=""

# 添加到默认的 dracut 模块
#add_dracutmodules+=""

# 添加到默认的额外内核模块
#add_drivers+=""

# 要包含在通用 initramfs 中的内核文件系统模块
#filesystems+=""

# 仅为启动当前硬件构建 initrd
#hostonly="yes"
#

# 安装本地的 /etc/mdadm.conf
#mdadmconf="no"

# 安装本地的 /etc/lvm.conf
#lvmconf="no"

# 要安装的 fsck 工具列表。如果没有指定，则使用硬编码的
# 默认，当前为："umount /sbin/fsck* xfs_db xfs_-
# check xfs_repair e2fsck jfs_fsck reiserfsck btrfsck"。安装是
# 机会性的，因此不存在的工具会被忽略。
#fscks=""
```

```
# 禁止安装任何 fsck 工具
#nofscks="yes"

# 默认挂载 / 和 /usr 为只读
#ro_mnt="no"

# 设置临时文件的目录
# 默认: /var/tmp
#tmpdir=/tmp
```

> 提示：根据 Red Hat 的目标，你在考试中不应该需要处理救援盘。然而，作为一名 RHCSA 也是一名 RHCE，你应该预料意之外的情况，因此确保你能够处理常见以及较少见的故障排除场景是一个好主意。

## 修复常见问题

在像这样简短的章节中，不可能考虑到在处理 Linux 时可能遇到的所有可能问题。不过，某些问题比其他问题更容易发生。在这一节中，你将学习一些更常见的问题。

## 重装 GRUB 2

引导加载程序代码不会无无故消失，但偶尔会发生 GRUB 2 引导代码损坏。在这种情况下，你最好知道如何重装 GRUB 2。具体方法取决于你的服务器是否仍处于可启动状态。如果是，重装 GRUB 2 相当简单。只需输入`grub-install`后跟你想要安装的设备名称。该命令有许多不同选项可以微调具体安装的内容，但你不需要它们，因为默认情况下，该命令会安装让你的系统再次启动所需的所有内容。

如果你的机器处于不可启动状态，情况会变得复杂一点。如果发生这种情况，你首先需要启动救援系统，并从救援系统恢复对服务器的访问。（具体操作步骤请参见练习 19.2）。在将服务器的文件挂载到`/mnt/sysimage`并使用`chroot /mnt/sysimage`将挂载的系统映像变为你的根映像后，操作如之前描述简单：只需运行`grub2-install`在 KVM 虚拟机上安装设备，命令为`grub2-install /dev/vda`；而在物理服务器或 VMware 或 VirtualBox 虚拟机上，则是`grub2-install /dev/sda`。

## 修复 Initramfs

在像这样简短的章节中，不可能考虑到在处理 Linux 时可能遇到的所有可能问题。不过，某些问题比其他问题更容易发生。在这一节中，你将学习一些更常见的问题。

或者，你可以使用带有多个选项的`dracut`命令为特定的内核环境创建 initramfs。还有一个名为`/etc/dracut.conf`的配置文件，你可以使用它在重新创建 initramfs 时包含特定选项。dracut 的配置分布在不同的位置：

- `/usr/lib/dracut/conf.d/*.conf`包含系统默认配置文件。
- `/etc/dracut.conf`包含自定义的 dracut 文件。
- `/etc/dracut.conf`被用作主配置文件。

列表 19.1 显示了`dracut.conf`配置文件的示例。

```
[root@server1 ~]# cat /etc/dracut.conf
# 将你的配置写在这里或单独的文件 *.conf 中
# 在 /etc/dracut.conf
# 参见 man dracut.conf(5)
```

```
# Sample dracut 配置文件

#logfile=/var/log/dracut.log
#fileloglvl=6

# 要使用的 dracut 模块精确列表。此处未列出的模块将
# 不会被包含。如果你只想添加某些可选模块
# 请使用 add_dracutmodules 选项。
#dracutmodules+=""

# 要省略的 dracut 模块
#omit_dracutmodules=""

# 添加到默认的 dracut 模块
#add_dracutmodules+=""

# 添加到默认的额外内核模块
#add_drivers+=""

# 要包含在通用 initramfs 中的内核文件系统模块
#filesystems+=""

# 仅为启动当前硬件构建 initrd
#hostonly="yes"
#

# 安装本地的 /etc/mdadm.conf
#mdadmconf="no"

# 安装本地的 /etc/lvm.conf
#lvmconf="no"

# 要安装的 fsck 工具列表。如果没有指定，则使用硬编码的
# 默认，当前为："umount /sbin/fsck* xfs_db xfs_-
# check xfs_repair e2fsck jfs_fsck reiserfsck btrfsck"。安装是
# 机会性的，因此不存在的工具会被忽略。
#fscks=""
```

```
# 禁止安装任何 fsck 工具
#nofscks="yes"

# 默认挂载 / 和 /usr 为只读
#ro_mnt="no"

# 设置临时文件的目录
# 默认: /var/tmp
#tmpdir=/tmp
```

> 提示：根据 Red Hat 的目标，你在考试中不应该需要处理救援盘。然而，作为一名 RHCSA 也是一名 RHCE，你应该预料意之外的情况，因此确保你能够处理常见以及较少见的故障排除场景是一个好主意。

## 修复常见问题

在像这样简短的章节中，不可能考虑到在处理 Linux 时可能遇到的所有可能问题。不过，某些问题比其他问题更容易发生。在这一节中，你将学习一些更常见的问题。

## 重装 GRUB 2

引导加载程序代码不会无故消失，但偶尔会发生 GRUB 2 引导代码损坏。在这种情况下，你最好知道如何重装 GRUB 2。具体方法取决于你的服务器是否仍处于可启动状态。如果是，重装 GRUB 2 相当简单。只需输入`grub-install`后跟你想要安装的设备名称。该命令有许多不同选项可以微调具体安装的内容，但你不需要它们，因为默认情况下，该命令会安装让你的系统再次启动所需的所有内容。
