
| 在线重做日志 (Online Redo Log) | 取决于重做日志文件是否多副本以及该文件是否是活动组的一部分。如果是多副本，数据库实例将发出错误信息并存活。如果没有多副本，实例将崩溃，如果该文件未归档，则其中的任何数据将丢失。 |

| 回滚 (Rollback) | 如果只有一个非 SYSTEM 回滚表空间，数据库实例将崩溃。只要有一个可用的回滚表空间，实例就应该存活，但性能会受到影响。如果有活动事务，数据可能会丢失。 |

| 临时 (Temp) | 数据库实例将继续存在，但任何需要磁盘排序的操作都将失败。 |

| 数据 (Data) | 丢失对表空间内对象的访问（`USERS`, `TOOLS`, `DRSYS` 被视为数据文件）。 |

| 索引 (Index) | 丢失性能，以及在重建表时创建/更新主键或唯一键的能力。数据可以访问，但任何需要索引的 DML 操作将失败。 |

Oracle 会在“注意到”文件丢失后立即对其做出反应。例如，在测试时，你可以删除 `system.dbf` 仍然执行某些查询，因为文件仍被认为是“打开”的，Oracle 并不知道它丢失了。然而，当发生日志切换且 Oracle 尝试访问该文件时，实例将崩溃，因为它已不再存在。所有 Oracle 后台进程（`PMON`、`SMON` 等）都将终止。用户可能会收到 `ORA-12571`: TNS:packet write failure 或 "ERROR at ora:03113: end-of-file on communication channel"，表示他们已失去与数据库的联系。警报日志中将有一个如下条目：

```
Sat Apr 14 15:04:17 2001
CKPT: terminating instance due to error 1242
Instance terminated by CKPT, pid = 2676
```

在此阶段，你拥有一个无法打开的崩溃数据库实例。你可能有一个或多个需要解决的活动事务。

磁盘丢失的问题更加复杂，原因在于，崩溃的磁盘很少只带走一个文件；通常会丢失好几个文件。例如，存放 `/u02` 的磁盘故障将影响图 9 所示的文件和数据库。

# Unix 和 Linux 上的 Oracle DBA

最建议的做法是对控制文件和在线重做日志进行多副本化（multiplexing）。在 Oracle 世界中，多副本意味着创建并维护文件的多个副本。这与镜像不同，因为镜像是在操作系统层面完成的，而多副本文件由 Oracle 管理。只有控制文件和在线日志可以多副本。

另一种增加容错性的常用方法是设置数据库在崩溃后自动重启。这种自动启动功能意味着当 Unix/Linux 服务器重启或崩溃时，Oracle 应该重启。SA 和 DBA 仍需要调查原因。

## 多副本控制文件

控制文件多副本意味着同一个数据库维护多个控制文件。Oracle 将从创建的第一个读取，但会写入所有控制文件（除非只有一个）。如果丢失了任何控制文件，数据库仍会崩溃，但恢复将大大简化。

通常，控制文件在创建数据库时就会进行多副本。数据库创建向导和大多数脚本会自动创建三个控制文件副本。这些文件位于你的 `configSID.ora` 或 `initSID.ora` 文件中。如果你想在数据库创建后添加额外的控制文件，请按步骤操作：

- 1. 正常关闭数据库。
- 2. 编辑 `configSID.ora` 或 `initSID.ora` 文件，添加新的控制文件名和位置。
- 3. 将一个良好的现有控制文件复制到指定的位置并赋予其正确的名称。
- 4. 重启数据库并查询 `V$CONTROLFILE` 以验证 Oracle 是否“看到”了它。

控制文件较小（每个约 4M），拥有额外的副本没有实际性能影响。只需确保它们放置在不同的文件系统中，以防一次故障损坏所有文件。

## 多副本在线重做日志

重做日志多副本在概念上与控制文件多副本非常相似。Oracle 自动维护文件的一个或多个副本。关键区别在于，丢失多副本重做日志文件会生成错误信息，但数据库实例将继续运行。此外，数据不会丢失。考虑到这些益处，将每个重做日志组放在不同的文件系统中是非常好的主意。

你在数据库创建后多副本化重做日志。使用以下步骤对重做日志组进行多副本处理：

## 备份与恢复

### 第 9 章

1. 使用 `V$LOG` 和 `V$LOGFILE` 识别每个组的成员，并识别哪一个是活动组。

```sql
SQL> select * from vlogfile;
```

| GROUP# | STATUS | MEMBER |
| :--- | :--- | :--- |
| 1 | | `/u03/oradata/rh1dev/redo01a.rd` |
| 2 | | `/u07/oradata/rh1dev/redo02a.rd` |
| 3 | | `/u11/oradata/rh1dev/redo03a.rd` |

```sql
SQL> select group#, members, bytes, status from v$log;
```

2. 为非活动重日志组添加新成员。

```sql
SQL> alter database add logfile member
2 /u08/oradata/rh1dev/redo02b.rd
3 to group 2;
```

数据库已更改。

对组 3 中的 `redo03.bdo` 重复此步骤。

3. 使用 `ALTER SYSTEM SWITCH LOGFILE` 切换到下一个组。然后为剩余的非活动重日志组添加新成员。

4. 执行多次日志切换以消除每个新成员的 INVALID（无效）或 STALE（过时）状态，可以通过 `VLOGFILE` 查看。

与控制文件相比，重日志的多路复涉及更多的维护和性能开销。具体来说，如果你将重日志文件所需的磁盘空间翻倍，由于额外的写入会导致更多的 I/O。然而，为了避免在丢失重日志文件时数据库崩溃并可能丢失数据，这是一个非常小的代价。

# 数据库自动启动

当 Unix 或 Linux 服务器关闭（计划内或其他）时，运行其上的任何数据库也会关闭。一旦服务器重启，任何数据库默认都将保持关闭状态。如果需要重启数据库，这可能会成为问题。除非有 DBA 7x24 小时值班以防出现问题，否则解决方案是让数据库在机器启动时自动重启。

## Unix 和 Linux 上的 Oracle DBA

Oracle Linux 服务器在关闭或启动时会经历一组预定义的阶段。每个运行级别（run level）都有一份与其相关的进程列表。DBA 可以包含 shell 脚本，在特定的运行级别启动或关闭一个或多个数据库和监听器。这允许数据库在服务器忙碌时自动关闭，并允许在服务器重启后重启数据库。发生崩溃时，Oracle 实例恢复将自动解决问题。

决定数据库是否自动重启的控制字段是 `/etc/oratab`（Linux 或 HP-UX）或 `/var/opt/oratab/oracle/oratab`（Sun Solaris）。图 9.2 显示了 `oratab` 文件的副本。

![](img/0735bb12e1d45128c662b4b409eb1bf1_263_0.png)

图 9.2 `/etc/oratab` 文件。

每个条目的最后一个字段（`Y` 或 `N`）表示数据库在重启时是否重启。如你所示，`rhlep1` 和 `rhldev1` 会自动重启。

Oracle 提供了两个脚本来自动启动和关闭 `/etc/oratab` 中指定的数据库。脚本是：

```
$ORACLE_HOME/bin/dbshutdown
```

和

```
$ORACLE_HOME/bin/dbstart
```

需要与系统管理员（SA）协作实现这些脚本，因为它们需要 root 权限。可能会出现特定于平台的问题，所以你应该考虑你的《安装和配置指南》。然而，以下步骤提供了一种在 Sun Solaris 上实现自动启动和关闭过程的方法：

1. （以 Oracle 身份）编辑 `ORACLE_HOME/bin/dbshutdown` 为 `SHUTDOWN IMMEDIATE`。
2. （以 root 身份）创建一个文件：`/etc/init.d/dbshutdown`。

```sh
#!/bin/sh

su - oracle -c "/u01/app/product/8.1.6/bin/lsnrctl stop"
su - oracle -c "/u01/app/product/8.1.6/bin/dbshut"
```

3. 为 `dbshut` 分配权限 755。

   `$ chmod 755 dbshut`

4. （以 root 身份）为 `/etc/rc.d/K01dbshut` 创建指向 `/etc/init.d/dbshut` 的软链接。

   `$ ln -s /etc/init.d/dbshut /etc/rc.d/K01dbshut`

   此链接将强制脚本关闭监听器。Oracle `dbshut` 脚本将关闭正在运行的数据库。

5. （以 root 身份）创建一个文件：`/etc/init.d/dbstart`。
