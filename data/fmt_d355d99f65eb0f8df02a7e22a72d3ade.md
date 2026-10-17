
## 17.12.8.2 灾后恢复

关键问题是：你的硬件是否进行了定期备份，这样就不需要担心软件了。

如果硬件已损坏，在尝试使用计算机之前应该更换部件。

如果你的硬件正常，请检查你的软盘。如果你使用的是拷贝的启动软盘，请以单用户模式启动（在启动提示符输入 `-s`）。跳过以下段落。

如果你有 `boot.flop` 和 `fixit.flip` 软盘，请继续阅读。将 `boot.flop` 插入第一个软盘驱动器和计算机中。屏幕上将显示原始菜单。选择使用 CDROM 或软盘的 Fixit-Repair 模式。在提示时插入 `fixit.flop`。执行你需要的其他程序位于 `/mnt2/rescue`（对于 5.2 之前的 FreeBSD 版本，位于 `/mnt2/stand`）。

恢复你的文件系统。

挂载文件系统的根分区（例如 `/dev/da1`）。如果 `bsdlabel` 损坏，使用 `bsdlabel` 重新分区，并使标签与你打印并保存的标签匹配。使用 `newfs` 重新创建文件系统。以读写模式重新挂载软盘的根分区（`mount -o rw /mnt`）。使用你的备份程序和磁带恢复该文件系统的数据（例如 `restore vrf /dev/sa0`）。卸载文件系统（例如 `mount /mnt` 之后）。对每个损坏的文件系统重复此操作。

一旦你的系统运行，请将你的数据备份到新的磁带上。无论再次发生什么崩溃或数据丢失，现在多花一个小时可能会避免日后遭受更多困扰。

## 17.13 网络、内存和文件支持的文件系统

由 Marc Vonfieldie 重新组织和增强。

除了你物理插入计算机的磁盘（软盘、CD、硬盘等）之外，FreeBSD 还能理解其他形式的磁盘——虚拟磁盘。

这些包括网络文件系统（如网络文件系统 NFS 和 Coda）、基于内存的文件系统以及文件支持的文件系统。

根据你运行的 FreeBSD 版本，你可能需要使用不同的工具来创建和使用文件支持以及基于内存的文件系统。

> 注意：使用 `devfs(5)` 为用户分配设备节点。

### 17.13.1 文件支持的文件系统

工具 `mdconfig(8)` 用于在 FreeBSD 下配置和启用内存磁盘 `md(4)`。要使用 `mdconfig(8)`，你必须加载 `md(4)` 模块或在你的内核配置文件中添加该支持：

```bash
device md
```

`mdconfig(8)` 命令支持三种内存支持的虚拟磁盘：使用 `malloc(9)` 分配的内存磁盘、使用文件或交换空间作为备备的内存磁盘。一种可能的用途是挂载存储在文件中的软盘或 CD 镜像。

挂载现有文件系统：

#### 示例 17-4. 使用 mdconfig 挂载现有文件系统镜像

```bash
# mdconfig -a t vnode -f diskimage -u 0
# mount /dev/md0 /mnt
```

使用 `mdconfig(8)` 创建新文件系统：

#### 示例 17-5. 使用 mdconfig 创建新的文件支持的磁盘

```bash
# dd if=/dev/saro of=newimage bs=1lk count=5k
5120+0 records in
5120+0 records out
# mdconfig -a t vnode -f newimage -u 0
# bslabel -w mdo auto
# newfs/md0:
```

`/dev/md0`: 5.0MB (10224 sectors) block size 16384, fragment size 2048
    4 cylinder groups of 1.25MB, 80 blocks, 192 inodes.
super-block backups (for fsck -b):
160, 2720, 7840

```bash
# mount /dev/md0 /mnt
# /mnt
Filesystem 1-blocks Used On
/dev/md0 4718 4338 0%
```

如果你没有使用 `-u` 指定单元，`mdconfig(8)` 将使用 `md(4)` 自动选择未使用的设备。分配的单元名称将输出在 stdout 上。关于 `mdconfig(8)` 的更多细节，请参考手册页。

`mdconfig(8)` 工具在创建文件支持的文件系统时非常有用。FreeBSD 自带了一个名为 `mdfs(8)` 的工具，它使用 `mdconfig(8)` 配置 `md(4)` 磁盘，使用 `newfs(8)` 在其创建 UFS 文件系统，并使用 `mount(8)` 进行挂载。例如，如果你想创建并挂载相同的文件系统，请尝试以下：

#### 示例 17-6. 使用 mdfs 配置并挂载文件支持的磁盘

```bash
# dd if=/dev/saro of=newimage bs=1lk count=5k
5120+0 records in
5120+0 records out
# mdfs -F newimage -s 5m md0 /mnt
# /mnt
Filesystem 1-blocks Used Capacity
/dev/md0 4718 4338 0%
```

如果你在使用 md 时没有单元号，`mdfs(8)` 将使用 auto-unit 选择未使用设备。关于 `mdfs(8)` 的更多细节，请参考手册页。

### 17.13.2 基于内存的文件系统

对于基于内存的文件系统，应使用 'swap backing'。使用交换支持并不意味着内存磁盘默认会交换到磁盘，而是内存磁盘从池中分配，并在需要时可以交换出。也可以创建由 `malloc(9)` 支持的内存磁盘，但如果内核耗尽，使用较大的 malloc 磁盘会导致系统崩溃（panic）。

#### 示例 17-7. 使用 mdconfig 创建基于内存的磁盘

```bash
# mdconfig -a t swap -s 5m -u 2
# newfs -u md1
/dev/md1:5.0MB (10240 sectors) block size 16384, fragment size 2048
using 4 groups of 1.27MB, 81 blocks, 192 inodes.
super-block backups (for fsck -b):
160, 2752, 5344, 7936
# mount /dev/md1 /mnt
# /mnt
Filesystem 1-blocks Used Available Capacity
/dev/md1 4718 2 4458 0%
```

#### 示例 17-8. 使用 mdconfig 创建新的基于内存的磁盘

```bash
# mdconfig -a 3m md2 /mnt
# /mnt
Filesystem 1-blocks Used Available Capacity
/dev/md2 4846 2 4458 0%
```

### 17.13.3 从系统中分离基于内存的文件系统

当不再使用基于内存或基于文件的系统时，你应该向系统释放所有资源。要要做的是卸载文件系统，然后使用 `mdconfig(8)` 将磁盘从系统中分离并释放资源。

例如，释放 `/dev/md4` 的所有资源：

```bash
# mdconfig -d -u
```

可以使用 `mdconfig -l` 命令列出已配置的 `md(4)` 设备的信息。

## 17.14 文件系统快照

Tom Rhodes 贡献。

FreeBSD 在 Soft Updates 中提供了一个功能：文件系统快照。

快照允许用户创建指定文件系统的镜像并将其视为文件。快照文件必须在执行操作的文件系统中创建，用户每个文件系统最多可以创建 20 个快照。

活动快照记录在超级块中，因此它们在系统重启重新挂载期间是持久的。当不再需要快照时，可以使用标准的 `rm(1)` 命令删除。快照可以按任何顺序删除，但可能无法获得所有使用的空间，因为另一个快照可能会占用某些释放的块。

不可更改的快照标志由 `mksnap_fs(8)` 在初始创建快照文件后设置。`unlink(1)` 命令对快照文件例外，允许删除它们。

快照使用 `mount(8)` 命令创建。使用以下命令将 `/var` 的快照放置在文件 `/var/snapshot/snap`：

```bash
# mount -u -o snapshot /var/snapshot/snap /var
```

或者，你可以使用 `mksnap_fs(8)` 创建快照：

```bash
# mksnap_fs_fs /var /var/snapshot/snap
```

可以使用 `find(1)` 命令在文件系统（例如 `/var`）中查找快照：

```bash
# find -t /var -flags snapshot
```
