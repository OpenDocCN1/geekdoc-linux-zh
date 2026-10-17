
### 从命令行挂载 CD-ROM

挂载 CD-ROM 非常简单。如果您在文本模式环境中工作（即使用远程 shell 或控制台），您可以按以下方式挂载 CD-ROM：

- 1. 将 CD-ROM 插入 CD-ROM 驱动器。
- 2. 以 root 身份运行 `mount /mnt/cdrom` 命令来挂载 CD-ROM。现在您应该能够从 `/mnt/cdrom` 目录访问插入的 CD-ROM。

![](img/9eb7e89292d2f85707b4d49102c865b7_197_0.png)

`mount /mnt/cdrom` 命令默认应该可以工作，因为 Red Hat Linux 在 `/etc/fstab` 文件中包含以下配置行，以便使用上述命令挂载 CD-ROM。

```
/dev/cdrom /mnt/cdrom iso9660 noauto,owner,kudzu,ro 0 0
```

如果此命令对您不起作用，您可以改用 `mount -t iso9660 /mnt/cdrom /dev/cdrom` 命令。
- 3. 当您需要弹出 CD-ROM 时，应使用 `umount /mnt/cdrom` 命令卸载它，然后运行 `eject /mnt/cdrom` 命令将其弹出。

### 从图形环境挂载 CD-ROM

如果您使用的是 X Window System，在将 CD-ROM 插入 CD-ROM 驱动器后，您应该能够访问 CD-ROM。单击桌面上的 CD-ROM 图标以访问内容。您可以通过右键单击 CD-ROM 图标并选择“弹出设备”选项随时弹出 CD-ROM，这将自动卸载 CD-ROM。

如果 X 在插入驱动器时未自动挂载您的 CD-ROM（如 root 用户时），您需要执行以下操作：
- 1. 通过单击面板上的工具箱图标运行 GNOME 控制中心程序，或单击主菜单按钮并选择程序 → 设置 → GNOME 控制中心，然后从左侧树菜单中选择外设 → CD 属性。
- 2. 在“数据 CD”部分下选择“插入时自动挂载 CD”选项。

![](img/9eb7e89292d2f85707b4d49102c865b7_198_0.png)

> 如果您只想在需要时挂载 CD-ROM，可以禁用自动挂载选项，然后只需右键单击桌面上的 CD-ROM 图标并选择“挂载设备”选项即可挂载它。
- 3. 如果您希望自动播放音频 CD，请在“音频 CD”部分下选择“插入 CD 时运行命令”选项。您也可以在命令行输入框中指定音频 CD 播放器命令，如果您愿意的话，尽管默认的 `gtcd` 播放器工作得相当好。

### 挂载软盘

挂载软盘非常简单。如果您正在运行远程 shell 或终端窗口，请插入软盘并运行 `mount /mnt/floppy` command to mount it. You should be able to access the floppy from the `/mnt/floppy` directory. If you're using the X Window System and are utilizing a graphical environment such as GNOME, simply insert the disk into the disk drive and double-click the floppy disk icon to view the contents of the floppy disk.

## 使用 file 确定文件类型

与 Windows 不同，Linux 不依赖文件扩展名来确定文件类型。在 Linux 中，您使用 `file` 命令来确定文件类型。例如，以下命令显示 `/usr/bin/file`（其本身）是什么类型的文件：

```
file /usr/bin/file
```

这是该命令输出的示例：

```
/usr/bin/file: ELF 32-bit LSB executable, Intel 80386, \
version 1, dynamically linked, not stripped
```

## 使用 stat 查看文件或目录的访问统计信息

您可以使用 `stat` 命令获取文件或目录的统计信息。`stat` 命令的语法是 `stat file_or_directory_path`。例如，以下命令显示 `/tmp` 目录的统计信息：

```
stat /tmp
```

这是其输出的示例：

```
File: "/tmp"

    Size: 2048      Filetype: Directory

    Mode: (1777/drwxrwxrwt)     Uid: (  0/ root)   Gid: (  0/ root)

Device: 3,0   Inode: 16321      Links: 22

Access: Sun Feb  7 02:00:35 1999(00000.00:01:11)

Modify: Sun Feb  7 02:01:01 1999(00000.00:00:45)

Change: Sun Feb  7 02:01:01 1999(00000.00:00:45)
```

## 使用 cp 复制文件和目录

使用 `cp` 命令将文件从一个位置复制到另一个位置。例如，以下命令将名为 `important.txt` 的文件从 `/some` 目录复制到 `/new/place` 目录：

```
cp /some/important.txt /new/place/
```

![](img/9eb7e89292d2f85707b4d49102c865b7_200_0.png)

如果需要，您还可以通过在命令中将新文件名添加到目标路径末尾来指定新的目标文件名。

要将文件复制到已存在同名文件的位置，您可以使用 `-f` 选项强制 `cp` 覆盖现有文件。例如，以下命令即使 `/new/place` 目录中已存在该名称的文件也会复制 `important.txt` 文件：

```
cp -f /some/important.txt /new/place/
```

要连同其所有文件和子目录一起复制目录，请使用 `-r` 选项递归复制目录。命令的语法是 `cp -r source_directory destination_directory`。例如，以下命令将 `/tmp/foo` 目录连同目录本身的内容和所有子目录一起复制到 `/zoo/foo` 目录：

```
cp -r /tmp/foo /zoo/foo
```

## 使用 mv 移动文件和目录

要移动文件或目录，请使用 `mv` 命令。`mv` 的语法是 `mv original_path new_path`。例如，以下命令将 `/file1` 移动到 `/tmp/file2`：

```
mv /file1 /tmp/file2
```

同样，您可以递归地连同其所有内容一起移动目录。为此，请使用 `-r` 选项使用 `cp` 将目录复制到新的文件系统，然后从当前位置删除该目录（请参阅下一节）。

![](img/9eb7e89292d2f85707b4d49102c865b7_201_0.png)

`mv` 不会在不同的文件系统之间移动目录。当您需要将目录从一个文件系统移动到另一个文件系统时，请使用 `-r` 标志使用 `cp` 命令复制目录，如上所述，然后您可以使用 `rm` 命令删除旧目录，如下所述。

## 使用 rm 删除文件和目录

要删除文件或目录，请使用 `rm` 命令。`rm` 命令的语法是 `rm file_or_directory_name`。例如，以下命令删除名为 `letter.txt` 的文件：

```
rm letter.txt
```

要递归删除目录的内容，您需要指定 `-r` 选项。您可以使用 `-f` 选项强制删除。例如，以下命令删除指定目录内的所有文件和子目录：

```
rm -rf directory
```

![](img/9eb7e89292d2f85707b4d49102c865b7_201_1.png)

您可以按如下方式设置名为 `rm` 的别名：

```
alias rm 'rm -i'
```

在这种情况下，`-i` 选项告诉命令在实际删除任何内容之前提示您。

## 处理权限

权限允许在多用户系统上实现安全性。在本节中，我讨论权限的基础知识以及可以更改权限的一些常用工具。我还为您提供一些示例权限策略，您可以按原样使用或根据需要进行自定义。

### 了解文件和目录权限

Linux 将文件或目录与用户和组关联，就像所有其他 Unix 和类 Unix 操作系统一样。术语权限指的是决定谁有权读取、写入和执行（对于可执行文件）文件的方面。

默认情况下，文件的权限属于文件的所有者。当创建新文件时，文件所有者是文件创建者，组是所有者的默认组。在 Red Hat Linux 中，当用户创建文件或目录时，其组也设置为用户的默认组，该组恰好是一个与用户名相同的私有组。
