

![](img/eff8b9287a5f38c5adf538f24aacf29e_500_0.png)

图 9-2 vgv01 至 vgv10 上的 lvol1

卷组 vgv01 至 vgv10 中均存在 lvol1。我们希望在每个逻辑卷上创建文件系统，以运行当前应用程序。尽管我们可以在命令行中执行相应的命令，但我们将使用 SAM 来完成此任务。

![](img/eff8b9287a5f38c5adf538f24aacf29e_501_0.png)

图 9-3 在 *vgv01* 的 *lvol1* 上添加文件系统

如图本图所示，我们选择在 *vgv01* 的 *lvol1* 上添加文件系统。

接下来，我们需要修改逻辑卷的默认设置，如本图 9-4 所示：

![](img/eff8b9287a5f38c5adf538f24aacf29e_502_0.png)

图 9-4 修改文件系统默认设置

在此界面中，我们需要确保*允许大文件*，因为我们将运行会创建许多大文件的数据库应用程序。如果我们在创建文件系统时未包含大文件支持，且正在运行 Online JFS，我们仍可使用 `fsadm` 命令将其转换为支持大文件。我们希望现在挂载此文件系统，并在系统启动时自动挂载，以便在 `/etc/fstab` 中生成相应的条目。

![](img/eff8b9287a5f38c5adf538f24aacf29e_503_0.png)

图 9-5 十个逻辑卷上的十个 VxFS 文件系统

使用 SAM，我们在所有十个 lvol1 上创建了十个 VxFS 文件系统。我们必须在 SAM 中逐个创建这十个文件系统，因此使用 shell 程序进行自动化处理可能更为合适。

SAM 会自动将这些条目添加到 /etc/fstab，因为我们指定了立即挂载并在系统启动时挂载，如下所示：

```text
# System /etc/fstab file. Static information about the file systems
# See fstab(4) and sam(1M) for further details on configuring devices.
/dev/vg00/lvol3 / vxfs delaylog 0 1
/dev/vg00/lvol1 /stand bfs defaults 0 1
/dev/vg00/lvol4 /opt vxfs delaylog 0 2
/dev/vg00/lvol5 /tmp vxfs delaylog 0 2
/dev/vg00/lvol6 /usr vxfs delaylog 0 2
/dev/vg00/lvol7 /var vxfs delaylog 0 2
/dev/vg00/lvol8 /home vxfs delaylog 0 2
/dev/vg00/lvol9 ... swap pri=0 0 0
/dev/vsapp/lvol1 /app vxfs rw, suid, largefiles, delaylog, datainlog 0 2
/dev/vgv01/lvol1 /u01 vxfs rw, suid, largefiles, delaylog, datainlog 0 2
/dev/vgv02/lvol1 /u02 vxfs rw, suid, largefiles, delaylog, datainlog 0 2
/dev/vgv03/lvol1 /u03 vxfs rw, suid, largefiles, delaylog, datainlog 0 2
/dev/vgv04/lvol1 /u04 vxfs rw, suid, largefiles, delaylog, datainlog 0 2
/dev/vgv05/lvol1 /u05 vxfs rw, suid, largefiles, delaylog, datainlog 0 2
/dev/vgv06/lvol1 /u06 vxfs rw, suid, largefiles, delaylog, datainlog 0 2
/dev/vgv07/lvol1 /u07 vxfs rw, suid, largefiles, delaylog, datainlog 0 2
/dev/vgv08/lvol1 /u08 vxfs rw, suid, largefiles, delaylog, datainlog 0 2
/dev/vgv09/lvol1 /u09 vxfs rw, suid, largefiles, delaylog, datainlog 0 2
/dev/vgv10/lvol1 /u10 vxfs rw, suid, largefiles, delaylog, datainlog 0 2
```

此列表显示了我们的十个逻辑卷，其中最后十个条目包含了我们设置的参数，例如 VxFS 和大文件支持。

没有任何理由表明我们不能在命令行中执行文件系统相关命令，例如 **newfs** 和 **fsadm**，就像我们之前执行卷相关命令一样。由于大多数人使用 SAM 执行这些操作，因此我认为使用 SAM 来说明会更为恰当。

下一节将提供一些使用逻辑卷管理器时可能需要执行的各种操作提示。这些都是我多次使用过的操作，当你需要执行类似任务时可能会对你有所帮助。

## 常用 LVM 操作

系统管理员在执行任何侵入性（存在更改 LVM 相关内容的可能性）LVM 命令之前通常都很谨慎。在执行任何侵入性 LVM 命令之前，请务必备份系统，并使用 Ignite-UX 创建可引导的恢复磁带。以下是我常规遇到的一些任务的操作步骤。请根据你的需求进行修改。请勿直接运行所示命令。你需要准备系统，替换卷的名称，并执行额外的步骤。不过，这些命令可以作为展示如何执行上述任务的良好示例。

我们要执行的第一个任务是在未镜像的系统上更换故障磁盘（图 9-6）。

```text
# vgrecreate -a /dev/vgXX /dev/rmdsk/cxtx0d
# vgchange -a y /dev/vgXX
# newfs -F vxfs /dev/vgXX/lvol1
# mount /mountpointname
```

注意事项：
- 确认你拥有 /etc/lvmconf/vgXX.conf
- vgcgbackup 会自动运行
- 故障磁盘在失效前未进行镜像
- 你的系统可能需要额外的步骤

### 图 9-6 更换非镜像磁盘

在此示例中，我们有一块非镜像且非根磁盘出现故障并需要更换。更换磁盘后，使用 **vgrecreate** 恢复该特定磁盘的卷组信息。然后，我们将卷组更改为可用状态，在磁盘上运行 **newfs**，并挂载使用该磁盘的文件系统。

在图 9-7 中，我们将再次更换故障的非根磁盘，但这次磁盘是镜像的。

```text
# vgcfgrestore - /dev/vgXX /dev/rdsk/cxtxdx ; volume group configuration restore
# vgchange -a y /dev/vgXX ; change volume group to available (-a y)
# vgsync /dev/vgXX ; resync logical volumes in volume group
```

注意事项：
- 故障磁盘在失效前是镜像的
- 你的系统可能需要额外的步骤

### 图 9-7 更换镜像磁盘

在此示例中，我们执行了与前两个相同的步骤，即恢复卷组配置并将卷组更改为可用状态。由于磁盘是镜像的，我们只需使用 vgsync 同步新磁盘与其镜像上的数据即可。

在图 9-8 中，我们将再次更换镜像磁盘，但这次磁盘上有引导区域。

```text
# vgcfgrestore - /dev/vgXX /dev/rdsk/ext0xd  ; volume group configuration restore
# vgchange -a y /dev/vgXX                         ; change volume group to available (-a y)
# vgsync /dev/vgXX                                 ; resync logical volumes in volume group
# mkboot /dev/rdsk/ext0xd                          ; create boot area on disk
# mkboot -a "hpux 1q" /dev/rdsk/ext0xd             ; specify low quorum in boot area
# shutdown <desired options>                        ; reboot system to take effect
```

注意事项：
- vgcfgbackup 会自动运行
- 确认你拥有 /etc/lvmconf/vgXX.conf
- 故障磁盘在失效前是镜像的
- 你的系统可能需要额外的步骤

### 图 9-8 更换带有引导区域的镜像磁盘

在此示例中，我们执行了与前一个示例相同的前三个步骤，但还需要在磁盘上创建引导区域。系统必须重新启动才能生效。

在图 9-9 中，我们要将一个卷组迁移到不同的系统上。

在系统 1 上：

```text
# vgchange -a n /dev/vgXX ; change volume group to unavailable (-a n) on 1st system
# vgexport -v -m mapfile -s /dev/vgXX ; make volume group unavailable on 1st system, mapfile will have to be copied to 2nd system, but you don’t have to specify here if standard volume names are used
```

在系统 2 上：

```text
# mkdir /dev/vgXX ; make directory on 2nd system for volume group
# mknod /dev/vgXX/group c 64 0xy0000 ; create special file for vol group (xy=group number such as 00 for vg00, 01 for vg01, and so on)
# vgimport -v -m mapfile -s /dev/vgXX ; import volume group using mapfile copied from 1st system or specify device filenames
# vgchange -a y /dev/vgXX ; make volume group available
```

- 编辑 /etc/fstab 或使用 SAM 以包含新的文件系统

注意事项：
- **vgcfgbackup** 会自动运行
- 你的系统可能需要额外的步骤

### 图 9-9 导出（移除）卷组并将其导入到另一系统

在此示例中，我们在从中迁移卷组的系统上执行了前两个步骤。我们使卷组不可用，然后导出卷组。需要将第一个系统中的 mapfile 复制到第二个系统。如果使用 /dev/vg01 等标准名称，则无需指定 mapfile 名称。无论如何，都必须将 mapfile 复制到卷组正在迁移到的系统。

在第二个系统上，我们为新的卷组创建目录和设备特殊文件。然后导入卷组的 mapfile 并使卷组处于活动状态。最后一步是在 **fstab** 中添加用于挂载文件系统的条目。

图 9-10 显示了将 VxFS 文件系统扩展 800 MBytes。

