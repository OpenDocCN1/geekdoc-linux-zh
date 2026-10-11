

## 全局文件系统 (GFS)

在 RHEL 中，主要使用 GFS 作为集群文件系统。GFS 是一个最初由明尼苏达大学开发的集群文件系统，后来由 Sistina Software 进行分发。Red Hat 于 2003 年底收购了 Sistina Software，并于 2004 年将其集群文件系统作为 GPL 许可下的开源软件发布。

用于 RHEL4 的 Red Hat 集群套件利用 GFS 6.1 作为共享存储，得益于其高吞吐量和高可用性特性，但它也可用于 Oracle Real Application Cluster (RAC) 并得到支持。

直到当前迭代版本 6.1 的所有版本在磁盘上是兼容的，并运行在 GFS 标签下。后继版本 GFS2 目前正在开发中，它将不再与 GFS(1) 在磁盘上兼容，但将消除其当前的一些注意事项。GFS2 最近已包含在 Linux 内核 2.6.19 的开发版本中；GFS1 是在树外开发的。

可以将 GFS 用作简单的本地文件系统，无需任何集群锁定机制，但通常它以集群模式运行，此时需要由 SAN 环境来补充。

SUSE Linux Enterprise Server 10 中不可用 GFS。

## Oracle 集群文件系统 2 (OCFS2)

本目标涵盖

- OCFS2 背景
- OCFS2 配置
- 从 OCFS 到 OCFS2 的迁移
- GFS - OCFS2 对比表

### OCFS2 背景

OCFS2 是一个由 Oracle 于 2005 年作为 GPL 许可下的开源软件发布的集群文件系统。与其 2002 年发布的前身 OCFS 相反，它现在是一个通用集群文件系统，适合作为比仅部署 Oracle Real Application Cluster (RAC) 更广泛的场景的存储基础。

在 SUSE Linux Enterprise Server 10 中，例如，它可以用于让多个主机访问 XenVM 回环磁盘映像。得益于 OCFS2，虚拟机可以从一个主机迁移到另一个主机。

Novell 将 OCFS2 版本 1.0.8 集成到 SLES 9 SP2，将版本 1.2.1 集成到 SP3 和 SLES 10。由于 OCFS2 从 2.6.16 版本开始已包含在主 Linux 内核中，因此将来可能会有更多的 Linux 发行版集成 OCFS2。

所有 OCFS2 版本——从版本 1.0 开始——在磁盘上是兼容的，但相应的工具不兼容。因此，请注意将它们一起升级，并仅使用与内核驱动处于同一级别的管理工具来访问集群文件系统。

在 SLES10 上，可以通过命令行或使用随附的 OCFS 控制台（提供图形界面）来设置 OCFS2。

OCFS2 具有以下特性：

- 符合 POSIX 标准
- 支持多种 CPU 架构，因为它是字节序安全的。
- 线程安全，异步 I/O，元数据和数据缓存提供高性能。
- 无锁的节点本地分配区域使新文件的创建速度更快。
- 基于区段；自动分配元数据组，没有固定的 inode 限制。
- 直接 I/O 以绕过本地操作系统缓存。
- 与 SUSE Linux Enterprise Server 10 中的 Heartbeat 2 集群解决方案完全集成。
- OCFS2 已在 RHEL4、SLES 9 SP3 和 SLES 10 上通过 Oracle 9iR2、10g、10gR2 RAC 认证。

### OCFS2 配置

以下示例配置假设 OCFS2 位于设备“sda”上。为了能够在节点之间共享此设备，可以使用第 9-1 页“iSCSI”一节中介绍的 iSCSI 使该设备可用。

> 为了避免存储设备成为潜在的单点故障，这会使 HA 集群的目的落空，存储设备也应包含 HA 特性。DRBD（分布式复制块设备）和 Heartbeat 可用于此目的；然而，DRBD 和 Heartbeat 的配置超出了本课程的范围。

配置 OCFS2 的以下步骤中，大多数需要在每个节点上执行：

1. 为图形化 OCFS2 前端 **ocfs2console** 创建 SSH 密钥。
   为了方便在不同节点上进行配置，通常使用 ssh 密钥。
   密钥由命令 **ssh-keygen** 生成。选项 **-N ""** 创建一个没有密码短语的密钥。**ssh-copy-id** 是一个脚本，它将公钥添加到目标计算机上的 .ssh/authorized_keys 文件中。

   ```
   dal0:~ $ ssh-keygen -t rsa -N ""
   Generating public/private rsa key pair.
   Enter file in which to save the key (/root/.ssh/id_rsa): <ENTER>
   Created directory '/root/.ssh'.
   Your identification has been saved in /root/.ssh/id_rsa.
   Your public key has been saved in /root/.ssh/id_rsa.pub.
   The key fingerprint is:
   cb:1e:a9:7b:08:a7:82:d5:24:fc:90:49:cc:84:d6:a7 root@dal0

   dal0:~ $ ssh-copy-id -i ~/.ssh/id_rsa.pub root@dal1;
   dal0:~ $ ssh-copy-id -i ~/.ssh/id_rsa.pub root@dal2;
   ...
   ```

2. 安装 OCFS2 软件包。
   使用 YaST 软件管理模块或命令 **yast -i ocfs2-tools ocfs2console**。

3. 创建 /etc/ocfs2/cluster.conf

   以下是一个具有两个节点的示例，如果增加更多节点，请相应地调整 "node_count"。

   ```
   cluster:
       name = mycluster
       node_count = 2
   node:
       name = da10
       cluster = mycluster
       number = 0
       ip_address = 10.0.0.10
       ip_port = 7777
   node:
       name = da11
       cluster = mycluster
       number = 1
       ip_address = 10.0.0.11
       ip_port = 7777
   ```

   除了主机名外，**name** 也可以是完全限定域名；名称解析必须有效。

4. 在共享块设备上创建 OCFS2。

   这仅在一个节点上执行。

   请注意使用与集群配置文件中相同的标签（上述示例中为 *mycluster*）。

   创建 OCFS2 文件系统的命令是 **mkfs.ocfs2**。

   不带选项输入命令将给出简明的语法概览：

   ```
   da3:~ # mkfs.ocfs2
   Usage: mkfs.ocfs2 [-b block-size] [-C cluster-size]
   [-N number-of-node-slots] [-T filesystem-type]
   [-L volume-label] [-J journal-options] [-H%q\v] device [blocks-count]
   ```

   手册页解释了可用的选项。

   以下命令在 /dev/sda 上创建一个 OCFS2 文件系统：

   ```
   dal0:~ # mkfs.ocfs2 -b 4k -C 128k -N 4 -L mycluster /dev/sda
   mkfs.ocfs2 1.2.1
   Filesystem label=mycluster
   Block size=4096 (bits=12)
   Cluster size=131072 (bits=17)
   Volume size=8595308544 (65577 clusters) (2098464 blocks)
   3 cluster groups (tail covers 1065 clusters, rest cover 32256 clusters)
   Journal size=67108864
   Initial number of node slots: 4
   Creating bitmaps: done
   Initializing superblock: done
   Writing system files: done
   Writing superblock: done
   Formatting Journals: done
   Writing lost+found: done
   mkfs.ocfs2 successful
   ```

5. 在 /etc/fstab 中添加一个条目。

   以下步骤在所有节点上执行，并假设设备（本例中为 /dev/sda）在所有节点上相同

   ```
   dal0:~ # echo '/dev/sda /mnt ocfs2 defaults 0 0' >> /etc/fstab
   ```

6. 配置 OCFS2 集群服务。

   确保 **Cluster to start on boot** 与 `/etc/ocfs2/cluster.conf` 中的条目相同

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

7. 自动启动存储集群服务。

   以下命令在 `/etc/init.d/rc*.d/` 中创建链接，以便在启动时启动服务。

   ```bash
   da10:~ # chkconfig -a o2cb
   da10:~ # chkconfig -a ocfs2
   ```

8. 手动启动 OCFS2 集群服务并挂载 OCFS2。

   以下命令启动 ocfs2 所需的服务：

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

   第二个命令挂载文件系统。使用命令 **mount** 查看结果。

9. 检查集群文件系统是否正常工作。

   ```
   dal0:~ # cat
   /sys/kernel/config/cluster/mycluster/heartbeat/dead_threshold
   7
   ```

10. 手动停止 OCFS2 集群服务并卸载 OCFS2。

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

