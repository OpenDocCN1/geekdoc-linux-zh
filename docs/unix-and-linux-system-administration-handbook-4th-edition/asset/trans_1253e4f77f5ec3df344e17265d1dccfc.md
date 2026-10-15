

**表 18.10 身份映射守护进程和配置**

| 系统 | 守护进程 | 配置 |
|---|---|---|
| Linux | /usr/sbin/rpc.idmapd | /etc/idmapd.conf |
| Solaris | /usr/lib/nfs/nfsmapid | /etc/default/nfs* |
| HP-UX | /usr/sbin/nfsmapid | /etc/nfs* |
| AIX | /usr/sbin/nfsrgyd | chnfsdom domain |

a. 域在 NFSMAPID_DOMAIN 参数中设置。

要重启守护进程。诸如详细日志记录和 nobody 账户的替代管理等选项通常可用；请参阅特定守护进程的手册页。

## 18.6 NFSSTAT：转储 NFS 统计信息

nfsstat 显示 NFS 系统维护的各种统计信息。nfsstat -s 显示服务器端统计信息，而 nfsstat -c 显示客户端操作的统计信息。默认情况下，nfsstat 显示所有协议版本的统计信息。例如：

```
$ nfsstat -c

Client rpc:
calls  badcalls  retrans  badxid  timeout  wait  newcred  timers
64235  1595      0        3       1592    0      0        886

Client nfs:
calls  badcalls  nclget   nclsleep
62613  3        62643    0
null   getattr  setattr  readlink lookup  root   read
0%     34%     0%       21%      30%     0%     2%
write  wrcache  create   remove   rename  link   symlink
3%     0%      0%       0%       0%      0%     0%
mkdir  readdir  rmdir    fsstat   0%
0%     6%      0%       0%
```

此示例来自一个相对健康的 NFS 客户端。如果超过 3% 的 RPC 调用超时，则很可能 NFS 服务器或网络存在问题。您通常可以通过检查 badxid 字段来发现原因。如果 badxid 接近 0 而超时大于 3%，则数据包在网络上传输到服务器和从服务器传输时丢失。您可以通过降低 rsize 和 wsize 挂载参数（读写块大小）来解决此问题。

如果 badxid 几乎与超时一样高，则服务器有响应，但响应太慢。更换服务器或增加 timeo 挂载参数。

## 18.7 专用 NFS 文件服务器

快速、可靠的文件服务是生产计算环境的基本要素。虽然您当然可以从工作站和现成的硬盘中自建文件服务器，但这样做通常不是性能最佳或最易于管理的解决方案（尽管通常是最便宜的）。

专用 NFS 文件服务器已经存在多年。它们与自制方案相比具有许多潜在优势：

- 它们针对文件服务进行了优化，通常提供最佳的 NFS 性能。
- 随着存储需求的增长，它们可以平滑扩展以支持数 TB 的存储和数百个用户。
- 它们比独立设备更可靠，得益于简化的软件、冗余硬件以及使用磁盘镜像。
- 它们通常为 UNIX 和 Windows 客户端提供文件服务。大多数甚至包含集成的 Web、FTP 和 SFTP 服务器。
- 它们通常比 UNIX 文件服务器更容易管理。
- 它们通常包含备份和检查点功能，这些功能优于普通 UNIX 系统所提供的功能。

我们最喜欢的专用 NFS 服务器之一由 Network Appliance, Inc.（netapp.com）制造。他们的产品从非常小到非常大不等，价格也还可以。EMC 是高端服务器市场中的另一家厂商。他们制造的产品不错，但请做好承受价格冲击的准备，并提高对营销术语的耐受度。由 HP 拥有的 LeftHand Networks 是近年来在低成本、高性能入门级存储产品方面获得认可的另一家厂商。

存储区域网络（SAN）系统是网络上高性能存储管理的另一种选择。它们与专用文件服务器的不同之处在于它们对文件系统一无所知；它们只是提供磁盘块。因此 SAN 不受操作系统开销的限制，可提供快速的读写访问，但如果没有集群文件系统的帮助，就无法管理多个客户端的并发访问。有关 SAN 的更多信息，请参阅第 274 页。

## 18.8 自动挂载

通过在 /etc/fstab 或 /etc/vfstab 中列出它们来在启动时挂载文件系统，可能会在大型网络上造成几种管理上的麻烦。

首先，在数百台机器上维护 fstab 文件可能很繁琐，即使有脚本和配置管理系统帮助也是如此。每个主机可能有略微不同的需求，因此需要单独关注。

