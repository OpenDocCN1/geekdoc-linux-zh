
`service cman start`

`service gfs2 start`

`gfs2` 服务脚本将 GFS 文件系统挂载到 `/etc/fstab` 文件中指定的位置。你需要在 `/etc/fstab` 中为所有要挂载的 GFS 文件系统添加条目。`stop` 选项将卸载这些文件系统。你可以使用 `cman_tool` 让节点加入集群或从集群中移除节点。

## 实施 GFS 2 文件系统

要设置 GFS 2 文件系统，你首先需要使用物理卷创建集群设备，并将它们组织为逻辑卷。你使用 `CLVM`（集群逻辑卷管理器）从物理分区设置逻辑卷（过去使用名为 `pool` 的卷管理器来完成此操作）。然后你直接在这些逻辑卷上安装 GFS 文件系统。`CLVM` 像 `LVM` 一样工作，使用相同的命令。它工作在分布式网络上，要求 `clvmd` 服务器正在运行。

然后你使用集群配置系统配置你的系统。创建一个 `/etc/cluster.conf` 文件并设置你的配置。配置将包含诸如使用的节点、隔离方法以及使用的锁定方法等信息。配置详情请查阅 `cluster.conf` 手册页。对于配置，你也可以使用 `system-config-cluster` 工具，它提供了一个易于使用的图形用户界面来设置你的 GFS 文件系统。你可以选择锁定和隔离方法以及挂载点和设备。然后你使用 `ccs_test` 工具测试配置。

```bash
ccs_test mygfs
```

然后你使用 `ccs_tool` 创建 `cluster.ccs`、`fence.ccs` 和 `node.ccs` 配置文件。这些文件被组织成一个 CCS 归档，放置在每个节点和集群设备上。

在每个节点上，你随后启动 `ccsd` 配置、`fenced` 隔离服务器以及你想使用的锁定方法，例如 `dlm`。有关锁定服务器的详细信息，请查阅相应的手册页。你可以使用前面提到的服务脚本来启动这些服务器。

要在集群设备上创建新文件系统，你使用 `gfs2_mkfs` 命令，然后使用 `-t gfs2` 选项挂载它们。以下命令在 `/dev/vg0/mgfs` 上创建 GFS 文件系统，然后将其挂载到 `/mgfs` 目录。对于 `gfs2_mkfs`，`-t` 选项指示使用的锁定表，`-p` 选项指定锁定协议，`-j` 选项指定日志数量。

```bash
gfs2_mkfs -t mycluster:mgfs -p lock_dlm -j 2 /dev/vg0/mgfs
mount -t gfs2 /dev/vg0/mgfs /gfs1
```

要让 `gfs` 服务脚本替你挂载 GFS 文件系统，你需要在 `/etc/fstab` 文件中为其添加一个条目。如果你不希望文件系统自动挂载，请添加 `noauto` 选项。

```bash
/dev/vg0/mgfs /mgfs gfs2 noauto,defaults 0 0
```

借助 `/etc/fstab` 中的 GFS 条目，你可以使用 `gfs2` 脚本挂载 GFS 文件系统。

```bash
service gfs start
```

### GFS 工具

GFS 具有不同类别的多个命令，例如处理隔离的 `fence_node`，管理 gulm 锁定的 `gulf_tool`，以及用于配置的 `ccs_tool` 等。用于管理 GFS 文件系统的 GFS 命令列于表 38-4 中。有关详细描述，请查阅它们各自的手册页。

### GFS 文件系统操作

GFS 具有不同类别的多个命令，例如处理隔离的 `fence_tool`，管理 gulm 锁定的工具，用于配置的 `ccs_tool`，以及用于集群管理的 `cman_tool` 等。几个 GFS 命令用于管理文件系统，例如用于挂载文件系统的 `gfs2_mount`，用于创建 GFS 文件系统的 `gfs2_mkfs`，用于检查和修复的 `gfs2_fsck`，以及用于扩展文件系统的 `gfs2_grow`。有关详细描述，请查阅它们各自的手册页。

> 注 对于 GFS 1，你使用不带数字 2 的 GFS 工具名称，用 `gfs` 代替 `gfs2`。

要挂载 GFS 文件系统，你使用指定 `gfs2` 为挂载类型的 `mount` 命令，如下所示：

```bash
mount -t gfs2 /dev/vg0/mgfs /mgfs
```
