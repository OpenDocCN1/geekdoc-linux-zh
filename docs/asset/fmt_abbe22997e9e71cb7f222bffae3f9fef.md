
| CFS Server | Mount Point | File System | FS Type |
|------------|-------------|-------------|---------|
| `molari` | `/cluster/members/member1/ boot_partition` | `root1_domainroot` | AdvFS |
| `molari` | `/fafax` | `tcshbafax` | AdvFS |
| `sheridan` | `/` | `cluster_rootroot` | AdvFS |
| `sheridan` | `/usr` | `cluster_sher/usr` | AdvFS |
| `sheridan` | `/var` | `cluster_var/var` | AdvFS |
| `sheridan` | `/kits` | `extrakits` | AdvFS |
| `sheridan` | `/u1` | `home/u1` | AdvFS |
| `sheridan` | `/cluster/members/member2/ boot_partition` | `root2_domainroot` | AdvFS |

这怎么可能？嗯，CFS 服务器将 I/O 请求发送到 DRD。CFS 从未看到错误，因为 DRD 通过自动重新路由分派请求的处理方式解决了问题。DRD 感知到它不能再使用正在使用的访问成员，因此它从设备的服务器列表中获取了新的访问成员。

在我们重新连接电缆后，DRD 几乎立即再次注意到设备。检查其中一个设备的路径，我们看到：

```
[sheridan]
# drdmgr -a check_path dsk1

截至 2001-07-24:00:42:42 来自成员 sheridan 的数据视图

设备名称：dsk1
本地设备路径：Exists
```

路径已恢复。`sheridan` 上的 DRD 也再次在本地提供磁盘服务。

```
[sheridan]
# drdmgr -a server -a accessnode dsk1 dsk3

截至 2001-07-24:00:42:53 来自成员 sheridan 的数据视图

设备名称：dsk1
设备类型：Direct Access IO Disk
设备状态：OK
服务器数量：2
服务器名称：molari
服务器状态：Server
服务器名称：sheridan
服务器状态：Server
访问成员名称：sheridan

Device Name: dsk3

Device Type: Direct Access IO Disk

Device Status: OK

Number of Servers: 2

  Server Name: molari

  Server State: Server

  Server Name: sheridan

  Server State: Server

Access Member Name: sheridan
```

我们只是重新连接了电缆——其余工作由 DRD 自动且透明地完成。这真是令人难以置信的东西！

## 15.4 DRD 事件

DRD 事件定义在 `/usr/share/evm/templates/clu/drd.evt` 模板文件中。以下是已注册的 DRD 事件。

```
# evmwatch -A -i -f "[name *.drd]" -t "[@priority] @name"

[200] sys.unix.clu.drd.server_add

[200] sys.unix.clu.drd.server_leave

[200] sys.unix.clu.drd.new_accessnode

[300] sys.unix.clu.drd.no_accessnode
```
