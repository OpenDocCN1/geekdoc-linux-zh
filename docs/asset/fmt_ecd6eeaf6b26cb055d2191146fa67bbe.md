
| TOOLS | `/u04/oradata/rh1dev1/tools01.dbf` | 104,857,600 |

| USERS | `/u04/oradata/rh1dev1/users01.dbf` | 109,051,904 |

| RBS | `/u05/oradata/rh1dev1/rollback01.rbs` | 707,788,800 |

| DRSYS | `/u10/oradata/rh1dev1/drsys01.dbf` | 88,080,384 |

```
SQL> select name from v$controlfile;
```

```
NAME
/u05/oradata/rh1dev1/control01.ctl
/u06/oradata/rh1dev1/control02.ctl
/u09/oradata/rh1dev1/control03.ctl
```

SQL> select group#, member from v$logfile;

| GROUP# | MEMBER |

| :--- | :--- |

| 1 | `/u03/oradata/rh1dev/redo/01a.rd` |

| 2 | `/u07/oradata/rh1dev/redo/02a.rd` |

| 3 | `/u11/oradata/rh1dev/redo/03a.rd` |

将这些查询结果与你想要创建的文件进行比较。它们应该是匹配的，否则某些文件没有被创建。如果是这种情况，请确定文件系统是否已满（`df -k`）。

# 编译对象

下一步是使用 `SQL*Plus` 登录数据库并查看。重新编译对象是检查失败实例的步骤。如果某些对象仍然无效，请执行以下命令：

```
SELECT object_type, count(*) FROM dba_objects WHERE status = 'INVALID' GROUP BY object_type;
```

| OBJECT_TYPE | COUNT |

| :--- | :--- |

| PACKAGE | 15 |

| PACKAGE BODY | 26 |

| PROCEDURE | 30 |

| VIEW | 10 |

编译无效对象

重新编译对象。例如：

```sql
SELECT count(*) FROM dba_objects WHERE object_type = 'JAVA';
```

你的数字应该是 9000 个对象，且没有一个是无效的。如果某些对象仍然无效，请重新执行过程。最后，请执行以下命令：

```sql
SELECT object_type, count(*) FROM dba_objects WHERE status = 'INVALID' GROUP BY object_type;
```

## 动态 SQL

``` |

  2000

 2000

  200 |
```

SQL> alter user sys identified by superdba7;

用户已更改（User altered.）。

SQL> !clear

还有其他用户账户应该锁定或更改密码。通过查询 `DBA_USERS` 表并选择用户名，可以得到大约 15 个标准账户，具体取决于你加载了哪些功能。

SQL> select username from dba_users order by created;

USERNAME
SYS
SYSTEM
OUTLN
DBSNMP
TRACESVR
AURORAORB$AUTHENTICATED
ORDSYS
ORDPLUGINS
MDSYS
CTXSYSYS

已选择 10 行（10 rows selected）。如果你有如 `SCOTT`、`ADAMS`、`BLAKE`、`CLARK` 和 `JONES` 等用户测试账户，可以使用此命令将其锁定：

SQL> alter user scott account lock;

用户已更改（User altered.）。

如果你不使用上下文选项（Context Option），可以锁定 `CTXSYS`、`TRACESVR`、`ORDSYS` 和 `ORDPLUGINS` 等特殊账户。`MDSYS` 用于空间选项（Spatial Option），因此如果你不需要它，也可以将其锁定。

## 修改默认密码

务必更改默认密码，否则人们将绕过你的安全程序。在 DBA 之间流传着非常流行的故事：一个经理前往一个“安全”站点从系统中获取某些数据。到达后，他因安全许可被扰了几个小时。他感到沮丧而绝望，在没人注意的情况下，尝试用 `SYS/change_on_install` 登录。令他惊讶的是，他竟然进去了。经理随后获取了所需的数据并离开，从未告诉该站点他们存在巨大的安全漏洞。我无法判断其中有多少是夸张，但可以肯定，这个安全漏洞存在于许多系统中。

你将在第 7 章“GUI 管理产品”中学习如何更改 `DBSNMP` 用户的密码。`DBMS` 应该更改密码，因为它用于数据库统计和调优。`AURORABS$UNAUTHENTICATED` 是一个特殊情况。根据我获得的信息，你不应该锁定它，但应该更改它的密码。这应该在稍后的版本中更改，目前它似乎没有危险权限，但某些 DBA 认为这种情况令人不安。

## 修改 oratab 文件

该文件包含每个数据库列表、其 `ORACLE_HOME` 以及用于判断数据库在机器重启时是否应自动重启的 `Y` 标志。它用于确定哪些数据库在服务器上、它们的版本以及它们是否应该自动重启。 脚本在设置用户登录环境时会打开此文件。在 `HP-UX` 和 `Linux` 机器上，`oratab` 文件位于 `/etc`，而在 `Solaris` 平台上，它位于 `/var/opt/oracle`。

如果你完全使用 `BCCA` 或 `DBCA` 创建数据库以生成脚本，`oratab` 文件将自动更新。如果你是手动创建并运行的脚本，则需要向此文件添加包含包含你数据库的行。以下是 `oratab` 文件的关键字段。

```
demo:/u01/app/oracle/product/8.1.6:N

rhitst1:/u01/app/oracle/product/8.1.6:N

rhdev1:/u01/app/oracle/product/8.1.6:N
```

简单地执行 `vi oratab`，移动到最后一行，然后输入 `yy` “复制（yank）”一行。然后输入 `p` 将该行粘贴到末尾。编辑该行显示你的数据库名称和正确的 `ORACLE_HOME`。目前，将最后一列留为 `N`。你将在第 9 章“备份与恢复”中学习如何设置数据库在重启时自动重启。

## 为 init.ora 创建软链接

在 `ORACLE_HOME/dbs` 下，需要一个指向 `ORACLE_BASE/admin/database_name/file` 中 `init.ora` 的 Unix 软链接。要查看哪些链接，请执行以下操作：

```
$ pwd

/u01/app/oracle/product/8.1.6/dbs

$ ls -alt init*
```

```
1 lrwxrrrwx 1 oracle dba 51
Feb 17 11:55 initrhitst1.ora -> /u01/app/oracle/admin/rhitst1/file/initrhitst1.ora
```

## Unix 和 Linux Oracle DBA

```
lrwxwxr-wx 1 oracle dba 45 Feb 17 10:44 initdemora.ora -> /u01/app/oracle/admin/demo/pfile/initdemora.ora
```

```
-rw-r--r-- 1 oracle dba 835 Apr 11 2000 initsoxx.sql
-rw-r--r-- 1 oracle dba 9219 Aug 27 1999 initdtw.ora
-rw-r--r-- 1 oracle dba 8385 Aug 27 1999 init.ora
```

注意第一字段中权限部分的“l”（例如 `lrwxrwrwx`）。这表示这是一个软链接。在这个例中，`inrhitst1.ora` 文件实际上只是指向 `/u01/app/oracle/admin/rh1st1/pfile/inith1st1.ora` 中真实文件的指针。Oracle 在此位置（`$ORACLE_HOME/dbs`）查找你正尝试启动的数据库的 ora 文件。Oracle 将使用此位置的软链接 `init.ora` 来启动数据库。

如果使用 `DBCA` 创建数据库或生成脚本，链接将自动创建。在这种情况下，它们是自动创建的。如果你没有使用 `DBCA` 创建了脚本，则新数据库的唯一 `init.ora` 在 `pfile` 目录中，因此需要为该文件创建一个链接。语法如下：

```
ln -s [文件物理存在的位置] [你放置文件并引导传入请求的位置].
```

```
$ ln -s /u01/app/oracle/admin/rh1dev/pfile/init1dev.ora /u01/app/oracle/product/8.1.6/dbs/init1dev.ora
```
