
## 使用 mount 挂载分区

一旦分区已使用文件系统格式化，您必须在挂载它之后才能使用它。接下来，让我们回顾一下如何执行此操作。

Linux 与其他操作系统（如 Windows）之间的一个关键区别在于，您需要先挂载文件系统才能使用它。这是新手 Linux 管理员容易掉入的又一个“陷阱”。您甚至需要挂载 CD、DVD、软盘和 USB 驱动器才能使用它们！我们将在本章的后面部分讨论可移动介质的挂载。

好消息是，挂载分区的过程相对简单。这是通过使用 `mount` 命令完成的。`mount` 实用程序将分区挂载到文件系统中的现有目录。当您切换到该目录时，实际上您就切换到了该分区。

新晋的 Linux 管理员有时会对这个概念感到困惑。其他操作系统，如 Windows，默认使用驱动器字母（如 C: 或 D:）来引用磁盘上的分区。

例如，如果你在 Windows 系统中有一个硬盘，上面有两个分区，第一个分区将通过驱动器字母 C 访问。第二个分区将通过驱动器字母 D 访问。每个驱动器字母都有自己独立的文件和目录层次结构。

Linux 不是这样！相反，Linux 使用虚拟文件系统（VFS），创建一个包含系统中所有存储设备上所有分区的单一层次结构。切换到分区挂载所在的目录，你就切换到了该分区。

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_411_0.png)

> **注意** 较新版本的 Windows 也允许您将分区挂载在目录中。然而，在我看来，这远不如在 Linux 下操作的那样优雅。

要使用 `mount` 来挂载分区，首先使用 `su` 切换到根账户。然后在 shell 提示符下输入 `mount -t file_system_type device mount_point`。我知道这看起来很复杂，但其实并没有那么难。例如，假设你在系统第二个硬盘的第一个分区上创建了 ext4 文件系统，现在你想将其挂载到一个名为 /mnt/exaspace 的目录中。为此，你需要在 shell 提示符下输入 `mount -t ext4 /dev/sdb1 /mnt/exaspace`，如下所示：

```
ws1:~ # mount -t ext4 /dev/sdb1 /mnt/exaspace/
ws1:~ #
```

现在，每当你在文件系统中切换到 /mnt/exaspace 目录时，你就切换到了新的分区（/dev/sdb1）。如果你不知道分区使用的文件系统类型，你可以在 `mount` 命令中使用 `-a` 选项而不是 `-t`。这将使 `mount` 尝试使用所有支持的文件系统类型来挂载分区，直到其中一种成功为止。

在大多数发行版中，/mnt 目录是挂载本地和远程文件系统的默认目录。当然，你不必使用它。你可以将分区挂载到任何你想要的目录。但是，根据惯例，/mnt 用于此目的。

在一些发行版中，它也是挂载可移动设备的默认位置。其他发行版，如 OpenSUSE 和较新版本的 Fedora，使用 /media 作为挂载可移动介质的默认位置。

你还可以在 `mount` 命令中使用 -o 选项来包含各种挂载选项。例如，你可以使用 -ro 将分区以只读方式挂载。请参见 `mount` 的 man 页面以获取所有可用选项的完整列表。

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_412_0.png)

> **提示** 我喜欢 `mount` 命令的一点是，它可以用来在文件系统中挂载 ISO 镜像，从而允许你访问其中的文件，而无需先将其刻录到光盘上。语法是 mount -o loop filename.iso mount_point。

挂载分区后，你可以使用不带开关的 `mount` 命令查看所有已挂载的文件系统，如下所示：

```
ws1:~ # mount
/dev/sda3 on / type ext4 (rw, acl, user_xattr)
proc on /proc type proc (rw)
sysfs on /sys type sysfs (rw)
debugfs on /sys/kernel/debug type debugfs (rw)
devtmpfs on /dev type devtmpfs (rw, mode=0755)
tmpfs on /dev/shm type tmpfs (rw, mode=1777)
devpts /dev/pts type devpts (rw, mode=0620, gid=5)
/dev/sda1 /boot type ext4 (rw, acl, user_xattr)
/dev/sda4 /var type ext4 (rw, acl, user_xattr)
securityfs /sys/kernel/security type securityfs (rw)
none on /proc/fs/vmblock/mountPoint type vmblck (rw)
fusectl on /sys/fs/fuse/connections type fusectl (rw)
gvfs -fuse-daemon /home/tux/.gvfs type fuse. gvfs =fuse-daemon
(rw, nosuid, nodev, user-tux)
/dev/sdb1 /mnt/extraspace type ext4 (rw)
ws1:~ #
```

如果你查看 `mount` 输出的最后一行，你会发现 /dev/sdb1 已挂载在 /mnt/extraspace 上，并使用了 ext4 文件系统。

此外，每当你挂载或卸载分区时，/etc/mtab 文件都会更新为已挂载文件系统的列表。你还可以通过查看此文件来了解已挂载文件系统的列表，如下面的示例所示：

```
ws1:~ $ cat /etc/mtab
/dev/sda3 / ext4 rw, acl, user_xattr 0 0
proc /proc proc rw 0 0
sysfs /sys sysfs rw 0 0
debugfs /sys/kernel/debug debugfs rw 0 0
devtmpfs /dev devtmpfs rw, mode=0755 0 0
tmpfs /dev/shm tmpfs rw, mode=1777 0 0
devpts /dev/pts devpts rw, mode=0620, gid=5 0 0
/dev/sda1 /boot ext4 rw, acl, user_xattr 0 0
/dev/sda4 /var ext4 rw, acl, user_xattr 0 0
securityfs /sys/kernel/security securityfs rw 0 0
none /proc/fs/vmblock/mountPoint vmblck rw 0 0
fusectl /sys/fs/fuse/connections fusectl rw 0 0
gvfs -fuse-daemon /home/tux/.gvfs fuse. gvfs =fuse-daemon
rw, nosuid, nodev, user-tux 0 0
/dev/sdb1 /mnt/extraspace ext4 rw 0 0
ws1:~ $
```

> **注意** 你还可以查看 /proc/mounts 以获取已挂载文件系统的列表。另一个用于查看已挂载分区的有用实用程序是 `df`。此实用程序显示你的分区、挂载位置、已使用空间以及剩余可用空间。

如果出于某种原因，你需要卸载分区，可以使用 `umount` 命令。要卸载分区，只需输入 `umount` 后跟设备或分区的挂载目录。例如，要卸载上一个示例中显示的 /dev/sdb1 分区，你可以输入 `umount /dev/sdb1` 或 `umount /mnt/extraspace`，如下所示：

```
ws1:~# umount /dev/sdb1
```

> **提示** 请注意，该命令是 "umount"，而不是 "unmount"。这是另一个 Linux 陷阱！

这引发了在 Linux 上工作的另一个问题。仅因为你使用 `mount` 挂载了文件系统，并不意味着系统重启后它会保持挂载状态。只要系统保持运行，分区就会保持挂载状态。然而，如果你重启，系统重新启动时分区不会重新挂载。

你可以使用 /etc/fstab 文件来解决这个问题。此文件包含操作系统每次启动时挂载的文件系统列表。典型的 /etc/fstab 文件如下：

```
ws1:~$ cat /etc/fstab
/dev/sda2          swap           swap          defaults                  0 0
/dev/sda3          /boot          ext4          acl,user_xattr            1 1
/dev/sda1          /              ext4          acl,user_xattr            1 2
/dev/sda4          /var           ext4          acl,user_xattr            1 2
proc               /proc          proc          defaults                  0 0
sysfs              /sys           sysfs         noauto                    0 0
debugfs            /sys/kernel/debug debugfs    noauto                    0 0
devpts             /dev/pts       devpts        mode=0620,gid=5           0 0
ws1:~$
```

我知道这个文件一开始看起来有点令人困惑，但实际上并不太难。/etc/fstab 文件中的每一行都指定在启动时要挂载的独立文件系统。每一行由六个字段组成，如表 10-1 所示。

请注意，我们之前创建的 /dev/sdb1 分区并未列在示例 fstab 文件中。这意味着系统重启后，它不会挂载在 /mnt/extraspace。我们可以通过将该分区添加到 fstab 文件来修复此问题。使用编辑器（如 vi）打开 /etc/fstab，然后添加以下行：

```
/dev/sdb1  /mnt/extraspace  ext4  acl,user_xattr  1  2
```

这指定使用 ext4 文件系统将 /dev/sdb1 分区挂载在 /mnt/extraspace。它还指定为该文件系统启用访问控制列表（这是一件非常好的事情！），并为该文件系统启用扩展用户属性。现在，每次重启系统时，分区都会自动挂载。

