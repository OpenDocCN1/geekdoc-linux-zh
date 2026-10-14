
## 如何挂载文件系统

你可以使用 `mount` 命令手动挂载文件系统。挂载文件系统的通用语法为：

```
mount [-t file_system_type] [-o mount_options] device mount_point
```

通过使用 `mount`，你可以覆盖 `/etc/fstab` 中的设置。例如，输入以下命令挂载 `/dev/hda9`：

```
mount /dev/hda9 /
```

通常不需要指定文件系统类型，因为它会自动识别（使用超级块中的 `/etc/fstab` 中在挂载文件系统时可以使用的一些选项）：

- `remount`. 此选项导致已挂载的文件系统重新挂载。当你修改 `/etc/fstab` 中的选项时，可以使用 `remount` 而无需重启系统。
- `rw`, `ro`. 这些选项指示文件系统是可写的 `rw` 还是只读的 `ro`。
- `sync`, `async`. 这些选项设置文件系统的输入输出是同步 `sync` 还是异步 `async`。默认设置是 `async`。
- `atime`, `noatime`. 这些选项设置是否更新文件的访问时间 `atime` 或不 `noatime`。`noatime` 选项应该提高性能。
- `nodev`, `dev`. `nodev` 选项防止设备文件在文件系统中解释为设备。
- `noexec`, `exec`. 你可以在具有 `noexec` 选项的文件系统中禁止执行程序。
- `nosuid`, `suid`. `nosuid` 选项确保文件系统的 suid 和 sgid 位。

某些选项在 `/etc/fstab` 中才有意义。这些选项包括：

- `auto`, `noauto`. 在 `/etc/fstab` 中设置 `noauto` 选项的文件系统在系统启动时不会挂载。这些通常是软磁盘驱动器或 CD-ROM 驱动器。
- `user`, `nouser`. 此选项允许用户挂载文件系统。通常这是 root 用户的权限。
- `defaults`. 此选项导致使用默认选项 `rw`、`suid`、`dev`、`auto`、`nouser` 和 `async`。

`noauto` 和 `user` 选项通常结合用于交换媒体，如软磁盘或 CD-ROM 驱动器。

## 如何在多个位置挂载文件系统

一旦挂载了文件系统，可以使用 `--bind` 参数（自 Linux 2.4.0 起）将其重新挂载到新位置。使用 `--bind` 的语法为：

```
mount --bind old_directory new_directory
```

确保文件系统空空的一种方法是在使用 `umount` 命令之前在 shell 提示符中使用 `cd`。此命令带你进入文件系统的根。例如，将 `/home/user` 目录挂载到 `/tmp/home`，你需要输入：

```
mount --bind /home/user /tmp/home
```

`mount --bind` 命令也用于通过挂载到 `/chroot` 目录来保护服务。

> 注意：为了确定操作文件或目录的进程，可以使用 `fuser` 工具。有关使用 `fuser` 工具的详情，请参阅检查 PID 使用 (`fuser`)。

## 如何卸载文件系统

一旦文件系统被挂载，你可以使用 `umount` 命令（不带 "n"）来卸载文件系统。你可以使用设备或挂载点通过 `umount` 卸载文件系统。

例如，要卸载挂载在 `/media/cdrom` 的 CD 文件系统，你可以输入：

- `umount /media/cdrom`

或

- `umount /dev/cdrom`

为了卸载文件系统，你不应该正处于 shell 提示符中的挂载点。如果你处于挂载点，Linux 会认为文件系统正“忙”并拒绝卸载文件系统。

确保文件系统空闲的方法是在使用 `umount` 命令之前在 shell 提示符中使用 `cd /`。此命令带你进入文件系统的根。

然而，有时无论你尝试做什么，系统（内核）仍然认为文件系统正忙。在这些情况下，你可以输入 `umount -f` 强制卸载文件系统。但是，我们建议将其作为最后的手段，因为内核认为文件系统仍挂载可能由于原因。

## 练习 3-3 从命令行管理文件系统

在本次练习中，你将通过以下操作从命令行管理文件系统：

- 第一部分：创建文件系统
- 第二部分：自定义文件系统

### 第一部分：创建文件系统

执行以下操作：

1. 从 KDE 桌面打开一个终端窗口；然后切换到 root 用户 (`su -`)，密码为 `novel`。

2. 创建以下文件系统：

   a. 输入以下内容在 `/dev/hda5` 上创建一个新的 FAT32 文件系统：

   ```
   mkfs.msdos -n data1 /dev/hda5
   ```

   类似“`mkfs.msdos 2.10 (22 Sep 2006)`”的消息将确认了文件系统的创建。

   b. 输入以下内容在 `/dev/hda6` 上创建一个新的 ext2 文件系统：

   ```
   mkfs -t ext2 -v /dev/hda6
   ```

   通过添加选项 `-v`，你将收到了关于新文件系统的详细信息。

   c. 输入以下命令在 `/dev/hda7` 上创建一个大小仅为 625 MB 的新 Reiser 文件系统：

   ```
   mkreiserfs /dev/hda7 160000
   ```

   会出现一条警告消息，指示 `/dev/hda7` 上的所有数据将丢失。

   d. 输入 `y` 继续。

3. 为文件 `/etc/fstab` 中的新文件系统添加条目：

   a. 输入 `ls -ld /export/` 确保存在一个名为 `/export/` 的目录。

   b. 输入 `cd /export/` 进入 `/export/` 目录。

   c. 使用 `mkdir` 在 `/export/` 下创建目录 `data1` 和 `data3`。

   d. 输入 `ls -l` 验证目录已创建。

   e. 按 `Alt+F2` 打开编辑器，输入 `kdesu kate /fstab` 并选择 `Run`，然后输入密码 `novell` 并选择 `OK`，打开 `/etc/fstab` 文件。

   f. 在 fstab 文件末尾添加以下条目：

   ```
   /dev/hda5 /export/data1 vfat defaults 1 2
   /dev/hda6 /export/data2 ext2 defaults 1 2
   /dev/hda7 /export/data3 reiserfs defaults 1 2
   ```

   必须在文件末尾包含一个空行，否则 `mount` 命令无法读取该文件。

   这些条目确保了 `hda5`、`hda6` 和 `hda7` 分区在系统启动或重启时被挂载。

   `da4` 分区是扩展分区，不需要挂载。

   g. 完成后，选择 `File > Save`（保持 `/etc/fstab` 打开）。

4. 从终端窗口，输入 `mount -a` 挂载所有新文件系统并重新读取 `/etc/fstab` 文件。

### 配置和管理 Linux 文件系统

5. 输入以下三个命令查看挂载文件系统的信息：

```
mount
df -h
cat /etc/mtab
```

### 第二部分：自定义文件系统

在本次练习中，你通过添加日志将分区 `/dev/hda6` 转换为 ext3 文件系统。你还调整了 `/dev/hda7` Reiser 文件系统的大小，使其占用整个分区而不仅仅是 625 MB。

执行以下操作：

1. 修改分区 `/dev/hda6`：

   a. 从终端窗口，输入以下命令查看 `/dev/hda6` 上 ext2 文件系统的详情：

   ```
   dumpe2fs /dev/hda6 | more
   ```

   注意块大小和文件系统状态。

   b. 在文件系统挂载时，输入以下命令为 ext2 文件系统赋予卷名 `/export/data2`：

   ```
   tune2fs -L /export/data2 /dev/hda6
   ```

   在 `/etc/fstab` 不用的系统救援情况下，为文件系统命名非常有用。使用这种命名约定是常见做法。

   c. 输入 `dumpe2fs /dev/hda6 | less` 验证文件系统现在已有了卷名。

   d. 输入 `tune2fs -j /dev/hda6` 为文件系统添加日志（使其成为 ext3 文件系统）。

   e. 输入 `dumpe2fs /dev/hda6 | less` 验证文件系统现在包含日志。

   f. 输入 `mount` 查看挂载文件系统的信息。

   注意文件系统仍作为 ext2 文件系统挂载。

   g. 输入 `umount /dev/hda6` 卸载分区。

   h. 输入 `dumpe2fs /dev/hda6 | less` 验证文件系统状态为洁净。

在 Kate 窗口中编辑 `/etc/fstab` 文件，将文件系统类型从 ext2 改为 ext3，如下：

```
/dev/hda6 /export/data2 ext3 defaults 1 2
```
