
+ 1 个驱动器：

| DriveName | State: up | /dev/ad0s1h | A: 0/69876 MB (0%) |
| :--- | :--- | :--- | :--- | :--- |
| V root | State: up | Plexes | 1 Size | 511 MB |
| V swap | State: up | Plexes | 1 Size | 4070 MB |
| V var | State: up | Plexes | 1 Size | 3059 MB |
| V tmp | State: up | Plexes | 1 Size | 1024 MB |
| V usr | State: up | Plexes | 1 Size | 61210 MB |

5 个卷：

| P root.p0 | C State: up | Subdis | 1 Size | 511 MB |
| :--- | :--- | :--- | :--- | :--- |
| P swap.p0 | C State: up | Subdis | 1 Size | 4070 MB |
| P var.p0 | C State: up | Subdis | 1 Size | 3059 MB |
| P tmp.p0 | C State: up | Subdis | 1 Size | 1024 MB |
| P usr.p0 | C State: up | Subdis | 1 Size | 61210 MB |
| P root.p1 | C State: faulty | Subdis | 1 Size | 511 MB |
| P swap.p1 | C State: faulty | Subdis | 1 Size | 4070 MB |
| P var.p1 | C State: faulty | Subdis | 1 Size | 3059 MB |
| P tmp.p1 | C State: faulty | Subdis | 1 Size | 1024 MB |
| P usr.p1 | C State: faulty | Subdis | 1 Size | 61210 MB |

## 使用 RAID 和 Vinum 增强磁盘性能

5 个子磁盘：
- S root.p0.s0 State: up D: DriveName Size: 511 MB
- S swap.p0.s0 State: up D: DriveName Size: 4070 MB
- S var.p0.s0 State: up D: DriveName Size: 3059 MB
- S tmp.p0.s0 State: up D: DriveName Size: 1024 MB
- S usr.p0.s0 State: up D: DriveName Size: 6120 MB
- S root.p1.s0 State: stale D: Drive2 Size: 511 MB
- S swap.p1.s0 State: stale D: Drive2 Size: 4070 MB
- S var.p1.s0 State: stale D: Drive2 Size: 3059 MB
- S tmp.p1.s0 State: stale D: Drive2 Size: 1024 MB
- S usr.p1.s0 State: stale D: Drive2 Size: 6120 MB

在另一个终端中，检查 `/dev` 内部是否存在名为 `usr`、`var`、`tmp` 的虚拟目录及其设备。这些就是你的新磁盘设备。你可以使用 `fsck -n - ufs /dev/vinum/root` 命令（以及针对其他驱动器设备的类似命令，排除交换分区）来检查虚拟驱动器是否工作正常。你应该会在子磁盘部分看到列出的所有驱动器名称，显示每个磁盘对每个卷的独立贡献。（这是一个镜像设置，因此每个卷的大小不会增加——它只会提高其可靠性。）

> 提示
你现在需要配置 `/etc/fstab` 以使用新的磁盘设备（例如，使用 `/dev/vinum/usr` 而不是 `/dev/ad0sif`）。

现在，你需要将每个原始分区的数据拷贝到每个卷的新子磁盘中。在 `gvinum` 中，为标记为 `State: stale` 的每个子磁盘发出 `start` 命令。

```bash
gvinum -> start root.p1.s0

GEOM_VINUM: sd root.p1.s0 is initializing

GEOM_VINUM: plex root.p1 is degraded
```
