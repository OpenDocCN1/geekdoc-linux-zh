
## 2. 输入以下命令：

```
make -f ins_rdms.mk dnfs_on
```

> 注意：每个实例只能有一个活动的 Direct NFS 客户端实现。在另一个实例上使用 Direct NFS 客户端将阻止另一个实现。

## 共享文件系统存储配置

如果 Oracle Database 使用通过 `oranstab` 配置的挂载点，则可以使用新文件 `oranstab` 来指定针对 Oracle Database 到 Direct NFS 客户端的额外选项。例如，您使用 `oranstab` 为挂载点指定额外的路径。您可以添加 `/etc` 或到 `$ORACLE_HOME/dbms`。

在使用 Oracle RAC 时，当 `oranstab` 文件放置在 `$ORACLE_HOME/dbms` 时，文件中的条目特定于共享数据库。在这种情况下，所有运行 Oracle RAC 的节点使用相同的 `$ORACLE_HOME/dbms/oranstab` 文件。在非共享 Oracle RAC 安装中，`oranstab` 必须在所有节点上进行复制。

当 `oranstab` 文件放置在 `/etc` 时，它可以包含集群节点上运行的所有 Oracle 数据库使用的挂载点，包括独立数据库。然而，在 Oracle RAC 系统上，如果 `oranstab` 文件放置在 `/etc`，则您必须在所有节点上同步每个 `/etc/oranstab` 文件，就像您必须处理 `/etc/fstab` 一样。

## 3.2.4 决定对数据文件使用 Direct NFS

Direct NFS 客户端是使用内核管理 NFS 的替代方案。本节包含有关 Direct NFS 客户端的信息：

- 关于 Direct NFS 客户端存储
- 使用 `oranstab` 文件配合 Direct NFS Client
- 使用 Direct NFS 客户端挂载 NFS 存储设备
- 使用 `oranstab` 指定网络路径

### 3.2.3.1 关于 Direct NFS 客户端存储

在 Oracle Database 11g Release 2 中，您无需使用操作系统内核 FS 客户端，而是配置 Oracle Database 使用 Oracle 内部 Direct NFS 客户端直接访问 NFS V3 服务器。

要启用 Oracle Database 使用 Direct NFS 客户端，在开始安装之前，NFS 文件必须通过常规 NFS 挂载进行挂载并可用。Direct NFS 在安装后管理设置。您应该将内核挂载选项作为备份，但对于正常操作，Direct NFS 客户端将管理 NFS 挂载。

请参考您的供应商文档完成 NFS 配置和挂载。某些 NFS 服务器要求 NFS 客户端使用保留端口连接。如果您的 NFS 服务器在开启了保留端口检查的情况下运行，则您必须禁用它以便 Direct NFS 客户端运行。禁用保留端口检查，以确保您的 NFS 服务器文档正常工作。

对于限制 root 端口的服务器，您可以使用 `insecure` 选项允许 root 以外的客户端连接到 NFS 服务器。或者，您可以按照第 3.2.12 节“禁用 Direct NFS 客户端 Oracle 磁盘管理 NFS 集群”所述禁用 Direct NFS 客户端。

> 注意：使用支持 Oracle RAC 的 NFS 服务器。请参考以下 URL 获取支持信息：`https://support.oracle.com`

为集群和 Oracle RAC 配置 Oracle Grid Infrastructure 3-9

### 使用 `oranstab` 文件配合 Direct NFS Client

如果您使用 Direct NFS 客户端，则可以选择使用一个新文件 `oranstab` 进行 Oracle 数据文件管理，以指定针对 Oracle Database 到 Direct NFS 客户端的特定选项。例如，您使用 `oranstab` 为挂载点指定额外的路径。您可以添加 `/etc` 或到 `$ORACLE_HOME/dbms`。
