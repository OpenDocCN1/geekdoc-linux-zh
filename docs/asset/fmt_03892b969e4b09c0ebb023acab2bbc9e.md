
`-t` 选项显示单个文件系统类型。使用 `nfs4` 参数时，它会显示 NFS 目录层次结构：

| df -ht nfs4 | Size Used Avail Use% | Mounted on |

|---|---|---|---|---|

| plum:/home/zach | 37G | 2.3G | 35G | 7% | /home/zach |

安全性
默认情况下，NFS 服务器使用 `AUTH_SYS`（第 793 页）认证，该认证基于受信任主机范式（第 382 页），所有基于此范式的其他服务都受到安全缺陷的困扰。此外，这种模式下的 NFS 文件传输是不加密的。由于这些问题，你应该只在单个局域网段上实现 NFS，在那里你可以（合理地）确定局域网段上的设备确实如它们所称。确保防火墙阻止来自局域网外部的 NFS 流量，永远不要在互联网上使用 NFS。为了提高安全性，确保服务器和客户端上的 UID 和 GID 相同（第 807 页）。

或者，你可以使用 `RPCSEC_GSS`（第 793 页）认证，这是 NFSV4 提供的新安全功能之一。`RPCSEC_GSS` 提供认证、验证和加密。本章将涵盖如何设置使用 `RPCSEC_GSS` 认证的 NFS 服务器。

### 更多信息

- Web NFSV4 主页：www.nfsv4.org
- NFSV4 安全安装教程：nfsv4.bull.opensource.org/doc/kerbernfs/krbnfs_howto_v3.pdf
- 主要是带有 NFSV4 信息的 NFSV3：nfs.sourceforge.net
- NFSV4 信息：www.citm.umich.edu/projects/nfsv4
- 更新 NFSV4 信息（包括文档）：http://wiki.linux-nfs.org
- GSS-API：www.nfs.org/faq/kerberos-faq/general/section-84.html
- PXE 启动服务器教程 (TFTP)：wiki.alteee.com/php/Setting_Up_A_PXE_Server_in_Fedora
- autofs 教程：www.linuxq.com/issue24/nielsen.html

本地页面：`autofs`（第 5 和 8 节），`autom`, `auto.master`, `exports`, `mountstats`, `nfs`（特别参见 SECURITY CONSIDERATIONS），`rpc.idmapd`, `rpc.gssd`, `rpc.mount`, `rpc.nfsd`, 以及 `showmount`

NFS HOWTO：now.sourceforge.net/nfs-howto

《NFS Illustrated》，Callahan 等, Addison-Wesley (1990年1月)

# 运行 NFS 客户端

本描述了如何设置 NFS 客户端、挂载目录层次结构以及提高 NFS 性能。错误列表和故障排除参见第 810 页。

## 796 第 22 章 NFS：共享目录层次结构

### 先决条件

安装以下软件包：

- `nfs-utils`
- `rpcbind`（随 `nfs-utils` 安装）

### rpcbind 初始化

运行 `chkconfig` 以在系统进入多用户模式时启动 `rpcbind` 守护进程：

```
# chkconfig rpcbind
```

启动 `rpcbind` 守护进程：

```
# service rpcbind start
```

## 挂载远程目录

要设置 NFS 客户端，以与挂载本地目录结构相同的方式挂载远程目录层次结构（第 520 页）。以下示例显示了挂载远程目录层次结构的两种方法，假设 `dog` 与本地系统在同一网络上，并与本地系统共享 `/home` 和 `/export`。`dog` 上的 `/export` 目录包含两个你想挂载的层次结构：`/export/progs` 和 `/export/oracle`。首先在（客户端）系统中运行 `mkdir` 来创建作为远程目录层次结构挂载点的目录：

```
# mkdir /dog.home /apps /oracle
```

你可以挂载任何目录层次结构，假设 `dog` 与本地系统在同一网络上，并与本地系统共享 `/home` 和 `/export`。`dog` 上的 `/export` 目录包含两个你想挂载的层次结构：`/export/progs` 和 `/export/oracle`。首先在（客户端）系统中运行 `mkdir` 来创建作为远程目录层次结构挂载点的目录：

```
# mkdir /dog.home /apps /oracle
```

你可以挂载任何导出的目录层次结构。在该示例中挂载 `/dog.home`、`/apps` 和 `/oracle`。以下命令手动挂载目录层次结构：

```
# mount dog:/home /dog.home
# mount -o ro,nosuid dog:/export /apps
# mount -o ro dog:/export /oracle
```

默认情况下，这些目录层次结构以读写方式挂载，假设 NFS 服务器正在导出它们。前面的命令挂载了目录层次结构。使用 `-ro` 选项强制以只读挂载。

### nosuid 选项

如果用户拥有挂载目录层次结构权限，，该命令挂载了 `/dog.home`。使用 `nosuid` 选项可以限制用户对挂载目录层次结构的执行权限（第 205）。

## 运行 NFS 客户端 797

### ndev 选项

挂载设备会产生另一个安全漏洞。最佳策略是不挂载不可信任的目录层次结构，除非用户需要使用设备层次设备。

### fstab 文件

如果你频繁挂载目录层次结构，可以将其添加到 `/etc/stab`（第 801 页）。或者，你可以使用 `mountpoint`（第 811 页）。以下 `/etc/stab` 条与之前的示例所示：

```
$ cat /etc/stab
```

| ... | | | |

|---|---|---|---|

| dog:/home | /dog.home | nfs4 | rw | 0 0 |

| dog:/export/progs | /apps | ro,nosuid | 0 0 |

| dog:/export/oracle | /oracle | nfs4 | ro | 0 |

使用 NFS 的文件始终位于本地系统，无论其类型是什么。通常不对 NFS 目录层次结构运行 `fsck` 或进行备份。`fstab` 中的第三列、第五列和第六列通常是 `nfs`（文件系统类型）、`0`（在该目录层次结构上运行 `fsck`）。挂载 NFS 目录层次结构的选项与挂载 `ext4` 或其他类型的文件系统不同。详情请参见 `mount` 章节（下）。

### 卸载层次结构

使用与卸载本地文件系统相同的方法卸载远程目录层次结构（第 523 页）。

## mount: 目录层次结构

`mount` 工具（第 520 页）将目录层次结构与挂载点（目录）关联。你可以使用 `mount` 挂载 NFS（远程）目录层次结构。本节介绍了 `mount` 选项。它列出了默认选项，随后是非默认选项（括号内）。你可以在命令行中使用这些选项，或在 `/etc/stab`（第 801 页）中设置。有关选项的完整列表，请阅 `mount` 和 `man` 页面。

以下是两个挂载远程目录层次结构的示例。都是将 `plum` 系统的 `/home/public` 目录挂载到本地系统的 `/home.public` 挂载点。当不带参数调用时，`mount` 会显示已挂载的文件系统列表，包括挂载时使用的选项。

第一个 `mount` 命令在不指定选项的情况下挂载远程目录。第二个 `mount` 命令的输出（列出挂载的文件系统）通过管道发送给 `grep`，`grep` 显示了（非常长的）逻辑行

提供了关于远程挂载目录的信息。所有以 `rw`（读写）开头的选项均为默认值或由 `mount` 命令指定的。

```bash
# mount /home/public /plum.public
# mount | grep plum
plum:/home/public on /plum.public type nfs4 (rw,relatime,vers=4,rsize=13102,wsize=13102,namen=255,hard,proto=tcp,port=0,time=600,retrans=2,sec,clientaddr=172.16.192.150,minversion=0,local_lock=none,addr=172.16.192.151)
# umount /plum.public
```

下一个 `mount` 命令通过指定 `noac` 选项监控远程目录；下一个 `mount` 命令的输出显示添加了 `noac` 选项。当你指定 `noac` 时，`mount` 会添加 `acregmin`、`acdirmax`、`acdirmin` 选项（均将它们设置为 0）。
