
The -t vfat part of the mount command specifies that the device you mount — /dev/hda1 — has an MS-DOS file system. Figure 3-4 illustrates the effect of this mount command.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_482_0.png)

图 3-4：
以下是如何在 /dosc 目录上挂载 DOS 分区的。

图 3-4 显示了 DOS 分区中的目录如何映射到 Linux 文件系统。在 DOS 下的 C:\DOS 目录在 Red Hat Linux 下变为 /dosc/dos。同样，C:\WINDOWS 现在是 /dosc/windows。你可能已经看出规律了。要将 DOS 文件名转换为 Linux（当你将 DOS 分区挂载到 /dosc 时），请执行以下步骤：

- 1. 将 DOS 名称改为小写。
- 2. 将 C:\ 更改为 /dosc/。
- 3. 将所有反斜杠（\）更改为斜杠（/）。

## 挂载 DOS 软盘

就像你在 Red Hat Linux 文件系统上挂载 DOS 硬盘分区一样，你也可以挂载 DOS 软盘。你必须以 root 身份登录才能挂载软盘，但你可以按照本节后半部分所示的步骤设置系统，以便任何用户都可以挂载 DOS 软盘。你还需要知道软盘驱动器的设备名称。默认情况下，Linux 定义了以下两个通用软盘设备名称：

- `/dev/fd0` 是 A 驱动器（第一个软盘驱动器）
- `/dev/fd1` 是 B 驱动器（第二个软盘驱动器，如果你有的话）

关于挂载点，你可以使用文件系统中的任何空目录作为挂载点，但 Red Hat Linux 系统自带一个目录 /mnt/floppy，专门用于挂载软盘。

要将 DOS 软盘挂载到 /mnt/floppy 目录，请将软盘放入驱动器并输入以下命令：

```
mount -t vfat /dev/fd0 /mnt/floppy
```

挂载软盘后，你可以使用 Linux 复制命令（cp）向软盘复制文件或从软盘复制文件。要将当前目录中的文件 gnome1.pcx 复制到软盘，请输入以下内容：

```
cp gnome1.pcx /mnt/floppy
```

同样，要查看软盘的内容，请输入以下内容：

```
ls /mnt/floppy
```

如果你想从驱动器中取出软盘，请先卸载软盘驱动器。卸载会移除软盘文件系统与 Red Hat Linux 文件系统上的挂载点之间的关联。使用 umount 命令像这样卸载软盘：

```
umount /dev/fd0
```

![](img/a7eec43a54473e95dc5ea333fecf1bd7_483_0.png)

你可以设置 Red Hat Linux 系统，使任何用户都可以挂载 DOS 软盘。例如，要允许任何用户将 A 驱动器中的 DOS 软盘挂载到 /a 目录，请执行以下步骤：

- 1. **以 root 身份登录。**
- 2. **通过在终端窗口中输入以下命令创建 /a 目录（挂载点）：**
  `mkdir /a`
- 3. **在文本编辑器（如 vi 或 Emacs）中编辑 /etc/fstab 文件，插入以下行，然后保存文件并退出编辑器：**
  `/dev/fd0   /a   vfat   noauto,user   0 0`

该行中的第一个字段是软盘驱动器的设备名称（/dev/fd0）；第二个字段是挂载目录（/a）；第三个字段显示文件系统的类型（vfat）。user 选项（出现在 noauto 旁边）使所有用户能够挂载 DOS 软盘。

4. 注销并以普通用户身份登录。

5. 为确认你能以普通用户而不仅仅是以 root 挂载 DOS 软盘，请将 DOS 软盘插入 A 驱动器并输入以下命令：

```
mount /a
```

挂载操作应成功，并且当你输入命令 ls /a 时，你应该能看到 DOS 软盘的列表。

6. 要卸载 DOS 软盘，请输入 umount /a。

## 使用 mtools

访问 MS-DOS 文件系统的一种方法是使用 mount 命令挂载 DOS 硬盘或软盘，然后使用常规 Linux 命令（如 ls 和 cp）来操作已挂载的 DOS 文件系统。这种挂载 DOS 文件系统的方法对于硬盘来说是可以的。Linux 可以在启动时自动挂载 DOS 分区，并且你可以在任何时候访问硬盘上的 DOS 目录。

然而，如果你想要 DOS 软盘的快速目录列表，挂载很快就会变得相当繁琐。首先，你必须挂载软盘驱动器。然后你必须使用 ls 命令。最后，在弹出软盘之前你必须使用 umount 命令。

这就是 mtools 包派上用场的地方。mtools 包实现了大多数常见的 DOS 命令；命令使用与 DOS 相同的名称，只是每个命令前加上 m 前缀。因此，获取目录列表的命令是 mdir，而 mcopy 用于复制文件。mtools 最好的地方在于，你不必挂载软盘就可以使用 mtools 命令。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_484_0.png)

因为 mtools 命令会读写物理设备（软盘），所以你必须以 root 身份登录才能执行这些命令。如果你希望任何用户都能访问 mtools 命令，你必须更改软盘驱动器设备的权限设置。使用以下命令允许任何人读取和写入第一个软盘驱动器：

```
chmod o+rw /dev/fd0
```

## 尝试 mtools

要尝试 mtools，请按照以下步骤操作：

- 1. **以 root 身份登录或输入 su - 然后输入 root 密码。**
- 2. **将 MS-DOS 软盘放入系统 A 驱动器中。**
- 3. **输入 mdir。**
  你应该会看到软盘的目录（以标准 DOS 目录列表格式显示）。

通常，你会使用 mtools 实用程序来访问软盘。默认配置文件 /etc/mtools.conf 设置为将软盘驱动器作为 A 驱动器访问。虽然你可以编辑该文件为 DOS 硬盘分区定义 C 和 D 驱动器，但你也可以使用 Linux mount 命令挂载它们来访问硬盘分区。因为你可以在启动时自动挂载硬盘分区，所以通过 Linux 命令访问它们通常同样容易。

你也可以通过 mtools 访问 Iomega Zip 驱动器。只需指定一个驱动器字母和相应设备的 filename 即可。对于内置 IDE（ATAPI）Zip 驱动器，请尝试使用 /dev/hdd4 作为设备文件，并在 /etc/mtools.conf 文件中添加以下行：

```
drive e: file="/dev/hdd4"
```

之后你应该能够使用 mtools 命令访问 Zip 驱动器（将其称为 E 驱动器）。例如，要查看目录列表，请将 Zip 磁盘放入 Zip 驱动器并输入：

```
mdir e:
```

## 学习 mtools 命令

mtools 包是一组实用程序的集合。到目前为止，我一直在使用 mdir——它是 DOS 中 DIR 命令的 mtools 对应项。其他 mtools 命令也相当容易使用。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_485_0.png)

如果你熟悉 MS-DOS 命令，使用 mtools 命令就很简单。将 DOS 命令以小写字母输入，并记得在每个命令前加上 m。因为 Linux 命令和文件名区分大小写，所以在输入 mtools 命令时必须全部使用小写字母。

表 3-4 总结了 mtools 中可用的命令。

### 表 3-4 mtools 命令

| mtools 实用程序 | MS-DOS 命令（如果有） | mtools 实用程序的功能 |
|---|---|---|
| mattrib | ATTRIB | 更改 MS-DOS 文件属性标志 |
| mbadblocks |  | 测试软盘并在文件分配表（FAT）中标记坏块 |
| mcd | CD | 更改 MS-DOS 目录 |
| mcopy | COPY | 在 MS-DOS 和 Linux 之间复制文件 |
| mdel | DEL or ERASE | 删除 MS-DOS 文件 |
| mdeltree | DELTREE | 递归删除 MS-DOS 目录 |
| mdir | DIR | 显示 MS-DOS 目录列表 |
| mdu |  | 列出目录及其内容占用的空间 |
| mformat | FORMAT | 在低级格式化的软盘上放置 MS-DOS 文件系统。（在 Red Hat Linux 中使用 fdformat 对软盘进行低级格式化。） |
| minfo |  | 获取有关 MS-DOS 文件系统的信息 |
| mkmanifest |  | 制作短名称等效列表 |
| mlabel | LABEL | 初始化 MS-DOS 卷标 |
| mmd | MD or MKDIR | 创建 MS-DOS 目录 |
| mmove |  | 移动或重命名 MS-DOS 文件或子目录 |
| mmount |  | 挂载 MS-DOS 磁盘 |
| mpartition |  | 创建 MS-DOS 文件系统作为分区 |
| mrd | RD or RMDIR | 删除 MS-DOS 目录 |
| mren | REN or RENAME | 重命名现有 MS-DOS 文件 |
| mshowfat |  | 显示 MS-DOS 文件的 FAT 条目 |
| mtoolstest |  | 测试并显示当前 mtools 配置 |
| mtype | TYPE | 显示 MS-DOS 文件的内容 |
| mwrite | COPY | 将 Linux 文件复制到 MS-DOS |
| mzip |  | 对 SCSI Zip 磁盘执行某些操作 |

你可以像使用相应的 DOS 命令一样使用 mtools 命令。例如，mdir 命令的工作方式与 DOS 中的 DIR 命令相同。表 3-4 中显示的所有其他 mtools 命令也一样。
