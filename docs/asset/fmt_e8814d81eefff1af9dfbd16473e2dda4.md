
```bash
da10:~ # /etc/init.d/o2cb configure
Configuring the O2CB driver.
This will configure the on-boot properties of the O2CB driver.
...
Load O2CB driver on boot (y/n) [y]: <ENTER>
Cluster to start on boot (Enter "none" to clear) [mycluster]: <ENTER>
Use user-space driven heartbeat? (y/n) [n]: <ENTER>
Writing O2CB configuration: OK
```

## 7. 自动启动存储集群服务

以下命令在 `/etc/init.d/rc*.d/` 中创建链接，以便在启动时启动服务。

```bash
da10:~ # chkconfig -a o2cb
da10:~ # chkconfig -a ocfs2
```

## 8. 手动启动 OCFS2 集群服务并挂载 OCFS2

以下命令启动 `ocfs2` 所需的服务：

```
dal0:~ # /etc/init.d/o2cb start;
Loading module "configfs": OK
Mounting configfs filesystem at /sys/kernel/config: OK
Loading module "ocfs2_nodemanager": OK
Loading module "ocfs2_dlm": OK
Loading module "ocfs2_dlmfs": OK
Mounting ocfs2_dlmfs filesystem at /dlm: OK
Starting cluster mycluster: OK
dal0:~ # /etc/init.d/ocfs2 start
Starting Oracle Cluster File System (OCFS2)     done
```

第二个命令挂载文件系统。使用命令 `mount` 查看结果。

## 9. 检查集群文件系统是否正常工作

```
dal0:~ # cat
/sys/kernel/config/cluster/mycluster/heartbeat/dead_threshold
7
```

## 10. 手动停止 OCFS2 集群服务并卸载 OCFS2

以下命令停止 OCFS2 集群服务：

```
dal0:~ # /etc/init.d/ocfs2 stop;
Stopping Oracle Cluster File System (OCFS2)     done
dal0:~ # /etc/init.d/o2cb stop;
Cleaning heartbeat on mycluster: OK
Stopping cluster mycluster: OK
Unloading module "ocfs2": OK
Unmounting ocfs2_dlmfs filesystem: OK
Unloading module "ocfs2_dlmfs": OK
Unmounting configfs filesystem: OK
Unloading module "configfs": OK
```

你还应熟悉图形化的 OCFS2 前端 `ocfs2 console`，它允许管理 OCFS2 的各个方面。

![](img/63e88022bf135307e3eac051ad238b5b_443_0.png)

![](img/63e88022bf135307e3eac051ad238b5b_443_1.png)

# OCFS 到 OCFS2 的迁移

OCFS 和 OCFS2 的磁盘布局不兼容。由于 OCFS 的驱动仅适用于 2.4.x Linux 内核，而 OCFS2 的驱动仅适用于 2.6.x Linux 内核，因此你无法在同一台机器上同时使用两者。

有两种可能性可以迁移到新的 OCFS2：

- 如果旧的集群文件系统仍然在线，你可以通过网络将其复制到新系统。你必须确保在最后一次复制之后，旧的 OCFS 存储集群没有任何更改；在迁移期间你需要双倍的 SAN 容量。

- Oracle 提供了 FSCat 工具，可以在用户空间读取 OCFS 磁盘镜像。使用这些工具在 OCFS2 集群节点上，你可以将 OCFS 备份提取到 OCFS2 挂载点。

## GFS - OCFS2 对比表

| 特性 | GFSv1 6.1 | OCFS2 1.2.3 |
|---|---|---|
| 发布日期 | 2006-08 (v1.0 1996) | 2006-07 (v1.0 2005) |
| Linux 内核包含情况 | 内核树外 | 2.6.16 |
| CPU 架构 | x86, x64, ia64 | x86, x64, ia64, ppc, ppc64 |
| 最大支持节点数 | 256 | 255 |
| 最大文件名长度 | 255 | 255 |
| 最大路径长度 | 无限制 | 无限制 |
| 块大小 | 512 B - 4 KB | 512 B - 4 KB |
| 集群大小 | - | 4 KB - 1 MB |
| 最大文件大小 | 2 TB / 16 TB / 8 EB | 4 TB / 16 TB / 4 PB |
| 最大文件系统大小 | 2 TB / 16 TB / 8 EB | 4 TB / 16 TB / 4 PB |
| 卷管理器 | LVM2 + CLVM | LVM2, EVMS |
| 锁管理器 | GULM, 内核 DLM | OCFS2 DLM |
| 集群管理器 | CMAN | O2CB (NM+HB+TCP) |
| 共享块设备 | GNBD, FC, iSCSI | FC, iSCSI |
| 在线/离线调整大小 | 增长/- | -/- |
| 用户/组配额 | 是/是 | -/- |
| 多路径 | 是 | 是 |
| 直接 I/O | 是 | 是 |

### 练习 10-1

## 设置 OCFS2

本练习的目的是让你熟悉 OCFS2。

本练习基于上一练习“设置 iSCSI 目标和 iSCSI 启动器”（第 9-23 页）。

你可以在练习册中找到本练习。

*(练习结束)*

### 总结

| **目标** | **总结** |
| --- | --- |
| 1. | 全局文件系统 (GFS)<br>在 RHEL 下，主要使用 GFS（全局文件系统）作为集群文件系统。 |
| 2. | Oracle 集群文件系统 2 (OCFS2)<br>OCFS2 是 SUSE Linux Enterprise Server 10 下使用的集群文件系统。<br>配置包含在 `/etc/ocfs2/cluster.conf` 中；创建文件系统的程序是 `mkfs.ocfs2`。<br>集群功能由服务 `o2cb` 和 `ocfs2` 提供。 |

# 第 A 部分

## 附录：AutoYaST

本节说明了如何使用 SUSE Linux Enterprise Server 10 的 AutoYaST 功能执行自动安装。

AutoYaST 便于大量机器的部署。安装由一个 XML 文件控制，该文件包含特定于机器的信息，例如 IP 地址、主机名、分区等。安装过程中无需手动干预。

安装通过 CD、启动软盘或支持 PXE 的网络网卡启动。

安装源可以是 CD 集合，也可以是网络中的安装服务器。访问安装服务器上的存储库所支持的协议为 NFS、HTTP 和 FTP。

### 目标

- 自动安装基础知识
- 设置安装服务器
- 为 AutoYaST 创建配置文件
- 启动安装

### 目标 1

## 自动安装基础知识

Red Hat 和 SUSE Linux Enterprise Server 10 都提供了一种自动化的安装方式：

- RHEL4 上的 Kickstart
- SUSE Linux Enterprise Server 10 上的 AutoYaST

### RHEL4 上的 Kickstart

Red Hat 使用 anaconda 工具进行安装。如果你自动设置安装，这被称为 kickstart 环境。

kickstart 配置文件是一个常规文本文件，其中包含对安装问题的回答，每行一条。

安装 Red Hat 系统时，会在 root 用户的 home 目录 (`/root`) 中创建一个 kickstart 配置文件 `anaconda-ks.cfg`。此文件包含你在安装期间输入的设置。在使用它之前，你必须取消包含分区设置的那些行的注释。
