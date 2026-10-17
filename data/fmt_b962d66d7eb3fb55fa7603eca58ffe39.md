
```bash
# mkdir -p /u01/app/11.2.0/grid
# mkdir -p /u01/app/grid
# chown -R grid:install /u01
# mkdir -p /u01/app/oracle
# chown oracle:install /u01/app/oracle
# mkdir -p /u01/app/oracle
# chown oracle:install /u01/app/oracle2
# chmod -R 775 /u01
```

运行这些命令后，你将拥有以下组和用户：

- 一个 Oracle 集中库存组，或称为 oracleinventory 组 (`oracleinstall`)，该主组的成员被授予了写入 `oracleInventory` 目录的权限。
- 一个独立的 ASM 组 (`asmadmin`)，其成员被授予 `SYSASM` 权限以管理 Oracle Clusterware 和 Oracle ASM。
- 一个独立的 ASM OSDBA 组 (`asmdba`)，其成员包括 `grid`、`oracle1` 和 `oracle2`并被授予访问 Oracle ASM 的权限。
- 一个独立的 ASM OSOPER 组 (`asmoper`)，其成员拥有有限的 Oracle ASM 管理员权限，包括启动和停止 Oracle ASM 的权限。
- 一个用于集群所有者的 Oracle Grid 安装组 (`grid`)，作为其主组，并将 OSASM (`asmadmin`) 和 ASM OSDBA (`asmdba`) 作为次要组。
- 两个不同数据库的两个独立 OSDB 组 (`dbal` 和 `dba2`)，为每个数据库建立 `SYDBA` 权限。
- 两个 Oracle 数据库所有者 (`oracle1` 和 `oracle2`)，用于划分 Oracle 数据库二进制文件的所有权，并以 `OracleInventory` 组为其主组，以其对应的数据库 OSDB 组 (`dbal` 和 `dba2`) 以及 ASM OSDBA 组 (`asmadmin`) 为次要组。
- 安装前，一个符合 OFA 标准的挂载点 `/u01` 属于 `grid:install`。
- 一个属于 Grid 安装所有者的 Oracle base `/u01/app/oracle` 属于 `grid:install`，初始权限为 775，在安装过程中会更改为 755。
- 一个 Oracle base `/u01/app/oracle2` 属于 `oracle2:install`，权限为 775。
- 一个 Grid home `/u01/app/11.2.0/grid` 属于 `grid:install`，权限为 775 (`drwxrxr-x`)。这些权限是安装必需的，在安装过程中会更改为 `root:install` 权限的 755 (`drwx-xr-x`)。
- `/u01/app/Inventory`。此路径仍然属于 `grid:install`，以便允许其他 Oracle 软件写入程序写入集中库存。

## 2.6 检查硬件要求

检查以下要求：

- 通用服务器要求
- 服务器硬件要求
- 服务器内存要求
- 检查服务器硬件和内存配置

### 2.6.1 通用服务器要求

- 确保服务器以运行级别（run level）3 或运行级别 5 启动。
- 确保服务器运行相同的操作系统二进制文件。Oracle Grid Infrastructure 安装和 Oracle Real Application Clusters (Oracle RAC) 支持在同一集群中使用具有不同硬件的服务器。

### 2.6.2 服务器硬件要求

每个系统必须满足以下最小硬件要求：

- 至少 1024 x 768 的显示分辨率，以便 OUI 正确显示。
- `/tmp` 目录至少有 1 GB 空间。
- Oracle Grid Infrastructure for a Cluster home (Grid home) 需要 6.6 GB 空间，这包括 ClusterClusterware 和 Oracle ASM 文件和日志文件、ACFS 日志文件，以及如果你的平台支持 Cluster Health Monitor 库。
- Grid Infrastructure 所有者的 Oracle base 目录中需要额外的高达 10 GB 空间，用于存储 Trace File Analyst 和 Collector 生成的诊断收集数据。
- 在 Linux x86 平台上，如果你打算安装 Oracle Database，请为 Oracle base 分配 4 GB 空间。
- 对于 Linux x86_64 平台，如果你打算安装 Oracle Database，请为 Oracle base 分配 4.6 GB 的磁盘空间。

> 注意：如果你打算在集群上安装 Oracle Databases 或 Oracle RAC，请注意每个服务器上的 `/dev/shm` 挂载区域的大小必须大于服务器数据库的系统全局区域 (SGA) 和程序全局区域 (PGA)。请数据库管理员审核预期的 SGA 和 PGA 大小，以确保在集群上安装数据库后无需增加 `/dev/shm`。

如果你正在安装 Oracle Database，那么由于你选择配置自动数据库备份，你需要在文件系统或 Oracle Automatic Storage Management 磁盘组中准备额外的空间作为快速恢复区 (Fast Recovery Area)。

另参：Oracle Automatic Storage Management Administrator's Guide

### 2.6.3 服务器内存要求

确保你的系统满足以下要求，取决于你的系统架构：

- 64 位系统和 Linux on System z 内存要求
- 内存要求

高级安装 Oracle Grid Infrastructure for a Cluster 预安装任务 2-25

## 检查硬件要求

**注意：** 在 Linux 上，Hugepages（大页）功能使用内存映射文件通过大页页表分配不可交换的内存。如果你启用了 Hugepages，则在计算交换空间之前，应从 RAM 中减去分配给 HugePages 的内存。

如果你遇到指示交换空间大小不足的 OUI 错误，但你的交换空间符合此处列出的要求，则可以忽略该错误。

#### 2.6.3.1 64 位系统和 Linux on System 内存要求

每个系统必须满足以下条件：

- 安装 Oracle Grid Infrastructure for a Cluster（包括计划安装 RAC 的安装）至少需要 2.5 GB 的 RAM。
- 交换空间等于可用 RAM 的倍数，如下表所示：

表 2-1

| 可用 RAM | 需要的 Swap |
| --- | --- |
| 2.5 GB 到 32 GB 之间 | 等于 RAM 的大小 |
| 大于 16 GB | 16 GB |

#### 2.6.3.2 内存要求

每个系统必须满足以下条件：

- 安装 Oracle Grid Infrastructure for a Cluster（包括计划安装 Oracle 的安装）至少需要 2.5 GB 的 RAM。
- 交换空间等于可用 RAM 的倍数，如下表所示：

表 2-2

| 可用 RAM | 需要的 Swap |
| --- | --- |
| 2.5 GB 到 16 GB 之间 | 等于 RAM 的大小 |
| 大于 16 GB | 16 GB |

### 2.6.4 检查服务器硬件和内存配置

要确保每个系统满足这些要求，请遵循步骤操作：

1. 确定物理 RAM，输入以下命令：

```bash
grep MemTotal /proc/meminfo
```

如果物理 RAM 的大小小于所需大小，则必须在继续之前安装更多内存。

2. 确定已配置交换空间的大小，输入以下命令：

```bash
grep SwapTotal /proc/meminfo
```

如有必要，请参考你的操作系统文档了解如何配置额外的交换空间。

3. 确定 `/tmp` 目录中的可用空间，输入以下命令：

```bash
df -k /tmp
```

此命令以 1 KB 块为单位显示磁盘空间。在大多数系统上，你可以使用带有 -h 标志的命令 (`df -h`) 以“人类可读”格式显示输出，例如 "2G" 和 "10M"。如果 `/tmp` 目录可用磁盘空间小于 1 GB（小于 1048576 个 1-块），请完成以下操作之一：

 删除 `/tmp` 目录中的不必要文件以释放空间。

 扩展包含 `/tmp` 的文件。如有必要，请联系系统管理员获取扩展文件的信息。

4. 确定系统的空闲 RAM 和磁盘空间量，输入以下命令：

```bash
free
```

> 注意：
> - Oracle 建议在确定最终值之前多次获取可用 RAM 和交换空间的值。因为可用 RAM 和交换空间会根据与计算机的交互而变化。
> - 联系你的操作系统供应商获取交换空间分配指南。供应商指南优于本指南中的交换空间要求。
