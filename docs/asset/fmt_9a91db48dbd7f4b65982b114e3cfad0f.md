
示例 3-17 列虚拟 SCSI 适配器

```
$ lsdev -virtual status description
ent3 Available Virtual I/O Ethernet Adapter (1-lan)
vhost0 Available Virtual SCSI Server Adapter
vhost1 Available Virtual SCSI Server Adapter
vhost2 Available Virtual SCSI Server Adapter
vhost3 Available Virtual SCSI Server Adapter
vhost4 Available Virtual SCSI Server Adapter
vhost5 Available Virtual SCSI Server Adapter
vhost7 Available Virtual SCSI Server Adapter
vhost8 Available Virtual SCSI Server Adapter
vhost9 Available Virtual SCSI Server Adapter
vhost10 Available Virtual SCSI Server Adapter
vsa0 Available LPAR Virtual Serial Adapter
```

- 3. 使用`lsmap -all`命令检查每个虚拟 SCSI 适配器的槽位号，如示例 3-18 所示。如果设备不可用，则定义时出现问题。您可以对每个设备使用`rmdev -dev vhostx-recursive`命令，并在需要时重启 VIOS。重启后，配置管理器将检测硬件并重新创建主机设备。

示例 3-18 虚拟 SCSI 槽位号

```
$ lsmap -all grep vhost
vhost0 U9124.720.10018EA-V1-C13 0x00000002
vhost1 U9124.720.10018EA-V1-C14 0x00000003
vhost2 U9124.720.10018EA-V1-C15 0x00000004
vhost3 U9124.720.10018EA-V1-C16 0x00000005
vhost4 U9124.720.10018EA-V1-C17 0x00000006
vhost5 U9124.720.10018EA-V1-C18 0x00000007
vhost7 U9124.720.10018EA-V1-C20 0x00000009
vhost8 U9124.720.10018EA-V1-C21 0x0000000a
vhost9 U9124.720.10018EA-V1-C22 0x0000000b
vhost10 U9124.720.10018EA-V1-C23 0x00000009
```

在我们的示例配置中，我们在`hdisk2`上创建了名为`rootvg_clients1`的卷组，并在`hdisk3`上创建了`rootvg_clients2`，并对其进行分区以为我们的五个 Linux 客户端分区提供启动磁盘。注意，`hdisk2`和`hdisk3`的大小均为 73 GB，受 RAID-5 保护，我们在 SPT 系统计划的每个 Linux 启动设备上分配了 10 GB。

> **重要：** 我们不建议将 VIOS `rootvg` 用于虚拟客户端磁盘（逻辑卷）。

- 4. 使用`mkvg`命令创建卷并将`hdisk2`分配给`rootvg_clients`，如示例 3-19 所示。

示例 3-19 为客户端分区创建 rootvg_clients

```
$ mkvg -vg rootvg_clients1 hdisk2
rootvg-clients1
$ mkvg -vg rootvg_clients2 hdisk3
rootvg-clients2
```

- 5. 定义所有将作为 hdisk 呈现给客户端分区的逻辑卷。在案例中，这些逻辑卷将是客户端分区的`rootvg`，如示例 3-20 所示。

示例 3-20 创建逻辑卷

```
$ mklv -lv rootvg_mgmt rootvg_clients1 10G
rootvg_mgmt
$ mklv -lv rootvg_dns rootvg_clients1 10G
rootvg_dns
$ mklv -lv rootvg_dhcp rootvg_clients1 10G
rootvg_dhcp
$ mklv -lv rootvg_firewall rootvg_clients1 10G
rootvg_firewall
$ mklv -lv rootvg_web rootvg_clients1 10G
rootvg_web
$ mklv -lv rootvg_database rootvg_clients1 10G
rootvg_database
$ mklv -lv rootvg_file rootvg_clients2 10G
rootvg_file
$ mklv -lv rootvg_print rootvg_clients2 10G
rootvg_print
$ mklv -lv rootvg_email rootvg_clients2 10G
rootvg_email
$ mklv -lv rootvg_data_file rootvg_clients2 10G
rootvg-data_file
```

- 6. 定义 SCSI映射以创建与上一步定义的逻辑卷关联的虚拟设备。根据示例 3-18，我们在 VIOS 上有 10 个虚拟设备。这些就是我们要映射到逻辑卷的设备。

示例 3-21 创建虚拟映射

```
$ mkdev -vdev rootvg_mgmt -adapter vhost0 -dev vmgmt
vmgmt Available
$ mkdev -vdev rootvg_dns -adapter vhost1 -dev vns
vns Available
$ mkdev -vdev rootvg_dhcp -adapter vhost2 -dev dhcp
dhcp Available
$ mkdev -vdev rootvg_firewall -adapter vhost3 -dev firewall
firewall Available
$ mkdev -vdev rootvg_web -adapter vhost4 -dev web
web Available
$ mkdev -vdev rootvg_database -adapter vhost5 -dev database
database Available
$ mkdev -vdev rootvg_file -adapter vhost7 -dev file
file Available
$ mkdev -vdev rootvg_print -adapter vhost8 -dev print
print Available
$ mkdev -vdev rootvg_email -adapter vhost9 -dev email
email Available
$ mkdev -vdev rootvg_data_file -adapter vhost10 -dev data_file
data_file Available
```

示例 3-22 列虚拟设备
