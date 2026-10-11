
```
00032 /dev/dsk/c9t0d0   00032 current
·
·
·
08733 /dev/dsk/c8t0d1   01729 current
08734 /dev/dsk/c8t0d1   01730 current
08735 /dev/dsk/c8t0d1   01731 current
08736 /dev/dsk/c8t0d1   01732 current
08737 /dev/dsk/c8t0d1   01733 current
08738 /dev/dsk/c8t0d1   01734 current
08739 /dev/dsk/c8t0d1   01735 current
08740 /dev/dsk/c8t0d1   01736 current
08741 /dev/dsk/c8t0d1   01737 current
08742 /dev/dsk/c8t0d1   01738 current
08743 /dev/dsk/c8t0d1   01739 current
08744 /dev/dsk/c8t0d1   01740 current
08745 /dev/dsk/c8t0d1   01741 current
08746 /dev/dsk/c8t0d1   01742 current
08747 /dev/dsk/c8t0d1   01743 current
08748 /dev/dsk/c8t0d1   01744 current
08749 /dev/dsk/c8t0d1   01745 current
08750 /dev/dsk/c8t0d1   01746 current
08751 /dev/dsk/c8t0d1   01747 current
08752 /dev/dsk/c8t0d1   01748 current
08753 /dev/dsk/c8t0d1   01749 current
08754 /dev/dsk/c8t0d1   01750 current
```

此列表在显示三个点的地方进行了缩写。只显示了第一个磁盘的开头和最后一个磁盘的结尾。`lvdisplay` 确实显示了组成该逻辑卷的五个主要磁盘。

最后一步是在我们在 `vgu01` 中设置的逻辑卷上放置文件系统。`SAM` 非常适合这项任务。图 9-2 显示了我们所创建的逻辑卷的 `SAM` 屏幕截图。为十个卷组中的每一个创建了一个逻辑卷。

![](img/eff8b9287a5f38c5adf538f24aacf29e_500_0.png)

图 9-2 vgv01 至 vgv10 上的 lvol1

卷组 vgv01 至 vgv10 中均存在 lvol1。我们希望在每个逻辑卷上创建文件系统，以运行当前应用程序。尽管我们可以在命令行中执行相应的命令，但我们将使用 `SAM` 来完成此任务。

![](img/eff8b9287a5f38c5adf538f24aacf29e_501_0.png)

图 9-3 在 `vgv01` 的 `lvol1` 上添加文件系统

如图本图所示，我们选择在 `vgv01` 的 `lvol1` 上添加文件系统。

接下来，我们需要修改逻辑卷的默认设置，如本图 9-4 所示：

![](img/eff8b9287a5f38c5adf538f24aacf29e_502_0.png)

图 9-4 修改文件系统默认设置

在此界面中，我们需要确保*允许大文件*，因为我们将运行会创建许多大文件的数据库应用程序。如果我们在创建文件系统时未包含大文件支持，且正在运行 Online JFS，我们仍可使用 `fsadm` 命令将其转换为支持大文件。我们希望现在挂载此文件系统，并在系统启动时自动挂载，以便在 `/etc/fstab` 中生成相应的条目。

![](img/eff8b9287a5f38c5adf538f24aacf29e_503_0.png)

图 9-5 十个逻辑卷上的十个 VxFS 文件系统

使用 `SAM`，我们在所有十个 lvol1 上创建了十个 VxFS 文件系统。我们必须在 `SAM` 中逐个创建这十个文件系统，因此使用 shell 程序进行自动化处理可能更为合适。

`SAM` 会自动将这些条目添加到 `/etc/fstab`，因为我们指定了立即挂载并在系统启动时挂载，如下所示：

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

没有任何理由表明我们不能在命令行中执行文件系统相关命令，例如 `newfs` 和 `fsadm`，就像我们之前执行卷相关命令一样。由于大多数人使用 `SAM` 执行这些操作，因此我认为使用 `SAM` 来说明会更为恰当。

下一节将提供一些使用逻辑卷管理器时可能需要执行的各种操作提示。这些都是我多次使用过的操作，当你需要执行类似任务时可能会对你有所帮助。

### 常用 LVM 操作

系统管理员在执行任何侵入性（存在更改 LVM 相关内容的可能性）LVM 命令之前通常都很谨慎。在执行任何侵入性 LVM 命令之前，请务必备份系统，并使用 Ignite-UX 创建可引导的恢复磁带。以下是我常规遇到的一些任务的操作步骤。请根据你的需求进行修改。请勿直接运行所示命令。你需要准备系统，替换卷的名称，并执行额外的步骤。不过，这些命令可以作为展示如何执行上述任务的良好示例。

我们要执行的第一个任务是在未镜像的系统上更换故障磁盘（图 9-6）。

```text
# vgrecreate -a /dev/vgXX /dev/rmdsk/cxtx0d
# vgchange -a y /dev/vgXX
# newfs -F vxfs /dev/vgXX/lvol1
# mount /mountpointname
```

注意事项：

- 确认你拥有 `/etc/lvmconf/vgXX.conf`

- `vgcgbackup` 会自动运行

- 故障磁盘在失效前未进行镜像

- 你的系统可能需要额外的步骤

### 图 9-6 更换非镜像磁盘

在此示例中，我们有一块非镜像且非根磁盘出现故障并需要更换。更换磁盘后，使用 `vgrecreate` 恢复该特定磁盘的卷组信息。然后，我们将卷组更改为可用状态，在磁盘上运行 `newfs`，并挂载使用该磁盘的文件系统。
