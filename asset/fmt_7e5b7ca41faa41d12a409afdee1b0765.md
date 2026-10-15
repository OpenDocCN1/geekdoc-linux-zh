
| --- | --- |
| `Alter_priv` | `Alter_priv` |
| `Alter_routine_priv` | `Alter_routine_priv` |
| `Create_priv` | `Create_priv` |
| `Create_routine_priv` | `Create_routine_priv` |
| `Create_tmp_table_priv` | `Create_tmp_table_priv` |
| `Create_view_priv` | `Create_view_priv` |
| `Delete_priv` | `Delete_priv` |
| `Drop_priv` | `Drop_priv` |
| `Event_priv` | `Event_priv` |
| `Execute_priv` | `Execute_priv` |
| `Index_priv` | `Index_priv` |
| `Insert_priv` | `Insert_priv` |
| `Lock_tables_priv` | `Lock_tables_priv` |
| `References_priv` | `References_priv` |
| `Select_priv` | `Select_priv` |
| `Show_view_priv` | `Show_view_priv` |
| `Trigger_priv` | `Trigger_priv` |
| `Update_priv` | `Update_priv` |
| `tables_priv` 表 | `columns_priv` 表 | `proc_priv` 表 |
| --- | --- | --- |
| `Table_priv` | `Column_priv` | `Proc_priv` |
| | `Column_priv` | |

#### 表 13.4 授权表 SSL 和资源管理列（仅限 user 表）

| SSL 列 | 资源管理列 |
| --- | --- |
| `ssl_type` | `max_connections` |
| `ssl_cipher` | `max_questions` |
| `x509_issuer` | `max_updates` |
| `x509_subject` | `max_user_connections` |

授权表系统包括 `tables_priv`、`columns_priv` 和 `proc_priv` 表，用于定义特定表、列以及存储函数和过程的权限。没有 `rows_priv` 表，因为 MySQL 不提供行级权限。例如，您无法将用户的访问权限限制为仅包含表中某列的特定值的那些行。如果需要此功能，您必须在自己的应用程序中实现它。实现协作行级锁定的一种方法是使用建议锁定函数，如 `GET_LOCK()` 和 `RELEASE_LOCK()`。此过程在第 C.2.8 节“建议锁定函数”中有描述。

MySQL 的新版本有时会增加新的权限。例如，`Event_priv` 和 `Trigger_priv` 列是在 MySQL 5.1.6 中实现的。当您升级现有的 MySQL 安装到此类版本时，在使用新权限之前必须更新授权表。第 12.3 节“管理 MySQL 用户帐户”描述了执行此操作的步骤。

##### 13.2.1.1 授权表访问范围列

授权表的范围列用于确定当帐户尝试执行给定操作时，服务器查询哪些行。每个授权表行包含

## 13.2 外部安全性：防止未授权的网络访问

`HOST` 和 `USER` 列，用于指示该行适用于由特定用户从指定主机发起的连接。例如，`USER` 表中 `HOST` 列和 `USER` 列分别为 `LOCALHOST` 和 `BILL` 的行，将用于 `BILL` 从本地主机发起的连接，但不适用于 `BETTY` 的连接。其他表包含额外的作用域列。`DB` 表包含一个 `DB` 列，用于指示该行适用于哪个数据库。类似地，`TABLES_PRIV` 和 `COLUMNS_PRIV` 表中的行包含作用域列，进一步将它们的范围缩小到数据库中的特定表或表中的特定列。`PROCS_PRIV` 的作用域列指定某行适用于哪个存储函数或存储过程。

### 13.2.1.2 授权表的权限列

授权表还包含权限列。对于每一行，这些列指示匹配作用域列中列出的值的用户持有哪些权限。MySQL 支持的权限在以下列表中展示，这些列表描述了管理权限以及控制数据库和表访问的权限。每个列表都使用了 `GRANT` 语句中使用的权限名称。在大多数情况下，这些权限名称与授权表中的权限列名称具有明显的相似性。例如，`SELECT` 权限对应于 `SELECT_PRIV` 列。

### 13.2.1.3 管理权限

以下权限适用于控制服务器操作或用户授予权限能力的管理操作：

- `CREATE USER`
  - 允许您使用 `CREATE USER`、`DROP USER`、`RENAME USER` 和 `REVOKE ALL PRIVILEGES` 语句。此权限是在 MySQL 5.0.3 中引入的。
- `FILE`
  - 允许您指示服务器读取或写入服务器主机上的文件。为了使该权限的使用保持在一定范围内，服务器采取了某些预防措施：
    - 您只能访问所有用户可读（world-readable）的文件，因此这些文件不太可能被以任何方式视为受保护的。
    - 您要写入的任何文件必须尚不存在。这防止您强制服务器覆盖重要文件，例如 `/etc/passwd` 或属于他人的数据库文件。（如果未执行此约束，例如，您可以完全替换 `mysql` 数据库中授权表的内容。）
  - 尽管服务器采取了这些预防措施，但如果没有正当理由，不应授予此权限；如第 13.2.4 节“应避免的授权表风险”中所述，这可能极其危险。如果您确实授予了 `FILE` 权限，请确保不要在 Unix 系统中以 root 登录用户运行服务器，因为 root 可以在文件系统的任何位置创建新文件。通过从普通登录账户运行服务器，您确保它只能在该账户可访问的目录中创建文件。另请参阅第 12.2.1.1 节“使用非特权登录账户运行服务器”。
- `GRANT OPTION`
  - 允许您将您自己拥有的权限（包括 `GRANT OPTION` 权限）授予其他用户。
- `PROCESS`
  - MySQL 服务器是多线程的，这使其能够同时处理多个客户端连接。这些线程可以被视为在服务器内运行的进程。`PROCESS` 权限允许您使用 `SHOW PROCESSLIST` 语句或 `mysqld processlist` 命令查看当前正在执行的活动信息。此权限使您能够查看所有活动，即使是与其他用户相关的活动。即使没有 `PROCESS` 权限，您也始终可以查看您自己的活动。
- `RELOAD`
  - 允许您执行多种管理服务器操作。拥有 `RELOAD` 权限，您能够发出诸如 `FLUSH` 和 `RESET` 之类的语句。您还可以执行以下 `mysqldadmin` 命令：`reload`、`refresh`、`flush-hosts`、`flush-logs`、`flush-privileges`、`flush-status`、`flush-tables` 和 `flush-threads`。
- `REPLICATION CLIENT`
  - 允许您使用 `SHOW MASTER STATUS` 和 `SHOW SLAVE STATUS` 语句查询主服务器和从服务器的位置和状态。
- `REPLICATION SLAVE`
  - 允许客户端连接主服务器并请求从服务器更新，并使用 `SHOW SLAVE HOSTS` 和 `SHOW BINLOG EVENTS` 语句。必须将此权限授予用于连接主服务器的从服务器账户。
- `SHOW DATABASES`
  - 允许您通过发出 `SHOW DATABASES` 语句查看所有数据库名称。如果您没有此权限，只有当您拥有针对特定数据库的某些权限时，才能看到该数据库名称。然而，任何适用于数据库的全局权限都会赋予这种能力，这包括通常全局授予的 `CREATE TEMPORARY TABLES` 和 `LOCK TABLES` 权限。为确保只有拥有 `SHOW DATABASES` 权限的用户可以使用 `SHOW DATABASES` 语句，请使用 `--skip-show-database` 选项启动服务器。
- `SHUTDOWN`
  - 允许您关闭服务器，例如使用 `mysqldadmin shutdown` 命令。
- `SUPER`
  - 允许您使用 `KILL` 语句或 `mysqldadmin kill` 命令终止服务器进程。此权限使您能够终止任何进程，即使是与其他用户相关的进程。即使没有 `SUPER` 权限，您也始终可以终止您自己的进程。
  - 由该权限启用的其他语句包括用于修改全局系统变量和全局事务隔离级别的 `SET`、`CHANGE MASTER`、`PURGE MASTER LOGS`、`SHOW MASTER STATUS`、`SHOW SLAVE STATUS`、`START SLAVE` 和 `STOP SLAVE`。`SUPER` 还允许您基于存储在 DES 密钥文件中的密钥，通过 `DES_DECRYPT()` 函数执行 DES 解密。
