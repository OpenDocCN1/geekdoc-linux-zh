
```
# cat /sys/kernel/mm/redhat_transparent_hugepage/enabled
```

其他内核：

```
# cat /sys/kernel/mm/transparent_hugepage/enabled
```

以下是显示启用 `[always]` 标志时使用透明 HugePages 内存的示例输出。

```
[always] never
```

> 注意：如果内核中移除了透明 HugePages，则 `/sys/kernel/mm/transparent_hugepage` 或 `/sys/kernel/mm/redhat_transparent_hugepage` 文件不存在。

要禁用透明 HugePages，请执行以下步骤：

- 1. 在 `/etc/grub.conf` 文件的内核启动命令行添加以下条目：`transparent_hugepage=never`

例如：

```
title Oracle Linux Server (2.6.32-300.25.1.el6uek.x86_64)
root (hdb0,0)
kernel /vmlinux-2.6.32-300.25.1.el6uek.x86_64 ro=LABEL=/
transparent_hugepage=never
initrd/initramfs-2.6.32-300.25.1.el6uek.x86_64.img
```

- 2. 重启系统以更改永久生效。

# 集群安装 Oracle Grid Infrastructure 概念

本附录解释了要求执行的预安装任务的原因以及其他安装概念。

本附录包含以下章节：

- 理解预安装配置
- 理解存储配置
- 理解服务器池
- 理解离地升级

## D.1 理解预安装配置

本节回顾了关于集群 Oracle Grid Infrastructure 预安装任务的相关概念。它包含以下子节：

- 理解 Oracle 组和用户
- 理解 Oracle Base 目录路径
- 理解网络地址
- 理解网络时间要求

### D.1.1 理解 Oracle 组和用户

本节包含以下主题：

- 理解 Oracle Inventory 组
- 理解 Oracle Inventory 目录

#### D.1.1.1 理解 Oracle Inventory 组

你必须拥有一个组，其成员被授予访问 Oracle Inventory (`oraInventory`) 目录的权限，该目录是服务器上所有 Oracle 软件安装的中央清单目录。该组成员具有 Oracle 中央清单 (`oraInventory`) 目录的写入权限，并被授予 Oracle Cluster 资源、OCR 密钥、Oracle Cluster home 中允许 DW 访问的目录或其他权限。默认情况下，此组名为 `oinstall`。Oracle Inventory 组必须是 Oracle 软件安装的主主组。

`oraInventory` 目录包含以下内容：

- 系统上 Oracle home 目录（Oracle Grid Infrastructure 和 Oracle Database）的注册表
- Oracle 软件安装的安装日志和跟踪文件。这些文件也会复制到相应的 Oracle home 中以供以后参考。
- 关于 Oracle 安装的其他元数据信息存储在各个 Oracle home 清单目录中，与中央清单分开。

你可以配置一个组作为 Oracle Inventory 的访问控制组、数据库管理员 (OSDBA) 以及所有 Oracle 软件用于操作系统身份验证的其他控制组。然而，如果你使用一个组为所有系统权限提供操作系统身份验证，则该组必须是你希望授予管理系统权限的所有用户的主主组。

> 注意：如果软件已安装在系统上，则现有的 Oracle Inventory 组必须是你用于安装 Oracle Grid Infrastructure 的操作系统 (`oracle` 或 `grid`) 的主主组。参考“确定 Oracle Inventory 是否以及 Oracle Inventory 是否存在”来识别 Oracle Inventory 组。

#### D.1.1.2 理解 Oracle Inventory 目录

Oracle 目录 (`oraInventory`) 是服务器上所有安装 Oracle 软件的中央清单位置。

当你首次在系统上安装 Oracle 软件时，系统会提示你提供 `orainventory` 目录路径。

当你为执行 Oracle Grid Infrastructure 安装的用户提供非环境变量 `ORACLE_BASE` 的 Oracle base 路径时，OUI 会 `ORACLE_BASE../oraInventory` 路径下创建 Oracle inventory。例如，如果 `ORACLE_BASE` 设置为 `/opt/oracle/11`，则 Oracle inventory 在路径 `/opt/oracle/oraInventory` 创建，这样所有安装的中央清单都在该特定 Oracle 安装用户的 Oracle base 之外。

如果你输入的路径未设置 `ORACLE_BASE`，则 Oracle Inventory 目录将放置在执行安装的用户的家目录下。例如：

```
/home/oracle/oraInventory
```

由于这可能导致后续多个 Oracle 软件所有者进行安装时出现权限错误，Oracle 建议不要接受此选项，并使用符合 OFA 标准的路径。

对于新安装，Oracle 建议创建一个符合 OFA 结构的 Oracle 路径（例如 `/u01/app/oraInventory`），该路径由 Oracle 软件所有者拥有，或者将 Oracle base 变量设置为符合 OFA 标准的路径。

如果你将 Oracle base 变量设置为如 `/u01/app/grid` 或 `/u01/app/oraInventory` 等路径，则 Oracle Inventory 将默认设置到该路径，并具有正确的权限，允许所有 Oracle 安装所有者写入此中央清单目录。

## D-2 Oracle Grid Infrastructure 安装指南

默认情况下，Oracle Inventory 目录不会安装在安装所有者的 Oracle base 目录下。这是因为 Oracle 软件安装共享一个公共的 Oracle Inventory，因此所有用户只有一个 Oracle Inventory，而每个用户都有独立的 Oracle base。

### D.1.2 理解 Oracle Base 目录路径

本节包含关于准备 Oracle base 目录的信息。

#### D.1.2.1 Oracle base 目录概述

在安装期间，系统会提示指定一个 Oracle base 位置，该位置由安装用户拥有。你可以选择一个具有现有 Oracle home 的位置，或者选择另一个不具备 Oracle base 目录结构的目录位置。

使用 Oracle base 目录路径有助于组织 Oracle 安装，并确保多个数据库的安装维持最优的可灵活架构 (OFA) 配置。

#### D.1.2.2 理解 Oracle Base 和 Grid Infrastructure 目录

即使你没有使用相同的软件安装 Grid Infrastructure (Oracle Clusterware 和 ASM) 或 Oracle Database，也请注意，Grid Infrastructure 安装期间的 `root.sh` 脚本会将放置集群二进制文件的 home 目录的所有权更改为 `root`，并将所有祖目录也更改为 `root`。由于此原因，Grid Infrastructure for cluster 无法与 Oracle software 位于一起。

> 参见 Oracle Database 安装指南获取更多关于 Oracle Restart 信息

## D1.3 理解网络地址

在安装期间，系统要求你指定每个网络接口的计划用途，将每个接口识别为公共或私有接口，或者你希望 Clusterware 使用的接口。公共和虚拟 IP 地址配置在公共接口上。参考以下详细信息获取有关每种类型的类型：

- 关于公共 IP 地址
- 关于私有 IP 地址
- 关于虚拟 IP 地址
- 关于网格命名服务 (GNS) IP 地址
- 关于 SCAN

### D1.3.1 关于公共 IP 地址

公共 IP 地址通过 DHCP 动态分配，或在主机文件中静态定义。它使用公共接口（客户端可用接口）。

### D1.3.2 关于私有 IP 地址

私有地址配置在私有接口上。Oracle Cluster 使用标记为私有的接口。每个节点都需要配置地址，但不需要额外配置。由于 Cache Fusion 和节点间的流量，Oracle 强烈建议使用物理隔离的私有网络。该网络仅供集群节点访问。你不应在具有私有地址的网络设置防火墙，因为可能会拦截流量。

### D1.3.3 关于虚拟 IP 地址

虚拟 IP (`VIP`) 地址注册在 GNS 或 DNS 中。为你的 VIP 选择符合以下要求的地址：
