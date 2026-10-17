
将 `ftype` 替换为文件系统类型（`ext2`, `ext3`, `reiserfs`, `nfs`, `iso960`, `udf`）。将 `datasource` 替换为设备（`/dev/hda1`, `/sda1` 等）。将 `mountpoint` 替换为它在文件系统中出现的位置。常用选项包括：

- `ro`：指定文件系统应以只读模式挂载。
- `umask=0000`：用于 FAT32 文件系统，允许所有用户读写。

## 命令行系统管理

在 `mount` 命令中可以找到额外的选项。

为了说明，如果你想挂载上一页在 `/dev/sdb1` 上创建的 `ext2` 文件系统，你首先创建 `/publicspace`，然后提供所有三个参数执行 `mount` 命令：

```
root@workstation20]# mkdir /publicspace

root@workstation20]# mount -t ext2 /dev/sdb1 /publicspace

root@workstation20]#
```

通过读取或写 `/publicspace` 中的文件或目录，可以访问或修改 `/dev/sdb1` 设备的内容。通过不带参数输入 `mount` 命令来验证你是否打印出已挂载文件系统的列表：

```
root@workstation20]# mount

/dev/sda2 / type ext3 (rw)

none on /proc type proc (rw)

usbdevfs on /proc/bus/usb type usbdevfs (rw)

/dev/sda1 / type ext3 (rw)

none on /dev/pts type devpts (rw,gid=5,mode=620)

none on /dev type tmpfs (rw)

/dev/sdb1 /publicspace type ext2 (rw)

root@workstation20]#
```

## 第 18 小节

你可以使用 `umount` 命令卸载已挂载的文件系统。`umount` 命令只需要一个参数：要卸载的设备或资源的名称，或者是挂载该设备或资源的挂载点名称。例如，考虑到我们在本节中发出的 `mount` 命令，以下两个 `mount` 命令是等价的：

```
umount /dev/sdb1

umount /publicspace
```

卸载设备或资源后，你可以使用不带参数的 `mount` 或 `df` 命令来验证它是否不再出现在已挂载的文件系统中。

![](img/486a8c2356942c74dbc4de3c2f5d0f4e_470_0.png)

## 什么是设备忙（Device Busy）错误？

如果你在尝试卸载文件系统时收到“device busy”（设备忙）错误，这意味着意味着某些进程或某个用户的当前工作目录仍位于该系统中，或者某些进程仍在使用存储在该文件系统上的某个文件。在用户或进程更改当前工作目录或关闭打开的文件之前，你将无法卸载该文件系统。

## 维护 /etc/fstab 文件

`/etc/fstab` 文件是一个设备、资源、文件类型和挂载点的列表，控制文件系统在计算机启动时如何挂载。该文件还列出了哪些文件系统是普通用户挂载和卸载的。`/etc/fstab` 文件中的每一行代表一个已挂载或未挂载的文件系统，每行的格式如下：

```
device mountpoint ftype option1,option2... dump fscklvl
```

该文件中的每个字段都在表 18.4 中进行了描述。

### 表 18.4 /etc/fstab 文件中的字段

| 字段 | 说明 |
| --- | --- |
| device | 包含此行所属文件系统的设备或资源名称。 |
| mountpoint | 文件系统在本地文件系统树中挂载的位置。 |
| ftype | 文件系统类型，通常为 `vfat`（用于 Windows 设备）、`nfs`（用于网络文件系统）、`ext2`、`ext3`、`reiserfs`、`iso9660` 或 `udf`。 |

## 命令行系统管理

### 表 18.4 续

| 字段 | 说明 |
|---|---|
| options | 逗号分隔的选项列表，如 `mount` 手页中所列出的。常用选项包括 `user` 和 `owner`（允许普通用户挂载和卸载设备）、`noauto`（防止设备在启动时自动挂载）以及 `defaults`（意味着不使用特殊选项）。 |
| dump | 此文件系统是否由 `dump` 命令备份。这是已过时的 Unix 遗留；从 Linux 2.4 版本开始，`dump` 命令已过时，因此它应始终设置为 0。 |
| fsck | 对于根文件系统以外的所有文件系统，此项应设置为 2。根文件系统应设置为 1。不需要检查的文件系统（如 `reiserfs` 或 `iso9660`）可以设置为 0。如果不确定，此文件文件应包含值 2。 |

如果你想让像上一节中创建的文件系统在系统启动时自动挂载，请向 `/etc/fstab` 文件的底部添加一个包含设备、挂载点、文件系统类型和其他信息的条目。按照我们在上一节中创建的示例文件系统，添加以下行：

```
/dev/sdb1 /publicspace ext2 defaults 0 2
```

通过编辑 `/etc/fstab` 文件，你可以让 Linux 在启动时自动挂载添加的存储设备或网络文件系统。你还可以添加额外的可移动设备，以便用户根据需要挂载和卸载它们。

有关 `/etc/fstab` 文件或其中可用选项的进一步文档，请参阅 `fstab(5)` 和 `mount` 的手册页。

## 管理账户

如果你运行的是多用户 Linux 系统，或者是一个许多具有远程登录权限的网络 Linux 系统，那么添加和删除用户及组对作为系统管理员来说至关重要。在第 4 小节“在控制台导航 Linux”中，你学习了用户、组和权限。现在你将学习如何创建权限生效的用户和组账户。

在命令行添加或删除用户和组的过程非常简单；任务可以通过 `adduser`、`grouppadd`、`usermod` 和 `groupdel` 命令完成。

### 添加和删除用户账户

每当你想让新用户通过其自己的文件和登录信息访问你的 Linux 系统时，你就需要在系统中添加一个用户账户。这通过两个步骤完成：

- 1. 调用存储在 `/usr/sbin` 中的 `adduser` 命令，将要创建的账户名称作为参数提供，并可选 `-c "Name"` 选项提供用户的真实姓名（该名称会被电子邮件程序使用）。
- 2. 调用 `passwd` 命令，将你刚刚创建的账户名称作为参数，为该账户分配密码。

例如，为名为 `joe` 的用户创建一个新账户，你调用 `adduser joe` 作为参数，然后调用 `passwd joe` 作为参数，并在提示时为 `joe` 输入密码：

```
[root@workstation20 you]# /usr/sbin/adduser -c "Joe Brady" joe

[root@workstation20 you]# passwd joe

Changing password for user.

New password:

Retype password:

passwd: all tokens updated.

[root@workstation20 you]#
```

为 `joe` 创建账户后，他可以使用配置的密码登录。他的家目录已创建：`/home/joe`。

要删除用户账户，使用位于 `/usr/sbin` 的 `userdel` 命令，将要删除的账户名称作为参数，如果想删除家目录，则可选 `-r` 选项。

```
[root@workstation20 you]# /usr/sbin/userdel joe

[root@workstation20 you]#
```
账户已从系统中不可恢复地删除。

## 命令行系统管理

### 删除账户要小心

如果你想删除某个账户但不确定是哪一个，可以通过显示 `/etc/passwd` 文件来获取系统中存在的账户列表，该文件每行一个账户。

但是，不要删除任何小于 500 的账户，因为小于 500 的账户属于系统服务。

### 添加和删除组

组使用户相互关联、协作项目或访问非组用户无法访问的特定设施或设备。要创建组，使用存储在 `/usr/sbin` 中的 `groupadd` 命令，将组名作为参数提供。按如下方式将名称作为参数传递 `groupadd`：

```
[root@workstation20 you]# /usr/sbin/groupadd programmers

[root@workstation20 you]#
```
组已创建。

删除组的过程同样简单，通过存储在 `/usr/sbin` 中的 `groupdel` 命令完成。要删除组，调用 `groupdel` 并将要删除的组名作为参数提供：

```
[root@workstation20 you]# /usr/sbin/groupdel programmers

[root@workstation20 you]#
```
