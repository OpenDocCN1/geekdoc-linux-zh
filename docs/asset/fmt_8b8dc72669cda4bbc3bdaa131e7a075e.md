
更多的 `find` 示例可以在 `grep` 和 `xargs` 命令的描述中找到。

# 替代方案

`find` 是一个重要的命令，但它很难使用，因为没有人能记住所有可能的选项。因此，有很多尝试创建比 `find` 更方便的替代方案。我在书中介绍了其中两个：

- `erd` 将 `du`、`find`、`ls` 和 `tree` 最重要的功能合并到一个命令中。
- 另一方面，`fzf` 以其交互式文件选择见长。

另一个选项是 `fd`（访问 https://github.com/sharkdp/fd），它与 `find` 非常相似。它最大的优势是选项更容易记忆，并且搜索结果以彩色显示。

## findmnt [options] [device/mountpoint]

不带参数的 `findmnt` 会返回集成在目录树中的所有文件系统的树形列表。结果还包含各种 `/dev`、`/proc`、`/sys` 和 `/run` 文件系统用于内部信息交换。

通过指定设备或挂载点，列表将缩小为通过这种方式选择的文件系统。其他允许的条目是文件系统的 UUID 或名称（标签）或主从设备号。

- `-A` 显示所有文件系统。
- `-l` 以表格形式显示结果（而不是树形）。
- `--mtab` 或 `--fstab` 仅考虑 `/etc/mtab` 或 `/etc/fstab` 中的条目。默认情况下，`findmnt` 考虑 `/proc/self/mountinfo`。
- `-o columns` 或 `--output columns` 输出指定的列。列包括：
  `SOURCE`: 设备
  `TARGET`: 挂载路径
  `FTYPE`: 文件系统类型
  `OPTIONS`: 挂载选项
  `SIZE`: 文件系统大小
- `-t typelist` 或 `--types typelist` 仅返回指定类型的文件系统。使用 `-t ext2,ext3,ext4`，只考虑 2、3、4 版本的 ext 文件系统。

## 示例

`findmnt` 显示测试计算机上所有激活的文件系统：

## firewall-cmd 选项

`firewall-cmd` 读取或更改 Fedora、RHEL 和 SUSE 发行版的防火墙配置。`firewall-cmd` 与后台运行的 `fireld` 程序通信。该程序为每个网络接口分配区域（zone）。`fireld` 意义区域是特定用途的规则集合。以下列表描述了最重要的区域：

- `block` 阻塞所有流量；发送者接收 ICMP 消息。
- `drop` 阻塞所有流量；不通知发送者。
- `external` 阻塞大部分端口并激活伪装 (IPv4)。该区域用于连接互联网的接口。
- `FedoraWorkstation` 和 `FedoraServer` 是 Fedora 安装网络接口的默认区域。`FedoraServer` 阻塞 SSH 和 DHCP 客户端以外的所有服务。`FedoraWorkstation` 宽松得多，还接受 Samba 连接以及 1025 到 65535 所有端口的流量。
- `home` 和 `internal` 阻塞大部分端口，但接受 Samba（仅作为客户端）、CUPS、Zeroconf/Avahi/mdns。这些区域用于被认为安全的本地网络。如果你想使用此区域并自行共享 Windows 网络目录，还必须启用 Samba 服务。
- `public` 与 `home` 类似，但阻塞 CUPS 和 Samba 客户端功能。该区域用于不安全网络中的互联网使用，例如公共无线网络中。
- `trusted` 允许任何网络流量。该区域用于安全良好的本地网络，但不用于 Wi-Fi 连接。

通常，`firewall-cmd` 仅动态进行更改。如果更改是永久的，你必须指定 `--permanent` 选项。这样规则将保存在 `/etc/firewalld` 目录中。

- `--add-interface=name` 或 `--remove-interface=` 默认区域，
  将指定的接口分配给默认区域，分配由 `--zone` 选项指定的区域，或移除此分配。在将接口分配给新区域之前，必须显式地移除之前的分配！

- `--add-prot=name` 或 `--remove-port=name`
  允许在通过 `--zone` 指定的区域中使用 TCP 端口，或阻塞该端口。

- `--add-service=name` 或 `--remove-service=name`
  允许在通过 `--zone` 指定的区域中使用网络服务（例如 `https` 或 `ssh`），或阻塞该服务。

- `--change-interface=iface`
  将活动区域分配给指定的网络接口。若要将另一个区域连接到接口，你还必须传递 `--zone=name` 选项。

- `--get-active-zones`
  列出所有正在使用的区域，并指示哪些网络接口被分配到了这些区域。

- `--get-default-zone`
  确定默认区域。

- `--get-services`
  列出 `firewall-cmd` 知知的所有网络服务。你可以通过 `--add-interface` 指定结果名称（`http`, `ssh` 等）。

- `--get-zones`
  列出 `firewall-cmd` 知知的所有区域。

- `--get-zone-of-interface=name`
  确定分配给指定网络接口的区域。

- `--list-all-zones`
  提供所有定义的防火墙区域的关键数据，并指定哪些网络接口被分配到了区域。

- `--list-ports`
  列出当前活动防火墙区域中允许的（即未阻塞的）端口。警告：该命令仅返回未分配服务名称的端口。端口 22 永远不会出现在结果中，因为它被分配给了 `ssh` 服务。你可以通过 `--list-all-zones` 或 `--list-services` 选项获取未阻塞的服务。

- `--list-services`
  列出当前活动防火墙区域中允许的（即未阻塞的）所有网络服务。

- `--permanent`
  将更改永久保存到防火墙配置中。然而，更改不会直接生效。如果你想立即且永久地进行更改，必须运行相关命令*两次*：一次带有 `--permanent`，另一次不带该选项。

- `--set-default-zone=name`
  定义默认区域。它适用于所有未显式分配了不同区域的网络接口。

- `--zone=name`
  指示要更改、编辑或读取哪个区域。

## 示例

以下命令首先确定网络接口 `enp0s3` 被分配到哪个区域，然后将该接口分配到信任（`trusted`）区域。这意味着所有服务都可以通过此接口。这些更改不是永久的，因此它们仅在下次重启计算机或防火墙守护进程之前有效。

```
root# firewall-cmd --get-zone-of-interface=enp0s3

public

root# firewall-cmd --zone=public --remove-interface=enp0s3

success

root# firewall-cmd --zone=trusted --add-interface=enp0s3

success
```

在第二个示例中，第一个命令用于确定网络接口 `enp0s5` 被分配到哪个区域。该计算机旨在通过此接口向外部世界提供 Web 服务器。但是，并不是泛泛地将接口分配到信任区域并启用所有其他可能的的服务，而是永久地更改了该区域的规则（这里是 `FedoraWorkstation`）：该区域现在允许 HTTP 和 HTTPS 协议。`reload` 命令激活了区域的更改。

```
root# firewall-cmd --get-zone-of-interface=enp0s5

root# firewall-cmd --permanent --zone=FedoraWorkstation --add-service=http

root# firewall-cmd --permanent --zone=FedoraWorkstation --add-service=https

root# firewall-cmd --reload
```
