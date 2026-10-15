
```
udb1nx02:/db2home/db2inst1/sqllib/adsm # ./dsmapipw
**************************************************
* Tivoli Storage Manager                         *
* API Version = 4.2.3                            *
**************************************************
Enter your current password:
Enter your new password:
Enter your new password again:

Your new password has been accepted and updated.
```

DB2 提供了 `db2adutl` 命令来管理 TSM 中的备份文件。您可以查看和删除 DB2 备份文件，并将备份文件从 TSM 存储带回数据库服务器。示例 5-8 显示了使用 `db2adutl` 的简单查询。

### 示例 5-8 db2adutl 查询示例

```
db2inst1@udb1nx02:~> db2adutl query full

Query for database ITSODB

Retrieving FULL DATABASE BACKUP information.
1 Time: 20021104103617 Oldest log: S0000043.LOG DB Partition Number: 1 Sessions: 1
2 Time: 20021104103534 Oldest log: S0000046.LOG DB Partition Number: 0 Sessions: 1
3 Time: 20021104103044 Oldest log: S0000045.LOG DB Partition Number: 0 Sessions: 1

db2inst1@udb1nx02:~> db2adutl query logs

Query for database ITSODB

Retrieving LOG ARCHIVE information.
Log file: S0000045.LOG, DB Partition Number: 1, Taken at: 2002-11-04-11.59.11
Log file: S0000046.LOG, DB Partition Number: 1, Taken at: 2002-11-04-11.59.11
Log file: S0000050.LOG, DB Partition Number: 0, Taken at: 2002-11-04-11.59.11
Log file: S0000051.LOG, DB Partition Number: 0, Taken at: 2002-11-04-11.59.14
```

> 注：关于使用 `db2adutl` 的完整说明写在 IBM DB2 UDB 命令参考 V8，SC09-4828 中。

#### 5.1.4 备份实用程序

我们已完成所有步骤，如 5.1.1 中所述，“启用 roll forward 和日志归档”，第 151 页，现在讨论如何进行数据库备份。

- **完全离线：** 完全离线数据库备份允许您在不应用任何日志记录的情况下恢复数据库映像。示例 5-9 显示了离线备份命令。

### 示例 5-9 完全离线备份到磁盘

```
db2inst1@udb1nx02:/db2backup> db2 backup db itsodb to /db2backup

Backup successful. The timestamp for this backup image is : 20021029163312

udb1nx02: db2 backup db itsodb to /db2backup completed ok
```

- **完全在线和增量：** 增量备份节省备份时间和资源。在线备份期间，数据库仍可供应用程序访问。示例 5-10 提供了完全在线备份的示例。

### 示例 5-10 增量备份到磁盘

```
db2inst1@udb1nx02:~> db2 backup db itsodb online incremental to /db2backup

Backup successful. The timestamp for this backup image is : 20021029165004

udb1nx02: db2 backup db itsodb online incremental to /db2backup completed ok
```

- **Delta 备份：** 示例 5-11 显示了在进行完全数据库备份后进行的 delta 数据库备份。

### 示例 5-11 Delta 备份

```
db2inst1@udb1nx02:~> db2 backup db itsodb online incremental delta to /db2backup

Backup successful. The timestamp for this backup image is : 20021029165624

udb1nx02: db2 backup db itsodb online incremental to /db2backup completed ok
```

#### 5.1.5 使用 Control Center 备份数据库

备份实用程序已完全集成在 DB2 Control Center 中（图 5-6）。

![](img/d95c931f4f3da4a6bd0ee55148fefad7_173_0.png)

图 5-7 生成的备份语句

另一种备份数据库的方法是通过控制中心生成脚本，并使用自己的调度程序定期运行此备份脚本。

![](img/d95c931f4f3da4a6bd0ee55148fefad7_174_0.png)

#### 5.1.6 在 DB2 命令行处理器中备份数据库

在示例 5-12 中，我们展示了一个用于备份我们的示例数据库 ITSODB 的脚本，该数据库是分区的。使用 `db2_all` 命令调用此脚本：

```
db2_all '/db2home/db2inst1/database_backup.ksh db2inst1 itsodb'
```

### 示例 5-12 备份脚本 database_backup.ksh

```
#!/usr/bin/ksh
#
# Script: backing up database
#---------------------------------------------

echo running against instance: ${1}
echo running against database: ${2}
INSTANCE=$1
DB_ALIAS=$2
#---------------------------------------------
# check for db2profile and execute it, if available
```
