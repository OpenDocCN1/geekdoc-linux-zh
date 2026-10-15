
条目中的字段授予的访问权限授予该条目。然而，在表对象中，为表中的每一列都维护了一组额外的访问权限。这些权限适用于条目中相应的列。当所有者或条目均未授予访问权限时，使用这些权限来授予访问。列规范中的访问权限适用于条目的所有者或组所有者，而不是表对象的所有者和组所有者。

当执行读取操作时，如果表未授予读取权限，条目未授予读取权限，但通过列访问授予了权限，则返回该条目并在列中带有正确的值，在未授予读取权限的列中显示字符串 *NP*。

例如，客户端对一个未授予其读取权限的表执行了列表操作。将检查每个符合客户端搜索标准的条目对象，以查看其是否授予了客户端读取权限。如果是，则将其包含在返回结果中。如果不是，则检查每一列以查看其是否授予了客户端读取权限。如果任何列授予了读取权限，则返回列数据。未授予读取权限的列其内容将被替换为字符串 *NP*。如果没有任何一列授予了读取权限，则不返回该条目。

## 协议操作授权

NIS+ 操作通过其所操作对象的权限具有隐式的访问控制。例如，若要读取表中的条目，你必须拥有该条目的读取权限。然而，NIS+ 操作默认不执行任何访问检查，因此允许所有人执行。

![](img/185d23104c385dfb6a62d64cc96b8997_968_0.png)

| 操作 | 使用该操作的命令示例 |
|---|---|
| `NIS_CHECKPOINT` | `nisping` |
| `NIS_CPTIME` | `nisping`, `rpc.nisd` |
| `NIS_MKDIR` | `nismkdir` |
| `NIS_PING` | `nisping`, `rpc.nisd` |
| `NIS_RMDIR` | `nisrmdir` |
| `NIS_SERVSTATE` | `nisbackup`, `nisrestore` |
| `NIS_STATUS` | `nisstat`, `rpc.nispasswdd` |

参阅 `nisopaccess(1)` 以了解如何对这些 NIS+ 操作强制执行访问控制。`nisopaccess(1)` 命令是 Solaris 8 版本中新增的。

## 命令列表

以下列表显示了所有与 NIS 相关的命令和编程函数。

### NIS+ 用户命令

- `nisaddent (1M)` 将 `/etc` 文件和 NIS 映射添加到其对应的 NIS+ 表中。
- `niscat (1)` 显示 NIS+ 表和对象。
- `nischgrp (1)` 更改 NIS+ 对象的组所有者。
- `nischmod (1)` 更改 NIS+ 对象的访问权限。
- `nischown (1)` 更改 NIS+ 对象的所有者。
- `nischttl (1)` 更改 NIS+ 对象的生存时间值。
- `nisdefaults (1)` 显示 NIS+ 默认值。
- `niserror (1)` 显示 NIS+ 错误消息。
- `nisgrep (1)` 搜索 NIS+ 表。
- `nispradm (1)` 管理 NIS+ 组。
- `nisln (1)` 为 NIS+ 对象创建符号链接。
- `nisls (1)` 列出 NIS+ 目录的内容。
- `nmatch (1)` 搜索 NIS+ 表。
- `niskmdir (1)` 创建 NIS+ 目录。
- `nisopcess (1)` 控制对 NIS+ 的访问。Solaris 8 版本中新增。
- `nispasswd (1)` 控制 NIS+ 密码信息。
- `nisrm (1)` 从命名空间中删除 NIS+ 对象。
- `nisrmdir (1)` 删除 NIS+ 目录。
- `nissowcache (1M)` 打印缓存文件的内容。
- `nistblad (1M)` 管理 NIS+ 表。
- `nistest (1)` 使用条件表达式返回 NIS+ 命名空间的状态。

### NIS+ 管理命令

- `aliasadm (1M)` 操作 NIS 别名映射。
- `nis_cachemgr (1M)` 缓存 NIS+ 服务器的信息。
- `nisaddcred (1M)` 创建 NIS+ 凭据。
- `nisaddent (1M)` 从相应的 `/etc` 文件或 NIS 映射创建 NIS+ 表。
- `nisauthconf (1M)` 配置 Diffie-Hellman 密钥。
- `nisbackup (1M)` 备份 NIS+ 主体的凭据。Solaris 8 版本中新增。
- `nisclient (1M)` 为 NIS+ 主体初始化 NIS+ 凭据。
- `nisd (1M)` NIS+ 服务进程。
- `nisd_resolv(1M)` NIS+ 服务进程。
- `nisinit (1M)` 初始化 NIS+ 客户端和服务器。
- `nislog (1M)` 显示 NIS+ 事务日志的内容。
- `nisping (1M)` 向 NIS+ 服务器发送 ping。
- `nispopulate (1M)` 填充 NIS+ 域中的 NIS+ 表。
- `nisprefadm (1M)` 为 NIS+ 客户端设置服务器偏好。Solaris 8 版本中新增。
- `nisrestore (1M)` 恢复 NIS+ 目录备份。Solaris 8 版本中新增。
- `nisserver (1M)` 设置 NIS+ 服务器。
- `nissetup (1M)` 初始化 NIS+ 域。
- `nisshowcache (1M)` 打印共享缓存文件的内容。
- `nisstat (1M)` 报告 NIS+ 服务器统计信息。
- `nisupdkeys (1M)` 更新 NIS+ 目录对象中的公钥。
- `rpc.nisd (1M)` NIS+ 服务进程。
- `rpc.nisd_resolv(1M)` NIS+ 服务守护进程。
- `sysidnis(1M)` 系统配置。

# NIS+ 编程 API

- `nis_add(3NSL)` NIS+ 命名空间函数。
- `nis_add_entry(3NSL)` NIS+ 表格函数。
- `nis_addmember(3NSL)` NIS+ 组操作函数。
- `nis_checkpoint(3NSL)` 杂杂的 NIS+ 日志管理函数。
- `nis_clone_object(3NSL)` NIS+ 子程序。
- `nis_creategroup(3NSL)` NIS+ 组操作函数。
- `nis_destroy_object(3NSL)` NIS+ 子程序。
- `nis_destroygroup(3NSL)` NIS+ 组操作函数。
- `nis_dir_cmp(3NSL)` NIS+ 子程序。
- `nis_domain_of(3NSL)` NIS+ 子程序。
- `nis_error(3NSL)` 显示 NIS+ 错误消息。
- `nis_first_entry(3NSL)` NIS+ 表格函数。
- `nis_freenames(3NSL)` NIS+ 子程序。
- `nis_freeresult(3NSL)` NIS+ 命名空间函数。
- `nis_freeservlist(3NSL)` 杂杂的 NIS+ 函数。
- `nis_freetags(3NSL)` 杂杂的 NIS+ 函数。
- `nis_getnames(3NSL)` NIS+ 子程序。
- `nis_getservlist(3NSL)` 杂杂的 NIS+ 函数。
- `nis_groups(3NSL)` NIS+ 组操作函数。
- `nis_ismember(3NSL)` NIS+ 组操作函数。
- `nis_leaf_of(3NSL)` NIS+ 子程序。
- `nis_lerror(3NSL)` 显示某些 NIS+ 错误消息。
- `nis_list(3NSL)` NIS+ 表格函数。
- `nis_local_directory(3NSL)` NIS+ 本地目录。
- `nis_local_group(3NSL)` NIS+ 本地名称。
- `nis_local_host(3NSL)` NIS+ 本地主机。
- `nis_local_names(3NSL)` NIS+ 本地名称。
- `nis_local_principal(3NSL)` NIS+ 本地主体。
- `nis_lookup(3NSL)` NIS+ 命名空间函数。
- `nis_mkdir(3NSL)` 杂杂的 NIS+ 函数。
- `nis_modify(3NSL)` NIS+ 命名空间函数。
- `nis_modify_entry(3NSL)` NIS+ 表格函数。
- `nis_name_of(3NSL)` 
- `nis_names(3NSL)` NIS+ 命名空间函数。
- `nis_next_entry(3NSL)` NIS+ 表格函数。
- `nis_objects(3NSL)` NIS+ 对象格式。
- `nis_perror(3NSL)` 显示 NIS+ 错误消息。
- `nis_ping(3NSL)` 杂杂的 NIS+ 日志管理函数。
- `nis_print_group_entry(3NSL)` NIS+ 组操作函数。
- `nis_print_object(3NSL)` NIS+ 子程序。
- `nis_remove(3NSL)` NIS+ 命名空间函数。
- `nis_remove_entry(3NSL)`
