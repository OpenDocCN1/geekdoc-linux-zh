
- `Ftype` 指定要操作的文件系统类型（参见 `ftype(1M)` 和 `fs_wrapper(5)`）。如果命令行未包含此选项，则通过 `/etc/fstab` 中的条目确定系统类型。如果 `/etc/fstab` 中没有条目，则从 `/etc/default/fs` 文件确定系统类型。

- `-o specific_options` 指定特定于文件系统类型。`specific_options` 是子选项和/或键/属性对列表。参见系统特定的 man 条目以获取支持的 `specific_options`。

- `-V` 输出完整的命令行，但不执行其他操作。命令行通过合并指定的选项、参数以及从 `/etc/fstab` 获取的其他信息生成。此选项允许用户验证命令行。

执行 `newfs` 命令在 `/dev/rdsk/c0s2` 上创建 HFS 文件系统：

```
newfs -F hfs /dev/rdsk/c0s2
```

![](img/6969df54e516231f8e64fd1177ac1127_536_0.png)

作者

`newfs` 由 HP 和加州大学伯克利分校开发。

文件

`/etc/default/fs` 指定默认文件系统类型的文件。

`/etc/fstab` 关于文件系统的静态信息。

参见

`fsck(1M)`, `fstyp(1M)`, `mkfs(1M)`, `newfs_Ftype(1M)`, `fstab(4)`, `fs_wrapper(5)`。

# pv 命令摘要

## "pv" 命令摘要

"pv" 命令 - 与物理卷相关的的命令摘要。

```
pvchange (1M)                                pvchange (1M)
名称
    pvchange - 修改 LVM 卷组中物理卷的特性和访问路径
用法
    /bin/pvchange [-A backup] -s pv_path
    /bin/pvchange [-A backup] -S autoswitch pv_path
    /bin/pvchange [-A backup] -x extensibility pv_path
    /bin/pvchange [-A backup] -t IO_timeout pv_path
```

```
pvcreate (1M)                                pvcreate (1M)
名称
    pvcreate -为 LVM 卷组创建物理卷
用法
    /bin/pvcreate [-b] [-B] [-d soft_defects] [-s disk_size] [-f]
    [-t disk_type] pv_path
```

```
pvdisplay (1M)                             pvdisplay (1M)
名称
    pvdisplay - 显示 LVM 卷组内物理卷的信息
用法
    /bin/pvdisplay [-v] [-b BlockList] pv_path ...
```

```
pvmove (1M)
```

# vg 命令摘要

## "vg" 命令摘要

"vg" 命令 - 与卷组（volume groups）相关的命令摘要。

```
vgcfbackup (1M)               vgcfbackup (1M)
NAME
    vgcfbackup - 创建或更新 LVM 卷组配置备份文件
SYNOPSIS
    /bin/vgcfbackup [-f vg_config_path] [-u] vg_name
```

```
vgcfrestore (1M)      vgcfrestore (1M)
NAME
    vgcfrestore - 从备份文件显示或恢复 LVM 卷组配置
SYNOPSIS
    /bin/vgcfrestore -n vg_name -l
    /bin/vgcfrestore -n vg_name [-o old_pv_path] pv_path
    /bin/vgcfrestore -f vg_config_path -l
    /bin/vgcfrestore -f vg_config_path [-o old_pv_path] pv_path
```

```
vgchange (1M)      vgchange (1M)
NAME
    vgchange - 设置 LVM 卷组的可用性
SYNOPSIS
    激活卷组
    /bin/vgchange -a availability [-l] [-p] [-q quorum] [-s] [-P resync_daemon_count] [vg_name ...]
    分配到高可用性集群并标记卷组为可共享
    /bin/vgchange -c cluster -S cluster vg_name
```

```
vgcreate (1M)      vgcreate (1M)
NAME
    vgcreate - 创建 LVM 卷组

### SYNOPSIS

```
/sbin/vgcreate [-A backup] [-x extensibility] [-e max_pe]

[-l max_lv] [-p max_pv] [-s pe_size] [-g vg_name]

vg_name pv_path ...
```
```

## vgdisplay(1M)

NAME - 显示有关 LVM 卷组的信息

### SYNOPSIS

```
/sbin/vgdisplay [-v] [vg_name ...]
```
```

## vgexport(1M)

NAME
vgexport - 导出 LVM 卷组及其关联的逻辑卷

### SYNOPSIS

```
/sbin/vgexport [-m mapfile] [-p] [-v] vg_name

/sbin/vgexport -m mapfile -s -v vg_name
```
```

## vgextend(1M)

NAME
vgextend - 通过添加物理卷来扩展 LVM 卷组

### SYNOPSIS

```
/sbin/vgextend [-A backup] [-g pvg_name] [-x extensibility]

vg_name pv_path ...
```
```

## vgimport(1M)

NAME
vgimport -向系统导入 LVM 卷组

### SYNOPSIS

```
/sbin/vgimport [-m mapfile] [-p] [-v] vg_name pv_path ...

/sbin/vgimport -m mapfile -s -v vg_name
```
