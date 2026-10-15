
4. 现在你应该已经该 LV 的空闲 LE 可供其他 LV 使用。

# 调整逻辑卷大小

如果你需要增加现有 LV 的大小，可以从新创建 PV 向其添加空间。这只需要恰当使用 `vgextend` 和 `lvextend` 命令。例如，要向与挂载在 `/home` 目录上的关联 VG 添加 PE，请采取以下步骤：

1. 备份 `/home` 目录上的任何数据。（这是一项标准的预防措施，如果一切顺利，则没有必要。在红帽圣诞节版中你甚至可以跳过这一步。但在实践中，你真的想冒用户数据的风险吗？）
2. 使用适当的类型扩展 VG 以包含新分区。例如，将 `/dev/sdd1` 添加到 `vg_00` VG，运行以下命令：

```
# vgextend vg_00 /dev/vdd1
```
3. 使用以下命令确保你的新分区已包含在 VG 中：

```
# vgdisplay vg_00
```
4. 现在你可以将空间扩展到当前 LV。例如，要将 LV 扩展到 2000MiB，运行以下命令：

```
# lvextend -L 2000M /dev/vg_00/lv_00
```

5. `lvextend` 命令可以按 KiB、MiB、GiB 甚至 TiB 增加分配 LV 的空间。例如，你可以通过以下命令指定一个 2GiB 的 LV：

```
# lvextend -L 2G /dev/vg_00/lv_00
```

6. 如果你喜欢指定额外的空间而不是总空间，可以使用以下示例中的语法为逻辑卷增加 1GiB：

```
# lvextend -L +1G /dev/vg_00/lv_00
```

7. 使用 `xfs_grow` 命令调整格式化卷的大小（如果是 ext2/ext3/ext4 使用 `resize2`）。如果你使用的是扩展的 LV，命令如下：

```
# xfs_grow /dev/vg_00/lv_00
```

8. 或者，可以使用之前描述的命令重新格式化 LV，文件系统可以使用新空间——从备份恢复数据。（如果你已经调整了 LV，请不要重新格式化。这会破坏现有数据！）

```
# mkfs.xfs -f /dev/vg_00/lv_00
```
9. 在任何情况下，都通过 `df` 命令检查新文件系统的大小来完成过程：

```
# df -h
```

# 文件系统管理

在访问文件系统之前，必须挂载文件系统。Linux 通常使用 `/etc/fstab` 配置激活此过程。当 Linux 启动时，`etc/fstab` 中指定的目录通过 `mount` 命令挂载卷。此部分的重点是 `/etc/fstab` 文件，它包含了自定义本地、远程和可移动文件系统的选项。

要查看 `/etc/fstab` 的内容，运行 `cat /etc/fstab` 命令。如图 7-8 所示，每行配置了不同的文件系统。

图 7-8 `/etc/fstab`

```
[root@server1 ~] cat /etc/fstab

# /etc/fstab Created by anaconda on Fri May 12 14:44: 

# Accessible filesystems, by are maintained under /dev/.

# 更多信息请参见 fstab(5), mount(8) 和 blkid(8)。

# 编辑此文件后，卷应格式化为文件系统。

dev/mapper/hel-root      xfs      defaults        UUID=c0e6b10b-22a4-4f13-a827-bf43fb7

dev/mapper/hel-home      xfs      defaults        UUID=408d3dae-6e0c-43ac-b805-d137c80d

/dev/sda                swap    0 0
```

图 7-9 `/etc/mtab`

```
[root@server1 ~]#cat /etc/mtab

sysfs /proc procfs rw,nosuid,nexec,relime 0

devtmp /dev tmpfs rw,nosuid,nexec,relime 0

devpts /dev/pts devpts rw,nosuid,noexec,mode=660,user=0,gid=0 0

sys/kernel/security /sys/kernel/security sysfs rw,nosuid,nexec,relime 0

dev-mapper /dev/mapper dev-mapper tmpfs rw,nosuid,nexec,relime 0

tmpfs /run tmpfs rw,nosuid,nexec,relime 0

journal /var/log/journal journal tmpfs rw,nosuid,nexec,relime 0

shm /dev/shm shm tmpfs rw,nosuid,nexec,relime,mode=0,maxsize=2097152 0

cgroup /dev/cgroup cgroup2-v2 cgroup2 tmpfs rw,nosuid,nexec,relime 0

cgroup /dev/cgroup/system.slice system.slice cgroup2 tmpfs rw,nosuid,nexec,relime 0

cgroup /dev/cgroup/user-1000.slice user-1000.slice cgroup2 tmpfs rw,nosuid,nexec,relime 0

cgroup /dev/cgroup/user-1000.session user-1000.session cgroup2 tmpfs rw,nosuid,nexec,relime 0

devdev /dev/devdev devdev tmpfs rw 0 0

devdev /dev/dev/pts /dev/devpts devpts rw,nosuid,nexec,relime 0

devdev /dev/dev/pts/0 /dev/pts/0 devpts rw,nosuid,nexec,relime 0

devdev /dev/dev/pts/1 /dev/pts/1 devpts rw,nosuid,nexec,relime 0

devdev /dev/dev/udev /dev/udev udev rw rw,nosuid,nexec,relime 0

devdev /dev/dev/udev-dev /dev/udev-dev tmpfs rw,nosuid,nexec,relime 0

devdev /dev/dev/udev-sub-dev /dev/udev-sub-dev tmpfs rw,nosuid,nexec,relime 0

devdev /dev/dev/udev-sub-devices /dev/udev-sub-devices tmpfs rw,nosuid,nexec,relime 0

devdev /dev/dev/udev-sub-run /dev/udev-sub-run tmpfs rw,nosuid,nexec,relime 0

devdev /dev/dev/udev-control-dev /dev/udev-control-dev tmpfs rw,nosuid,nexec,relime 0

devdev /dev/dev/udev-control-sub-dev /dev/udev-control-sub-dev tmpfs rw,nosuid,nexec,relime 0

devdev /dev/dev/udev-control-sub-devices /dev/udev-control-sub-devices tmpfs rw,nosuid,nexec,relime 0
