
软盘挂载后，你可以使用 Linux 的复制命令（`cp`）向软盘复制文件和从软盘复制文件。要将当前目录中的文件 `gnome1.pcx` 复制到软盘，输入以下内容：

```
cp gnome1.pcx /mnt/floppy
```

同样，要查看软盘的内容，输入以下内容：

```
ls /mnt/floppy
```

当你想从驱动器中取出软盘时，首先卸载软盘驱动器。此操作会移除软盘文件系统与 Linux 文件系统上的挂载点之间的关联。使用 `umount` 命令卸载设备，如下所示：

```
umount /dev/fd0
```

你可以设置 Linux 系统，使任何用户都可以挂载 DOS 软盘。你只需以 root 身份登录并在 `/etc/fstab` 文件中添加一行。例如，要启用用户在 `/a` 目录挂载 A: 驱动器上的 DOS 软盘，请执行以下步骤：

- 1. 以 root 身份登录。
- 2. 使用以下命令创建 `/a` 目录：
  `mkdir /a`
- 3. 在文本编辑器（如 `vi` 或 `Emacs`）中编辑 `/etc/fstab` 文件并插入以下代码。然后保存文件并退出编辑器。
  `/dev/fd0   /a   vfat   noauto,user   0 0`
  在该行中，`user` 选项（紧跟在 `noauto` 后面）使所有用户都可以挂载 DOS 软盘。该行中的第一个字段是设备名称（`/dev/fd0`），第二个是挂载目录（`/a`），第三个字段显示文件系统类型（`vfat`）。
- 4. 注销并以普通（非 root）用户身份登录。
- 5. 为测试无需 root 即可挂载 DOS 软盘，将 DOS 软盘插入 A: 驱动器并输入以下命令：
  `mount /a`
  请注意，你使用挂载目录作为 `mount` 命令的参数。挂载操作应成功，并且当你输入命令 `ls /a` 时应能看到 DOS 软盘的列表。
- 6. 要卸载 DOS 软盘，输入 `umount /a`。

## 使用 mtools 访问和操作 DOS/Windows 软盘

到目前为止，你已学习了一种访问 MS-DOS 文件系统的方法：使用 `mount` 命令挂载 DOS 硬盘或软盘；然后使用常规 Linux 命令，如 `ls` 和 `cp`。对于硬盘来说，这种挂载 DOS 文件系统的方法是可以的。Linux 可以在启动时自动挂载 DOS 分区，并且你随时可以访问硬盘上的 DOS 目录。

但是，如果你想快速列出 DOS 软盘的目录，你可能会觉得挂载很麻烦。这时 `mtools` 包就派上用场了。`mtools` 包是一组实用程序，实现了大多数常见的 DOS 命令。这些命令的名称与 DOS 中的相同，只是每个命令前加上 `m` 前缀。因此，`mdir` 会检索目录列表，`mcopy` 会复制文件。`mtools` 最好的地方在于，你无需挂载软盘即可使用 `mtools` 命令。

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_213_0.png)

由于 `mtools` 命令会向物理设备（软盘）写入和读取数据，因此你必须以 root 身份登录才能执行这些命令。如果想让任何用户访问 `mtools` 命令，你必须更改软盘驱动器设备的权限设置。使用以下命令允许任何人对第一个软盘驱动器进行读写：

```
chmod o+rw /dev/fd0
```

### 验证是否已安装 mtools

`mtools` 包随本书附带的 CD-ROM 上的 Red Hat Linux 发行版提供。安装 Red Hat Linux 时，`mtools` 会作为基础 Linux 的一部分自动安装。`mtools` 可执行文件位于 `/usr/bin` 目录中。要查看是否已安装 `mtools`，请在 shell 提示符下输入 `ls /usr/bin/mdir`。如果 `ls` 命令显示该文件存在，则说明你的系统上可以使用 `mtools`。

你也可以输入以下 `rpm` 命令来验证系统上是否已安装 `mtools`：

```
rpm -q mtools
mtools-3.9.7-3
```

如果已安装 `mtools`，输出会显示 `mtools` 包的完整名称。示例输出显示系统上安装了 `mtools` 版本 3.9.7。要尝试 `mtools`，请按以下步骤操作：

- 1. 以 root 身份登录，或输入 `su` 然后输入 root 密码。
- 2. 将 MS-DOS 软盘放入系统 A: 驱动器中。
- 3. 输入 `mdir`。你应该会看到软盘的目录（采用标准的 DOS 目录列表格式）。

### 检查 /etc/mtools.conf 文件

`mtools` 包应能与默认设置一起工作；但如果出现任何错误，你应检查 `/etc/mtools.conf` 文件。该文件包含 `mtools` 实用程序所看到的驱动器（如 A:、B: 和 C:）的定义。以下是典型的 `/etc/mtools.conf` 文件中的几行：

```
drive a: file="/dev/fd0" exclusive 1.44m
drive b: file="/dev/fd1" exclusive 1.44m
# First SCSI hard disk partition
#drive c: file="/dev/sda1"
# First IDE hard disk partition
drive c: file="/dev/hda1"
# IDE Zip drive
drive X: file="/dev/hdd4" exclusive
```
