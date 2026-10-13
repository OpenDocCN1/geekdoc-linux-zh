
注意，你可以运行 `exportfs` 命令配合 `-i` 选项指定要导出的资源，而无需向 `/etc/exports` 文件添加条目。通过这种方式资源将保持导出状态，直到手动取消导出或重启服务器。例如，要使用上述选项导出 `/usr/share/main`，请运行命令：

```
# exportfs -o ro,sync -i rhel03:/usr/share/main rhel04:/usr/share/main
```

导出资源时常用的选项如表 26-5 所示。

| 选项 | 描述 |
| --- | --- |
| `*` | 代表所有匹配。在上面的示例中，`*` 表示任何客户端都可以导出该资源，`*geticertify.com` 表示 getertify.com 域上的任何客户端系统都可以挂载该资源。你可以指定一个或多个主机名、IP 地址、域名或网络地址。 |
| `all_squash` / `no_squash` (default=`no_squash`) | `all_squash` 将客户端系统上的用户视为匿名用户，而 `no_squash` 则不是。 |
| `gid=GID`(default=6534) | 将 GID 分配给匿名组。 |
| `uid=UID`(default=6534) | 将 UID 分配给匿名用户。 |
| `mp` | 仅当指定的目录是文件系统时导出。 |
| `root_squash` / `no_root_squash` (default=`root_squash`) | `root_squash` 通过将 NFS 客户端上的 root 用户映射为 UID 为 65534 的特殊无权限用户 nobody 来防止其获取挂载资源的 root 权限。`no_root_squash` 允许 root 访问。建议使用默认值以防止客户端未经访问。 |
| `rw` / `ro` (default=`ro`) | `rw`（读/写）允许修改文件，`ro`（只读）禁止。 |
| `secure` / `insecure` (default=`secure`) | `secure` 允许访问小于 1024 的端口，`insecure` 允许访问超过 1024 的端口。 |
| `secure_locks` / `insecure_locks` (default=`secure_locks`) | `secure_locks` 检查旧版 NFS 客户端的文件权限，`insecure_locks` 则不检查。 |
| `subtree_check` / `no_subtree_check` (default=`no_subtree_check`) | 启用或禁用对导出资源上级目录的权限检查。 |
| `sync` / `async` (default=`sync`) | 更改在命令完成后写入磁盘。 |

表 26-5 选项

## 使用 NFS 配置器配置 NFS 服务器

要使用 Red Hat 配置器配置 NFS 服务器，请按照以下步骤操作：

1. 在终端中执行 `system-config-nfs` 或选择（GNOME 系统 / (KDE 主菜单 -> 系统 -> NFS)）。NFS 配置器将如图 26-1 所示打开。`Add` 按钮允许你导出新资源，`Server Settings`（图 26-2）允许你定义用于 NFS 守护的任何特定端口，而不是预定义的端口。

2. 有三个选项卡——`Basic`（基础）、`General Options`（常规选项）和 `User Access`（用户访问）——主界面。`Basic` 选项卡用于输入要导出的资源名称、服务器的主机名或 IP 地址、要出的域名或网络（或使用 `*` 表示所有主机）以及权限。`General Options` 和 `User Access` 选项卡允许你修改表 26-5 中列出的某些选项。在 `Basic` 选项卡中指定资源名称 `/usr/share/main` 导出到 `rhel03` 和 `rhel04`。将其他选项卡中的选项保持默认值。完成后点击 `OK`。系统使用带有 `-option` 的 `exports` 命令导出资源。见图 26-3。

## NFS 与自动

### 配置 NFS 客户端

成功配置 NFS 客户端的步骤如下：

1. 在 NFS 服务器上执行以下命令以确定可导出资源：

```bash
# showmount -e
rhel02 的导出列表：
/var/opt *
/usr/local/bin *
/home *.geticertify.com
/usr/share/man rhel03,rhel04
```

或者，使用 `exports` 命令对 `/var/lib/nfs/etab` 文件执行 `cat`：

```bash
# exportfs
/usr/share/man rhel03
/usr/share/man rhel04
/home *.geticertify.com
/usr/local/bin <rw>
/var/opt <rw>
# cat /var/lib/nfs/etab
/usr/share/man rhel03(ro,sync,wdelay,hide,nocrossmnt,secure,root_squash,no_all_squash,no_subtree_check,secure_locks,acl,mapping=identity,anuid=65534,ongid=6534)
/usr/share/man rhel04(ro,sync,wdelay,hide,nocrossmnt,secure,root_squash,no_all_squash,no_subtree_check,secure_locks,acl,mapping=identity,anuid=65534,ongid=6534)
/home *(rw,sync,wdelay,hide,nocrossmnt,secure,root_squash,no_all_squash,no_subtree_check,secure_locks,acl,mapping=identity,anuid=65534,ongid=6534)
/usr/local/bin *(rw,sync,wdelay,hide,nocrossmnt,secure,root_squash,no_all_squash,no_subtree_check,secure_locks,acl,mapping=identity,anuid=65534,ongid=6534)
/var/opt *(rw,sync,wdelay,hide,nocrossmnt,secure,root_squash,no_all_squash,no_subtree_check,secure_locks,acl,mapping=identity,anuid=65534,ongid=6534)
```

```
# service portmap start
Starting [ OK ]
# service nfslock start
Starting NFS stat: [ OK ]
```

5. 编辑 `/etc/fstab` 并为资源添加以下条目。这样做是为了确保客户端重启时 NFS 资源能够自动挂载。

```bash
rhel02:/usr/share/man    /usr/share/man nfs  ro,sync      0 0
rhel02:/home               /home           nfs  rw,sync      0 0
rhel02:/var/opt            /var/opt        nfs  rw,sync      0 0
rhel02:/usr/local/bin      /usr/local/bin nfs  rw,sync      0 0
```

6. 如果挂载点不存在，请使用 `mkdir` 命令创建所需的挂载点。

7. 使用 "-at nfs" 选项执行 `mount` 命令以挂载所有远程资源：

```bash
# mount -at nfs
```

或者，你可以通过三种方法手动挂载资源。对每个资源重复下面的第一个命令并使用 `-o sync` 指定正确的选项，运行第二个命令从 `/etc/fstab` 文件中获取额外信息，或者执行第三个命令挂载 `/etc/fstab` 文件列出的所有配置 NFS 资源：

```bash
# mount -t nfs -o ro,sync rhel02:/usr/share/man /usr/share/man
# mount /usr/share/man
# service netfs start
Mounting other filesystems: [ OK ]
```
