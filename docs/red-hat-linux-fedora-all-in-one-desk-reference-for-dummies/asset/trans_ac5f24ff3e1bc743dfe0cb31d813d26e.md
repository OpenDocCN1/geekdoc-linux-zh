
The first command turns off all permissions for everyone, and the second command turns on the read and write permissions for the owner (you). Type ls -l to verify that the change took place (you should see a permission setting of -rw------). Here's a sample output from ls -l:

```
-rw------ 1 naba naba 3 Jun 30 18:45 mystuff
```

Note the third and fourth fields that show naba naba. These two fields show the file's user and group ownership. In this case, the name of the user is naba and the name of the group is naba as well (because Red Hat Linux creates a group for each user).

Sometimes you have to change a file's user or group ownership for everything to work correctly. For example, suppose you are instructed (by a manual, what else) to create a directory named cups and give it the ownership of user ID lp and group ID sys. How would you do it?

Well, you can log in as root and create the directory with the command mkdir:

```
mkdir cups
```

If you check the file's details with the ls -l command, you see that the user and group ownership is root root.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_198_0.png)

To change the owner, use the chown command. For example, to change the ownership of the cups directory to user ID lp and group ID sys, type

```
chown lp.sys cups
```

## Commands for working with files

要从一个目录复制文件到另一个目录，请使用 cp 命令。例如，要将文件 /usr/X11R6/lib/X11/xinit/Xclients 复制到当前目录（例如你的主目录）中的 Xclients.sample 文件，请输入以下内容：

```
cp /usr/X11R6/lib/X11/xinit/Xclients Xclients.sample
```

如果要将文件复制到当前目录但保留原始名称，请将句点（.）用作 cp 命令的第二个参数。因此，以下命令将 /etc/X11 目录中的 XF86Config 文件复制到当前目录（用单个句点表示）：

```
cp /etc/X11/XF86Config .
```

cp 命令会制作文件的新副本并保留原文件不变。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_199_0.png)

如果要将目录的全部内容（包括所有子目录及其内容）复制到另一个目录，请使用命令 cp -ar sourcedir destdir（这会将 sourcedir 目录下的所有内容复制到 destdir）。例如，要将 /etc/X11 目录中的所有文件复制到当前目录，请输入以下命令：

```
cp -ar /etc/X11 .
```

![](img/a7eec43a54473e95dc5ea333fecf1bd7_199_1.png)

要将文件移动到新位置，请使用 mv 命令。原始副本将被删除，目标位置会出现新副本。你可以使用 mv 重命名文件。如果要将 today.list 的名称更改为 old.list，请按如下方式使用 mv 命令：

```
mv today.list old.list
```

另一方面，如果要将 today.list 文件移动到名为 saved 的子目录，请使用此命令：

```
mv today.list saved
```

mv 的一个有趣功能是，你可以使用它将整个目录（连同其所有子目录和文件）移动到新位置。如果有一个名为 data 的目录包含许多文件和子目录，你可以使用以下命令将整个目录结构移动到 old_data：

```
mv data old_data
```

要删除文件，请使用 rm 命令。例如，要删除名为 old.list 的文件，请输入以下命令：

```
rm old.list
```

![](img/a7eec43a54473e95dc5ea333fecf1bd7_199_2.png)

请小心使用 rm 命令——尤其是在以 root 身份登录时。使用 rm 很容易无意中删除重要文件。

## Commands for working with directories

为了在主目录中组织文件，你必须创建新目录。使用 mkdir 命令创建目录。例如，要在当前目录中创建名为 images 的目录，请输入以下内容：

```
mkdir images
```

创建目录后，你可以使用 cd images 命令切换到该目录。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_200_0.png)

你可以使用 mkdir 命令的 -p 选项创建整个目录树。例如，假设你的系统有 /usr/src 目录，你想创建目录树 /usr/src/book/java/examples/applets。要创建此目录层次结构，请输入以下命令：

```
mkdir -p /usr/src/book/java/examples/applets
```

![](img/a7eec43a54473e95dc5ea333fecf1bd7_200_1.png)

当你不再需要目录时，请使用 rmdir 命令删除它。

你只能在目录为空时删除目录。

要删除空目录树，可以使用 -p 选项，如下所示：

```
rmdir -p /usr/src/book/java/examples/applets
```

此命令会删除 applets 的空父目录。命令在遇到非空目录时停止。

## Commands for finding files

find 命令对于查找符合搜索条件的 文件（和目录）非常有用。

当我多年前开始使用 UNIX（20 世纪 80 年代初的 Berkeley UNIX）时，find 命令让我困惑。我很长时间都只使用一种基本的 find 语法，然后才逐渐使用更复杂的语法。我最初学到的基本语法是用于在整个文件系统中查找文件。方法如下：假设你想查找名称以 gnome 开头的任何文件或目录。输入以下 find 命令来查找这些文件：

```
find / -name "gnome*" -print
```

如果未以 root 身份登录，你可能会收到一堆错误消息。如果这些错误消息让你烦恼，只需按如下方式修改命令，错误消息就会成为历史（或者，正如 UNIX 爱好者所说，将它们发送到位桶）：

```
find / -name "gnome*" -print 2> /dev/null
```

此命令告诉 find 从根目录（/）开始查找，查找与 gnome* 匹配的文件名，并显示任何匹配文件的完整路径名。最后一部分（2> /dev/null）只是将错误消息发送到一个特殊文件，这相当于直接忽略它们。

你可以使用这种简单形式的 find 的变体来定位任何目录（以及该目录包含的任何子目录）中的文件。如果你忘记了在主目录中存储了所有名为 report*（名称以 report 开头）的文件的位置，可以使用以下命令搜索文件：

```
find ~ -name "report*" -print
```

当你熟悉这种 find 语法后，就可以使用 find 的其他选项。例如，要仅查找特定类型的文件（如目录），请使用 type 选项。以下命令显示 Linux 系统中的所有顶级目录名称：

```
find / -type d -maxdepth 1 -print
```

在典型的 Linux 系统中，你可能不需要使用 find 的复杂形式——但如果需要，你可以使用以下命令查找其余的 find 选项：

```
man find
```

## Commands for mounting and unmounting

假设你想在文本控制台登录时（没有 GUI 帮助你）访问本书附带的 DVD 上的文件。为此，你必须先将 DVD 驱动器的文件系统挂载到 Red Hat Linux 文件系统中的特定目录上。

以 root 身份登录（或输入 su - 成为 root），将 DVD 插入 DVD 驱动器，然后输入以下命令：

```
mount /dev/cdrom /mnt/cdrom
```

此命令将名为 /dev/cdrom 的设备（指 CD-ROM 以及 DVD-ROM 驱动器）上的文件系统挂载到 Linux 文件系统中的 /mnt/cdrom 目录（也称为挂载点）上。

mount 命令成功完成后，你可以通过将 /mnt/cdrom 目录视为光盘的顶级目录来访问 DVD 上的文件。换句话说，要查看 DVD 的内容，请输入

```
ls -F /mnt/cdrom
```

使用完 DVD 后——并且在从驱动器弹出之前——你必须使用以下 umount 命令“卸载”光盘驱动器：

```
umount /dev/cdrom
```

通常在 /mnt 目录中的目录上挂载设备。Red Hat Linux 附带两个预定义目录：/mnt/cdrom 用于挂载 DVD，/mnt/floppy 用于挂载软盘驱动器。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_202_0.png)

## Commands for checking disk-space usage

我想告诉你两个命令——df 和 du——你可以用它们来检查系统的磁盘空间使用情况。这些命令使用简单。df 命令显示所有已挂载设备的磁盘空间使用情况摘要，如以下示例所示：

```
df
```

| 文件系统 | 1K-块 | 已用 | 可用 | 使用% | 挂载点 |
|------------|-----------|------|-----------|------|------------|
| /dev/hda5 | 7392428 | 3583420 | 3433492 | 52% | / |
| /dev/hda3 | 101107 | 9322 | 8656 | 10% | /boot |
| none | 127376 | 0 | 127376 | 0% | /dev/shm |
| /dev/cdrom | 658144 | 658144 | 0 | 100% | /mnt/cdrom |

输出是一个表格，显示设备、存储总千字节、使用量、可用量、使用百分比和挂载点。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_202_1.png)

要以更易读的格式查看 df 的输出，请输入 df -h。以下是 df -h 命令的输出：

```
df -h
```

| 文件系统 | 大小 | 已用 | 可用 | 使用% | 挂载点 |
|------------|------|------|-------|------|------------|
| /dev/hda5 | 7.1G | 3.5G | 3.3G | 52% | / |
| /dev/hda3 | 99M | 9.2M | 85M | 10% | /boot |
| none | 125M | 0 | 125M | 0% | /dev/shm |
| /dev/cdrom | 643M | 643M | 0 | 100% | /mnt/cdrom |

如果你将此输出与普通 df 的输出（见上一个列表）进行比较，你会看到 df -h 使用 M 表示兆字节、G 表示千兆字节等术语打印大小。这显然比 1K-blocks 更容易理解。

另一个命令——du——对于查找目录占用多少空间很有用。例如，输入以下命令来查看
