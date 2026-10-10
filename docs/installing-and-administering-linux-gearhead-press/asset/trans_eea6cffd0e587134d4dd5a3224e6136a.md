

## 示例 4.12 使用 stat 获取 inode 和时间戳信息

为了获取其主目录中特定（即*已过期*）子目录的 inode 信息，唐·吉诃德输入

```
$ stat expired<Enter>
File: "expired"
Size: 4096 Blocks: 8 Directory
Access: (0775/drwxrwxr-x) Uid: ( 501/ quixote) Gid: ( 607/ knights01)
Device: 306 Inode: 109096 Links: 5
Access: Wed Jul 12 18:13:21 2001
Modify: Mon Jul 10 13:22:17 2001
Change: Mon Jul 10 13:22:17 2001
```

在示例 4.12 中显示的 stat 结果中，让我们看看 Access、Modify 和 Change 这几行：

- **Access** 表示文件已被读取或写入，并告诉我们最后一次发生这些操作的时间和日期。当文件被读取但未对其做出更改时，访问时间会发生改变，但修改时间或更改时间不会改变。
- **Modify** 指示文件或目录的内容已发生变化，并指示最后一次发生这种情况的时间和日期。
- **Change** 告诉我们 inode 信息已发生变化，并指示最后一次发生这种情况的时间和日期。

此时，正如我们在示例 4.5 中之前提到的，唐·吉诃德删除了 *expired* 和 *misc* 目录及其内容。图 4.4 展示了唐·吉诃德在 RFI 目录中的部分现在看起来的样子。

## 软盘的格式化和访问

许多用户，特别是新用户或前 DOS 和前 Windows 用户，不知道他们可以在 Linux/UNIX 中使用软盘。虽然我们中的许多人都在大型网络上使用 UNIX 类型的系统，并在不同程度上放弃了“跑腿传输”（sneaker netting），但大多数甚至所有用户仍然时不时地需要它。在本节中，我们将在一张软盘上创建类似 Linux 的 ext2 文件系统，在另一张软盘上创建 DOS 文件系统。

![](img/cae5c706c216875d12d4b7d28144cc71_134_0.png)

图 4.4 唐·吉诃德的 RFI 目录结构部分。

### 带有 ext2 文件系统的软盘

你可以以 Linux 支持的六种文件系统类型中的任意多种方式在软盘上创建和操纵文件。本部分描述的 ext2 文件系统程序应用于在两个类似 Linux 的系统之间移动软盘时。

我们将从一开始格式化一张软盘。将软盘插入你的软盘驱动器。以下程序可以作为 root 用户或普通用户完成。让我们作为普通用户来执行。因此，将软盘放入软盘驱动器中后，输入

```
$ fdformat /dev/fd0H1440<Enter>
```

你必须指定软盘在设备 /dev/fd0 中；也就是说，在第一个软盘驱动器中。（如果它在第二个软盘驱动器中，你必须指定 /dev/fd1。）你输入 H1440（在此规范和 /dev/fd0 设备名称之间没有空格）以告诉系统 /dev/fd0 包含一个容量为 1.44MB 的 3.5 英寸高密度软盘。如果你的软盘是其他类型，请查阅 fdformat 手册页以获取适当的描述。

当系统执行 fdformat 命令时，它响应以

```
Double-sided, 80 tracks, 18 sec/track. Total capacity 1440 kB.
Formatting . . . (counts to 80) done
Verifying . . . (also counts to 80) done
```

现在软盘已经格式化完毕，下一步是在其上创建文件系统。Linux 支持大约十几种你只能在软盘上创建的文件系统类型。在这个第一个程序中，我们将创建一个 ext2 文件系统，以与在 Linux 安装期间在硬盘上创建的 ext2 文件系统兼容。继续作为普通用户，输入

```
$ /sbin/mkfs -t ext2 /dev/fd0<Enter>
```

普通用户应使用 /sbin/mkfs 作为命令，因为目录 /sbin 可能不在他们的 $PATH 中。如果你作为 root 用户执行此任务，你只需要输入 mkfs 作为命令，因为 /sbin 已经在 root 的 $PATH 环境变量中。

-t 选项表明用户即将告诉系统要在软盘上安装什么类型的文件系统。该选项后跟参数 ext2，它是默认的 Linux 文件系统类型。输入命令后，系统会执行它并响应以

```
mke2fs 1.19, 13-Jul-2000 for EXT2 FS 0.5b, 95/08/09
Linux ext2 filesystem format
Filesystem label:
OS Type: Linux
Block size = 1024 (log=0)
Fragment size = 1024 (log=0)
184 inodes, 1440 blocks
72 blocks (5.00%) reserved for the super user
First data block=1
1 block group
8192 blocks per group, 8192 fragments per group
184 inodes per group
Writing inode tables: done
Writing superblocks and filesystem accounting information: done
```

简而言之，系统告诉你它已经完成了软盘的格式化，现在等待进一步指示。（对于输出的解释，这超出了本书的范围，请查阅第 15 章“Linux 文档和支持”中提到的信息源之一。）

下一步是挂载文件系统，这意味着必须告诉系统使新定义的文件系统（在这种情况下是新格式化的软盘）成为其树状文件层次结构的一部分。作为 root 用户输入下一个命令，因为普通用户在尝试时会失望。他们只会得到 mount : only root can do that 错误消息。那么，以下是命令：

```
# mount -t ext2 /dev/fd0 /mnt/floppy<Enter>
```

> 注意 最好且最轻松地作为 root 或超级用户执行此任务（挂载文件系统）。出于安全原因，不允许普通用户挂载或卸载文件系统。然而，普通用户可以通过使用 mtools 来绕过此限制，我们将在第 5 章中讨论。

mount 命令告诉系统将位于 /dev/fd0 上的 ext2 文件系统作为总文件系统的一部分，并将新添加的文件系统称为 /mnt/floppy（即，称为 /floppy 的子目录位于称为 /mnt 的子目录中，都是根目录的一部分）。你可以给它起其他名称，但这个名称是 Linux 约定。如果你正确输入了所有内容，系统将照你命令行事，并响应以另一个 root 提示符。

为了查看到目前为止发生了什么，输入以下行：

```
# ls -la /mnt/floppy<Enter>
```

系统响应以

```
total 14

drwxr-xr-x 3 username username 1024 Apr 28 16:36 .

drwxr-xr-x 4 root root 1024 Jan 31 11:31 ..

drwxr-xr-x 2 root root 12288 Apr 28 16:36 lost+found
```

系统已经将软盘上最大的子目录命名为 **lost+found**。如果你愿意，你可以更改其名称。还要注意，单点特殊文件的所有权已分配给 username，因为我们是以普通用户身份开始该程序的。如果我们以 root 用户身份完成了整个程序，那么单点文件的所有权将是 root root。

现在你准备好使用 Linux 命令将软盘作为文件系统的一部分使用。

当你使用完软盘并希望将其取出时，请记住你不能立即“弹出”软盘。首先，你必须从总文件系统中卸载软盘的文件系统（再次，作为 root 用户）。为此，输入

```
# umount /mnt/floppy<Enter>
```

或

```
# umount /dev/fd0<Enter>
```

注意命令是 **umount**，而不是“unmount”。同样，你必须是一个 root 用户才能卸载文件系统，正如你必须是一个 root 用户才能挂载它一样。此外，你不能从软盘本身的文件目录中卸载；你必须 cd 出去。否则，你会得到 device busy 错误消息。

现在，你可以移除软盘了。当你想要再次使用它时，你必须重新输入 *mount* 语句以让 Linux 再次识别它。但你不需要编辑 /etc/fstab 文件，因为这些规格设置仍然存在。

### DOS 文件系统

在上一节中，我们格式化了一张软盘以兼容类似 Linux 的 ext2 文件系统。然而，要在 Linux 系统和 DOS 文件系统之间进行“跑腿传输”，你使用的命令类似于前文讨论的命令，但有所不同。我们将再次从格式化软盘开始。

