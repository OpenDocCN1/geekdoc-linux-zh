
`umask` `0077`

`touch` `tempfile`

`ls` `-l` `tempfile`

`-rw------- 1 david users 0 Apr 19 11:21 tempfile`

更多信息请参阅 `bash` 的 `man` 页（帮助文档）。

要使用 `chmod` 设置特殊权限，请将数字相加并将它们放在第一列。例如，为了设置用户 ID（SUID）和设置组 ID（SGID），我们使用 `6` 作为第一列：

```bash
chmod 6755 /tmp/example
ls -l /tmp/example
-rws-sr-x 1 david users 0 Apr 19 11:21 /tmp/example
```

如果你对八进制值感到困惑，可以使用 `chmod` 的字母。权限组表示为：

| 所有者 (Owner) | `u` |
| :--- | :--- |
| 组 (Group) | `g` |
| 其他 (World) | `o` |
| 所有 (All) | `a` |

要执行上述操作，我们需要使用几条命令：

```bash
% chmod a+rx /tmp/example
% chmod u+w /tmp/example
% chmod ug+s /tmp/example
```

有些人更喜欢使用字母而不是数字。无论哪种方式的结果都是相同的权限。

八进制格式更快，也是你在 `shell` 脚本中最常用的格式。有时字母更强大。例如，在使用八进制格式时，没有简单的方法可以在保留文件其他组权限的同时更改其中一组权限。而使用字母则轻而易举。

```bash
% ls -l /tmp/
--rw-xr-x 1 alan users 0 Apr 19 11:21 /tmp/example0
--rw-xr-x 1 alan users 0 Apr 19 11:21 /tmp/example1
---r--r-- 1 alan users 0 Apr 19 11:21 /tmp/example2
% chmod g-w /tmp/example?
--rw-r--x 1 alan users 0 Apr 19 11:21 /tmp/example0
--rw------ 1 alan users 0 Apr 19 11:21 /tmp/example1
---r--r-- 1 alan users 0 Apr 19 11:21 /tmp/example2
```

我们在上面的多个地方提到了用户 ID 和设置组 ID 权限。你可能好奇这是什么。通常情况下，当你运行一个程序时，它是在你的用户账户下运行的。也就是说，它拥有你作为用户的所有的所有权限。组也是如此。当你运行一个程序时，它在你的当前程序下执行。通过 `set user ID`，你可以强制程序始终以程序所有者（如 `root`）的身份运行。`Set group ID` 相同，但是针对组的。

请小心这一点，`set user ID` 和 `set group ID` 程序可能会你的系统上留下巨大的安全漏洞。如果你经常设置由 `root` 拥有的 `user ID` 程序，你就允许任何人运行该程序并以 `root` 身份运行。`root` 在系统上没有任何限制，你可以看到这将如何导致重大的安全问题。简而言之，使用 `user ID` 和 `set group ID` 权限并不是坏事，只要运用常识即可。

## 9.3 链接

链接是文件之间的指针。通过链接，你可以让文件存在于许多位置并通过许多名称访问。链接有两种类型：硬链接（`hard links`）和软链接（`soft links`）。

硬链接是特定文件的名称。它们只能存在于单个系统中，并且当真实名称从系统中删除时，它们才会被删除。这些在某些情况下很有用，但许多用户发现软链接更通用。

软链接也称为符号链接（`symbolic link`），可以指向文件系统之外的文件。它实际上是一个包含所需信息的小文件。你可以添加和删除软链接而不会影响实际文件。由于符号链接实际上是一个包含自身信息的小文件，它甚至可以指向目录。例如，`/var/tmp` 实际上是 `/tmp` 的符号链接，这很常见。

链接没有自己的权限集或所有权，而是反映它们指向的文件的权限。`Slack` 主要使用软链接。这里有一个常见的例子：

```bash
$ ls -l /bin/sh
rwxrxr-x 1 root 4 Apr 6 12:34 /bin/sh -> bash
```

`Slack` 下的 `shell` 实际上是 `bash`。删除链接使用 `rm` 完成。`ln` 命令用于创建链接。这些命令将在第 10 章中进行深入讨论。

对软链接（`symlinks`）特别小心很重要。一次，我在一台机器上工作，该机器每晚上备份磁带一直失败。有两个链接被创建在彼此下方的目录中。

## 9.4 挂载设备

在 Linux 中，文件系统通常是被挂载到目录树中的某个位置。这个位置被称为挂载点（`mount point`）。要挂载设备，你需要使用 `mount` 命令。

挂载设备通常可以是硬盘分区、光盘、USB 驱动器或网络文件系统。在挂载设备之前，你可能需要配置一个挂载表，通常是 `/etc/stab`。这个文件告诉系统在启动时应该挂载哪些设备。

### fstab

让我们看看 `/etc/stab` 的一个示例：

```bash
/dev/sda / ext2 defaults 0 0
/dev/sda2 /usr/local ext2 defaults 0 0
/dev/sda3 /home ext2 defaults 0 0
/dev/sda4 /swap swap defaults 0 0
/dev/sdb1 /export ext2 defaults 0 0
/dev/sdb2 /pts devpts defaults 0 0
none /proc proc defaults 0 0
/dev/fd0 /mnt auto 0 0
/dev/cdrom /mnt/cdrom iso9600ro 0 0
```

第一列是设备名称。在这种情况下，文件系统是分区。第二列是挂载点。第三列是文件系统类型。第四列是选项。第五列和第六列是用于 `fsck` 检查的参数（对于交换 分区这些通常设为 0）。

### mount 和 umount

将另一个设备挂载到你的文件系统很容易。你只需要使用 `mount` 命令，以及一些选项。如果设备在 `/fstab` 文件中有条目，使用 `mount` 就会简化。例如，假设我想挂载我的光驱驱动器，并且我的 `fstab` 文件如前一节所示。我会这样挂载：

```bash
% mount -t iso9600 -o ro /dev/cdrom /mnt/cdrom
```

该命令包含了之前 `fstab` 示例中的相同信息，但我们将解释所有部分。`-t iso9600` 是要挂载设备的文件系统类型。在这种情况下，它是 `iso9600` 文件系统，这是光驱驱动器最常用的。`-o ro` 以只读模式挂载设备。`/dev/cdrom` 是要挂载设备名称，`/mnt/cdrom` 是文件系统中挂载该驱动器的位置。

在你需要移除当前挂载的软盘、光驱或其他可移动设备之前，你必须先卸载它。这是通过 `umount` 命令完成的。

不要问 'h' 去到哪里了，因为我们无法告诉你。你可以使用挂载的设备或挂载点作为 `umount` 的参数。例如，如果你想从上一个示例中卸载 CD-ROM，以下任一命令均有效：

```
# umount /dev/cdrom
# umount /cdrom
```
