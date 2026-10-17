
导致服务器使用单线程运行。这用于 Linux 下的调试，因为 Linux 通常至少使用三个线程。自 MySQL 5.1.17 起，此选项已被弃用，推荐使用 `--thread-handling=one-thread`。

- `--pid-file=file_name`

当 `mysqld` 启动时，它将进程 ID (PID) 写入文件。此选项指定 PID 文件的路径名。其他进程可以使用该文件来确定服务器的进程号，通常用于向其发送信号。例如，`mysql.server` 在发送信号使服务器关闭时会读取该文件。如果 `file_name` 作为相对路径提供，则从数据目录开始解释。此选项对嵌入式服务器没有影响。

- `--safe-mode`

此选项类似于 `--skip-new`，但禁用了更多功能。如果 MySQL 表现不稳定，或者复杂语句似乎产生错误结果，您可以尝试使用它。

- `--safe-show-database` (`布尔型`)

此选项已废弃：MySQL 管理员应使用 `SHOW DATABASES` 权限来管理对数据库名称的访问。

- `--safe-user-create` (`布尔型`)

禁止没有用户权限表 `INSERT` 访问权限的用户创建账户。

## F.12.2.1 Windows 选项

本节中的选项仅适用于在 Windows 下运行的服务器。服务名称和命名管道名称不区分大小写。共享内存名称区分大小写。

- `--console` (`*boolean*`)

显示用于错误消息的控制台窗口。

- `--enable-named-pipe` (`*boolean*`)

对于包含命名管道支持的 MySQL 服务器，命名管道连接默认是禁用的。此选项启用命名管道连接。默认的管道名称为 `MySQL`。可以使用 `--socket` 选项更改名称。启用命名管道可能会在服务器关机时导致问题。请测试您的系统，以确保此选项能正常工作。

- `--install [service_name]`

将服务器安装为在 Windows 启动时自动运行的服务。如果未指定 `service_name`，默认服务名称为 `MySQL`。

- `--install-manual [service_name]`

将服务器安装为在 Windows 启动时不会自动运行的服务。您必须手动启动该服务。如果未指定 `service_name`，默认服务名称为 `MySQL`。

- `--remove [service_name]`

从服务中移除服务器。如果未指定 `service_name`，默认服务名称为 `MySQL`。

- `--shared-memory [boolean]`

启用共享内存连接的支持。默认的共享内存名称为 `MySQL`。可以使用 `--shared-memory-base-name` 选项更改名称。

- `--standalone`

将服务器作为独立程序运行，而不是作为服务运行。

## F.12.2.2 InnoDB 选项

本节中的选项是 InnoDB 存储引擎特有的。

- `--innodb` (`*boolean*`)

启用 InnoDB 存储引擎。如果编译时包含了 InnoDB，则默认启用。如果您不使用 InnoDB 表，可以使用 `--skip-innodb` 来禁用 InnoDB，从而节省内存。

- `--innodb_autoextend_increment=size`

如果 InnoDB 共享表空间配置为自动扩展，此选项控制扩展的增量大小。值以兆字节（MB）为单位指定。默认值为 8MB。

- `--innodb_data_file_path=filespec_list`

InnoDB 表空间组件文件的规范。该选项值的格式在第 12.6.3.1 节“配置 InnoDB 表空间”中讨论。

- `--innodb_data_home_dir=dir_name`

InnoDB 表空间组件所在目录的路径。

- `--innodb_fast_shutdown` (`*boolean*`)

加快服务器关机过程；InnoDB 存储引擎会跳过某些通常执行的操作。

- `--innodb_file_per_table` (`*boolean*`)

如果启用此选项，InnoDB 将为新创建的表创建独立的表空间文件。也就是说，每个 InnoDB 表都有一个位于其数据库目录中的 `.ibd` 表空间文件。共享表空间仅用于 InnoDB 数据字典条目，而不用于数据或索引存储。该选项默认禁用。

- `--safemalloc-mem-limit=n`

模拟内存不足。该值代表可用于分配的内存量的限制。只有当服务器在配置时使用了 `--with-debug=full` 选项编译时，才能使用此选项。

- `--secure-auth` (`*boolean*`)

防止客户端连接，除非它们使用 MySQL 4.1 中引入的更安全的密码格式。

- `--secure-file-priv=dir_name`

设置 `secure_file_priv` 系统变量，该变量将某些文件操作限制在指定目录中。此选项是在 MySQL 5.0.38/5.1.17 中引入的。

- `--skip-grant-tables` (`*boolean*`)

禁用使用权限表验证客户端连接。这允许任何客户端拥有完全访问权限进行任何操作。它还禁用了 `CREATE USER`、`DROP USER`、`RENAME USER`、`GRANT`、`REVOKE` 和 `SET PASSWORD` 语句。您可以通过发出 `FLUSH PRIVILEGES` 语句或 `mysqladmin flush-privileges` 命令，或者在不使用 `--skip-grant-tables` 的情况下重新启动服务器，来指示服务器重新开始使用权限表。

- `--skip-host-cache`

禁用主机名缓存。

- `--skip-locking`

此选项已弃用，建议使用 `--skip-external-locking`。请参阅 `--external-locking` 的说明。

- `--skip-name-resolve`

抑制主机名解析。如果指定了此选项，权限表必须通过 IP 地址或 `localhost` 指定主机。

- `--skip-networking`

此选项禁用 TCP/IP 连接。只有本地客户端可以连接，并且必须使用非 TCP/IP 接口。Unix 客户端可以使用 Unix 套接字文件连接。Windows 客户端可以使用共享内存或命名管道连接。

- `--skip-new`

跳过使用新的、可能不安全的例程。

- `--skip-safemalloc`

跳过内存分配检查。只有当服务器在配置时使用了 `--with-debug=full` 选项编译时，才能使用此选项。

- `--skip-show-database`

默认情况下，任何用户都可以发出 `SHOW DATABASES` 语句。如果用户具有 `SHOW DATABASES` 权限，则显示所有数据库；否则，显示该用户具有某些权限的数据库。使用 `--skip-show-database` 选项后，只有具有 `SHOW DATABASES` 权限的用户才能使用 `SHOW DATABASES` 语句，在这种情况下它会显示所有数据库。

- `--skip-stack-trace`

在发生错误时跳过堆栈跟踪打印。

- `--skip-symlink`

此选项已弃用，建议使用 `--skip-symbolic-links`。请参阅 `--symbolic-links` 的说明。

- `--skip-thread-priority`

通常，更新（修改表的语句）的优先级高于获取数据的语句。如果这不理想，此选项会使服务器不为不同类型的语句分配不同的优先级。

- `--slow-query-log` (`*boolean*`)

为 `--log-output` 选项选定的日志目标启用慢查询日志，如果作为 `--skip-slow-query-log` 给出，则禁用该日志。此选项是在 MySQL 5.1.12 中引入的。

- `--sql-bin-update-name` (`*boolean*`)

将 `sql_log_bin` 和 `sql_log_update` 绑定在一起，使得设置其中一个（通过 `SET` 语句）也会设置另一个。由于更新日志不再存在，此选项在 MySQL 5.0 中已过时。应改用二进制日志。

- `--sql-mode=mode_list`

此选项修改服务器行为的某些方面，使其按照标准 SQL 执行，或与旧版其他数据库服务器或 MySQL 服务器兼容。`mode_list` 应为一个或多个模式值的逗号分隔列表，或为空字符串以清除模式。允许的模式值在附录 D“系统、状态和用户变量参考”中 `sql_mode` 系统变量的说明中给出。

- `--symbolic-links` (`*boolean*`)
