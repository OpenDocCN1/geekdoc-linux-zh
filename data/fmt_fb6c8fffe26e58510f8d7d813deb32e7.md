
# 使用 RMAN 注册、同步和重置数据库

还有其他三个 RMAN 命令用于对恢复库执行初始设置和配置操作。本质上，这些命令是使用频率较低的维护命令。这些命令分为以下类别：

- 注册和注销目标数据库
- 重置恢复库
- 同步恢复库

你应该熟悉这些设置和配置类别以及相关的命令。

## 注册和注销目标数据库

注册目标数据库是为了让 RMAN 能够在恢复库中存储有关目标数据库的信息。这些是 RMAN 用于妥妥备份数据库的信息。以下是注册目标数据库的示例：

```bash
oracle@octilli:~> rman target / catalog rman/rman@rcat

noracle@octilli:~> . oraenv
ORACLE_SID = [tst9] ? orc9
oracle@octilli:~> rman target / catalog rman/rman@rcat
```

Recovery Manager: Release 9.0.1.0.0 - Production

(c) Copyright 2001 Oracle Corporation. All rights reserved.

connected to target database: ORC9 (DBID=3960695)

connected to recovery catalog database

```sql
RMAN> register database;

database registered in recovery catalog
starting full resync of recovery catalog
full resync complete
```

```sql
RMAN>
```

Copyright ©2002 SYBEX, Inc., Alameda, CA www.sybex.com

通过注销目标数据库，你移除了备份数据库所需的信息。此任务不在 RMAN 实用程序中执行，而是通过作为恢复库模式所有者执行存储过程来完成。

以下是注销目标数据库的示例：

1. 你必须在位于 Recovery Manager 恢复库的 DB 表中获取 `DB_ID` 和 `DB_KEY` 值。

```bash
oracle@octilli:~ ~ sqlplus rman/rman@rcat
```

```sql
SQL*Plus: Release 9.0.1.0.0 - Production on Sat Oct 6 22:42:08 2001
```

(c) Copyright 2001 Oracle Corporation. All rights reserved.

Connected to:

Oracle9 Enterprise Edition Release 9.0.1.0.0 Production

With the Partitioning option

JSever Release 9.0.1.0.0 - Production

```sql
SQL> select * from db;
```

| DB_KEY | DB_ID | HIGH_CONF_RECID | CURR_DBINC_KEY |
|---|---|---|---|
| 504 | 396065 | 0 | 505 |

```sql
SQL>
```

2. 然后，你必须使用这些值运行存储过程。

```sql
SQL> execute dbms_rcat.unregisterdatabase(504,396065);
```

PL/SQL procedure completed.

3. 最后，你可以验证该数据库已不在恢复库中。

```sql
SQL> select * from db;
```

no rows selected

SQL> 

## 重置恢复库

重置恢复库允许你清除所有恢复库信息并重新开始。如果恢复库已损坏或你需要进行全新的设置，这将非常有用。以下是重置恢复库的示例：

1. 连接到恢复库并执行重置命令。

```sql
RMAN> connect catalog rman/rman

connected to recovery catalog database

RMAN> reset catalog;

recovery catalog reset
```

2. 重置恢复库后，你需要重新注册目标数据库。

```bash
oracle@octilli:~> rman target / catalog rman/rman@rcat
```

Recovery Manager: Release 9.0.1.0.0 - Production

connected to target database: ORC9 (DBID=3960695)

connected to recovery catalog database

```sql
RMAN> register database;

database registered in recovery catalog
starting full resync of recovery catalog
full resync complete
```

## 同步恢复库

同步恢复库使 RMAN 能够比较目标数据库与存储在恢复库中的信息并更新恢复库。部分同步不会使用物理信息（如数据文件、表空间）来更新恢复库。完全同步会捕获上述所有物理信息以及更改的记录。此过程在执行备份时发生。

以下是连接目标数据库并同步恢复库的示例：

1. 通过向 `DATA` 表空间添加新的数据文件对目标数据库进行物理更改。

```sql
oracle@octilli:~ sqlplus /nolog
```

SQL*Plus: Release 9.0.1.0.0 - Production on Tue Oct 9 17:52:19 2001

(c) Copyright 2001 Oracle Corporation. All rights reserved.

```sql
SQL> connect /as sysdba
Connected.
SQL> ALTER TABLESPACE DATA ADD
DATAFILE '/db01/oracle/tst9/data02.dbf' SIZE 20M
```

2. 接下来，连接到 RMAN 并同步恢复库以反映此更改。

```bash
oracle@octilli:~ rman target / catalog rman/rman@rcat
```

Recovery Manager: Release 9.0.1.0.0 - Production

connected to target database: TST9 (DBID=205850149)

connected to recovery catalog database

```sql
RMAN> resync catalog;
```

starting full resync of recovery catalog

full resync complete

3. 现在运行报告以查看 TST9 数据库的更改。注意新的数据文件 `data02.dbf`，它是报告中的第八个数据文件。

## 从恢复目录中生成列表和报告

```sql
RMAN> report schema;
```

数据库架构报告

| 文件 K-bytes | 表空间 | RB 分段 | 数据文件名称 |
|---|---|---|--|
| 1 | 204800 SYSTEM | YES | `/db1/oracle/tst9/system01.dbf` |
| 2 | 40960 RBS | YES | `/db1/oracle/tst9/rbs01.dbf` |
| 3 | 10240 TEMP | NO | `/db1/oracle/tst9/temp01.dbf` |
| 4 | 10240 USERS | NO | `/db1/oracle/tst9/users01.dbf` |
| 5 | 5120 TOOLS | NO | `/db1/oracle/tst9/tools01.dbf` |
| 6 | 51200 DATA | NO | `/db1/oracle/tst9/data01.dbf` |
| 7 | 10240 INDX | NO | `/db1/oracle/tst9/indx01.dbf` |
| 8 | 20480 DATA | NO | `/db1/oracle/tst9/data02.dbf` |

```sql
RMAN>
```
