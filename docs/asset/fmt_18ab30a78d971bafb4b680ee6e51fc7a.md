
```
castle# df
  (/dev/disk/c0t3d0s0): 119680 blocks 407239 files
  /proc                 (/proc) 0 blocks 930 files
  /dev/fd               (fd) 0 blocks 0 files
  /tmp                  (swap) 252720 blocks 9771 files
  /files                (/dev/disk/c0t0d0s2): 293656 blocks 236812 files
castle$ 
```

列报告文件系统位置、文件系统的设备名称、空闲块数量和 inode 数量。

# `df` 241

要以旧的 SunOS 4.x 格式显示输出，请输入 `df -k` 并按回车，如下例所示。

```
castle% df -k
Filesystem kbytes used avail capacity Mounted on
/dev/dsk0t3d0s0 87909 819239 58375 94% /
/proc 0 0 0 0% /proc
fd 0 0 0 0% /dev/fd
swap 126632 276 126356 1% /tmp
/dev/dsk0t0d0s2 489702 342874 146339 71% /files
castle%$
```

对于本地磁盘分区，这些列报告文件系统位置、总千字节、可用千字节、容量使用百分比和挂载点。

`directory` 表示有效的目录名。如果你指定了 `directory`，`df` 将报告包含目录的文件系统。`block-device` 表示块设备（例如 `/dev/dsk/c1d0s7`）；如果你指定了 `block-device`，则相应的文件系统不需要挂载。`resource` 是一个 NFS 资源。

## 选项

- `-a` 报告所有文件系统，包括那些在 `/etc/mntab`（参见 `mntab(4)`）条目中设置了 `ignore` 选项的文件系统。
- `-b` 打印空闲文件总数。
- `-e` 仅打印空闲文件数量。
- `-F Ftype` 指定要操作的 `Ftype`。只有当文件系统未挂载时才需要使用此选项。`df` 通过将目录、 `block-device` 或 `resource` 与 `/etc/vfstab` 表中的条目匹配（参见 `vfstab(4)`）或咨询 `/etc/default/fs` 从此选项中确定 `Ftype`。参见 `default_fs(4)`。此命令可能不支持所有的 `Ftypes`。
- `-k` 以千字节为单位打印分配情况。输出每个指定的文件系统包含一行信息。这些信息包括文件系统名称、分配给现有文件系统的总空间、系统、非特权用户创建新文件的可用空间量，以及当前分配给文件系统上所有文件的正常可用空间百分比。此选项会覆盖 `-b`, `-e`, `-n` 和 `-t` 选项。
- `-l` 仅报告本地文件系统。此选项仅用于已挂载的文件系统。它不能与 `-o` 选项一起使用。
- `-n` 仅打印 `FSType` 名称。在不带操作数调用时，该选项列出已挂载的文件系统类型列表。此选项仅用于已挂载的文件系统。它不能与 `-o` 选项一起使用。
- `-o FSType-specific-options` 将 `FSType-specific-options` 指定为逗号分隔的列表，中间不留空格。
- `-P` 与 `-k` 相同，但以 512 字节为单位报告。（仅限 `/usr/xpg4/bin/df`。）
- `-t` 打印带有总数的列表。这会覆盖 `-b`, `-e` 和 `-n` 选项。
- `-V` 回显完整的文件系统命令行集，但不执行它们。命令行是通过使用用户提供的选项和操作数，并添加源自 `/etc/motab`、`/etc/vfstab` 或 `/etc/default/fs` 的信息而生成的。你可以使用此选项来验证和确认命令行。

### 操作数

- `- directory` 一个有效的目录名。`df` 报告包含目录的文件系统。
- `- block-device` 一个块设备（例如 `/dev/dsk/c1d0s7`）；如果你指定了 `block-device`，则相应的文件系统不需要挂载。
- `- resource` 一个 NFS 资源。

## 用法

- `- directory` 一个有效的目录名。`df` 报告包含目录的文件系统。
- `- block-device` 一个块设备（例如 `/dev/dsk/c1d0s7`）；如果你指定了 `block-device`，则相应的文件系统不需要挂载。
- `- resource` 一个 NFS 资源。

## 示例

以下是 `df` 的输出：

```
castle# df
  (/dev/disk/c0t3d0s0): 119680 blocks 407239 files
  /proc                 (/proc) 0 blocks 930 files
  /dev/fd               (fd) 0 blocks 0 files
  /tmp                  (swap) 252720 blocks 9771 files
  /files                (/dev/disk/c0t0d0s2): 293656 blocks 236812 files
castle$ 
```

以下是带 `-k` 选项的输出：

```
castle% df -k
Filesystem kbytes used avail capacity Mounted on
/dev/dsk0t3d0s0 87909 819239 58375 94% /
/proc 0 0 0 0% /proc
fd 0 0 0 0% /dev/fd
swap 126632 276 126356 1% /tmp
/dev/dsk0t0d0s2 489702 342874 146339 71% /files
castle%$
```

以下是带 `-V` 选项的输出：

```
castle% df -V
Solaris 10)
```

以下是带 `-t ufs` 选项的输出：

```
castle% df -t ufs
Filesystem kbytes used avail capacity Mounted on
/dev/dsk0t3d0s0 87909 819239 58375 94% /
/proc 0 0 0 0% /proc
/dev/dsk0t0d0s2 489702 342874 146339 71% /files
```

以下是带 `-f ufs` 选项的输出：

```
castle% df -f ufs
Filesystem kbytes used avail capacity Mounted on
/dev/dsk0t3d0s0 87909 819239 58375 94% /
/proc 0 0 0 0% /proc
/dev/dsk0t0d0s2 489702 342874 146339 71% /files
```

以下是带 `-f nfs` 选项的输出：

```
castle% df -f nfs
Filesystem kbytes used avail capacity Mounted on
/proc 0 0 0 0% /proc
```

以下是带 `-P` 选项的输出：

```
castle% df -P
Filesystem inodes free capacity Mounted on
/dev/disk/c0t3d0s0 119680 407239 58375 94% /
/proc 0 930 0 0% /proc
/dev/fd 0 0 0 0% /dev/fd
swap 252720 9771 242949 4% /tmp
/dev/disk/c0t0d0s2 293656 236812 56844 100% /files
```

以下是带 `-a` 选项的输出：

```
castle% df -a
Filesystem inodes free capacity Mounted on
/dev/disk/c0t3d0s0 119680 407239 58375 94% /
/proc 0 930 0 0% /proc
/dev/fd 0 0 0 0% /dev/fd
swap 252720 9771 242949 4% /tmp
/dev/disk/c0t0d0s2 293656 236812 56844 100% /files
```

## 245

### name

DHCP 协议返回给客户端的参数的长名称。

## 退出状态

- `0` 操作成功。
- `-2` DHCP 失败。DHCP 代理可能未运行，接口可能配置失败，或者没有收到满意的 DHCP 响应。
- `-3` 参数错误。
- `-4` 设置了计时器，使用了等待模式（参见 `ifconfig(1M)`），且接口在过期前未配置。
- `-6` 某些系统错误（不应发生）。

## 属性

有关以下属性的描述，请参见 `attributes(5)`：

| 属性类型 | 属性值 |
|---|---|
| 可用性 | SUNwcsr |

## 参见
