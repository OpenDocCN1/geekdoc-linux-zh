

## 自动挂载设置

默认情况下，ZFS 文件系统会自动挂载，无需 **vfstab** 条目。但是，你可以通过设置 ZFS 文件系统属性来改变这一行为。交换区域和非文件系统挂载仍应出现在 **vfstab** 中。

**mount**、**umount**、**swapon** 和 **fsck** 都会读取文件系统清单，因此其中列出的数据正确且完整会很有帮助。如果你在命令行中只指定了分区名或挂载点，你也许还想借助该清单来确定要执行的操作。例如，在第 262 页所示的 Linux **fstab** 配置中，命令

```
$ sudo mount /media/cdrom0
```

与输入下面的命令效果相同：

```
$ sudo mount -t udf -o user,noauto,exec,utf8 /dev/scd0 /media/cdrom0
```

命令 **mount -a** 会挂载文件系统清单中列出的所有常规文件系统；它通常在引导时由启动脚本执行。²⁰ 带有 *fstype* 参数的 **-t**、**-F** 或 **-v** 标志（Linux 用 **-t**，Solaris 和 HP-UX 用 **-F**，AIX 用 **-v**）可将操作限制为特定类型的文件系统。例如，

```
$ sudo mount -at ext4
```

会挂载所有本地 ext4 文件系统。**mount** 命令按顺序读取 **fstab**。因此，挂载在其他文件系统之下的文件系统，在 **fstab** 文件中必须位于其父分区之后。例如，如果 **/var** 是独立文件系统，则 **/var/log** 的行必须位于 **/var** 的行之后。

用于卸载文件系统的 **umount** 命令接受类似的语法。你不能卸载某个进程正将其用作当前目录或其上仍有文件打开的文件系统。有一些命令可用来识别妨碍你执行 **umount** 操作的进程；参见第 144 页。

HP-UX 的 **fstab** 文件是我们示例系统中最传统的一个。以下是只有一个卷组的系统的条目：

| 设备 | 挂载点 | 类型 | 选项 | 序号 |
|---|---|---|---|---|
| /dev/vg00/lvol3 | / | vxfs | delaylog | 0 1 |
| /dev/vg00/lvol1 | /stand | vxfs | tranflush | 0 1 |
| /dev/vg00/lvol4 | /tmp | vxfs | delaylog | 0 2 |
| /dev/vg00/lvol5 | /home | vxfs | delaylog | 0 2 |
| /dev/vg00/lvol6 | /opt | vxfs | delaylog | 0 2 |
| /dev/vg00/lvol7 | /usr | vxfs | delaylog | 0 2 |
| /dev/vg00/lvol8 | /var | vxfs | delaylog | 0 2 |

每行有六个字段，以空白字符分隔。每一行描述一个文件系统。这些字段传统上会对齐以便阅读，但并非必须对齐。

有关 NFS 的更多信息，请参见第 18 章。

第一个字段给出设备名。fstab 文件可以包含来自远程系统的挂载，在这种情况下，第一个字段包含 NFS 路径。server:/export 这种写法表示名为 server 的机器上的 /export 目录。

第二个字段指定挂载点，第三个字段指定文件系统类型。用于标识本地文件系统的确切类型名称因机器而异。

第四个字段指定默认应用的挂载选项。选项有很多；有关所有文件系统类型通用的选项，请参见 mount 的手册页。个别文件系统通常会引入自己的选项。上面显示的所有选项都是 VxFS 特有的。例如，delaylog 选项为了速度而牺牲了一定的可靠性。有关此选项及其他 VxFS 挂载选项的更多信息，请参见 mount_vxfs 手册页。

第五和第六个字段是残留字段。它们本应是“转储频率”列和用于控制 fsck 并行度的列。在当代系统中，两者都不重要。

下面是从 Ubuntu 系统的 fstab 中挑选的一些额外示例。总体格式相同，但 Linux 系统通常会有一些额外花哨内容。

```
proc /proc proc defaults 0 0
UUID=a8e3...8e8a / ext4 errors=remount-ro 0 1
UUID=13e9...8d2 none swap sw 0 0
/dev/scd0 /media/cdrom0 udf,iso9660 user,noauto,exec,utf8 0 0
/dev/scd1 /media/cdrom1 udf,iso9660 user,noauto,exec,utf8 0 0
/dev/fd0 /media/floppy0 auto rw,user,noauto,exec,utf8 0 0
```

第一行涉及 /proc 文件系统，它实际上由内核驱动程序呈现，并没有真正的后备存储。第一列中列出的 proc 设备只是一个占位符。

第二行和第三行使用分区 ID（UUID，我们为便于阅读而对摘录做了截断）而不是设备名来标识卷。这种替代方案在 Linux 系统上很有用，因为磁盘分区的设备名不稳定；添加或移除磁盘可能会导致所有其他磁盘改变名称（例如，从 /dev/sdb1 变为 /dev/sdc1）。UUID 仅与分区的内容相关联，因此无论分区隐藏在哪里，都可以通过它找到该分区。请注意，这一约定既适用于交换分区，也适用于根分区。

