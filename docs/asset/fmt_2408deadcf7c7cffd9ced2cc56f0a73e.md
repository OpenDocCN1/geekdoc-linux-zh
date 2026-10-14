
```
[molari]
# export EVM_SHOW_TEMPLATE="@member_id [@priority] @name"
[molari]
# evmatch -A -f "[name *.scsi] [name *.drd] | [name *.cfs]"
2 [200] sys.unix.clu.drd.server_leave_hwid.50
2 [200] sys.unix.clu.drd.server_leave_hwid.53
2 [200] sys.unix.clu.drd.server_add_hwid.50
2 [200] sys.unix.clu.drd.new_accessnode_hwid.50
2 [200] sys.unix.clu.drd.new_accessnode_hwid.50
2 [200] sys.unix.clu.drd.server_leave_hwid.52
2 [200] sys.unix.clu.drd.server_add_hwid.53
2 [200] sys.unix.clu.drd.new_accessnode_hwid.53
2 [200] sys.unix.clu.drd.server_add_hwid.52
sys.unix.clu.drd.new_accessnode._hwid.52
sys.unix.clu.drd.new_accessnode._hwid.52
```

## 第 15 章

看起来来自 sheridan(member2) 的 DRD 检测到了问题。与在 sheridan 上看到的相比，我们在 molari 上只看到了少数几个事件。你问：“你的意思是 sheridan 没有挂起或崩溃吗？” 是的，sheridan 仍在运行。事实上，这是我们拔掉电缆时 sheridan 看到的内容：

```
[sheridan]
# export EVM_SHOW_TEMPLATE="@member_id [@priority] @name"
[sheridan]
# evmatch -A -f "[name *.scsi] [name *.drd] | [name *.cfs]"
2 [200] sys.unix.clu.drd.server_leave_hwid.50
2 [200] sys.unix.clu.drd.server_add_hwid.53
2 [200] sys.unix.clu.drd.new_accessnode_hwid.50
2 [200] sys.unix.clu.drd.new_accessnode_hwid.50
2 [200] sys.unix.clu.drd.server_leave_hwid.52
2 [200] sys.unix.clu.drd.binlog_hwsi.50
[200] sys.unix.clu.drd.binlog_hwsi
[400] sys.unix.clu.drd.binlog_hwsi

[200] sys.unix.clu.drd.binlog_hwsi.51
[400] sys.unix.clu.drd.binlog_hwsi.51
[400] sys.unix.clu.drd.binlog_hwsi.52
[400] sys.unix.clu.drd.binlog_hwsi.53
[400] sys.unix.clu.drd.binlog_hwsi.53
[400] sys.unix.clu.drd.binlog_hwsi.54
[400] sys.unix.clu.drd.binlog_hwsi.55
[400] sys.unix.clu.drd.binlog_hwsi.55

[200] sys.unix.clu.drd.server_add_hwid.53
[200] sys.unix.clu.drd.new_accessnode_hwid.53
[200] sys.unix.clu.drd.new_accessnode_hwid.53
[200] sys.unix.clu.drd.binlog_hwsi.50
[200] sys.unix.clu.drd.server_add_hwid.52
[200] sys.unix.clu.drd.new_accessnode_hwid.52
[200] sys.unix.clu.drd.new_accessnode_hwid.52
[200] sys.unix.clu.drd.binlog_hwsi.51
```

为了节省页面我们截断了输出，但正如你看到的，除了 DRD 事件外，sheridan 还看到了 SCSI 事件。考虑到它不再能看到几块磁盘，这并不意外。

使用 `hmmgr` 命令，看看我们还能看到哪些设备：

```
[sheridan]
# hmmgr -show scsi -bus 3
```

| SCSI | DEVICE | DEVICE DRIVER NUM DEVICE FIRST | HWID:DEVICEID HOSTNAME | TYPE | SUBTYPE OWNER PATH | FILE VALID PATH |
| --- | --- | --- | --- | --- | --- | --- |
| 50: 3 | sheridan disk | none 0 1 | | | | |
| 51: 4 | sheridan disk | none 2 1 | | | | |
| 52: 5 | sheridan disk | none 0 1 | | | | |
| 53: 6 | sheridan disk | none 0 1 | | | | |
| 54: 7 | sheridan disk | none 2 1 | | | | |
| 55: 8 | sheridan disk | none 2 1 | | | | |

如果你将此输出与断开电缆前收到的 `hmmgr` 命令输出进行比较，你会发现没有设备有效路径。

sheridan 上的 DRD 看到了什么？我们可以使用之前相同的 `drdmgr` 命令来查找：

```
[sheridan]
# drdmgr -a server -a accessnode dsk1 dsk3

View of Data from member sheridan as of 2001-07-27:24:00:27

Device Name: dsk1

Device Type: Direct Access IO Disk

Device Status: OK

Number of Servers: 1

Server Name: molari

Server State: Server

Access Member Name: molari

Device Name: dsk3

Device Type: Direct Access IO Disk

Device Status: OK

Number of Servers: 1

Server Name: molari

Server State: Server

Access Member Name: molari
```

通过上面的输出可以看出，molari 现在正在向 sheridan 提供数据。

好了，现在是真正的难题了：“哪个成员是 `cluster_root`、`cluster_usr`、`cluster_var` 和 sheridan 的 `boot_partition` 的 CFS 服务器？” 嗯，我们没有看到任何 CFS 事件。尽管 sheridan 不再能直接访问设备，它还能提供文件系统吗？你肯定的。

```
[sheridan]

# cfs

-------------------------------------------------------------

CFS Server           Mount Point               File System             FS Type

molari               /cluster/members/member1/ root1_domain#root AdvFS

                     boot_partition

                     fafrak                   tcrhb#fafrak      AdvFS

sheridan             /                         cluster_root#root AdvFS

sheridan             /usr                      cluster_usr#usr   AdvFS

sheridan             /var                      cluster_var#var    AdvFS
```
