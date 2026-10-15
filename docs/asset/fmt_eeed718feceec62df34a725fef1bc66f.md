
本文档通过 Oracle Support 的 Rapid Visibility (RaV) 流程交付给您，因此未经过独立的技术审查。

适用范围：
Oracle Server - Enterprise Edition - Version: 10.2
此问题可能发生在任何平台上。

### 症状

datapump import 导入失败，并出现以下错误set：

```
Import: Release 10.2.0.3.0 - 64bit Production on Monday, 03 September 2007 12:49:00

Copyright (c) 2003, 2005, Oracle. All rights reserved.
Connected to: Oracle Database 10g Enterprise Edition Release 10.2.0.3.0 -64bit Production
With the Partitioning, OLAP and Data Mining options
Master table "STRADMIN","SYS_IMPORT_FULL_02" successfully loaded/unloaded
"STRADMIN","SYS_IMPORT_FULL_02": stradmin@ FULL=y DIRECTORY=dir DUMPFILE=STREAMS_CONFIGURATION TRANSFORM=OID DATABASE_EXPORT/TABLE
ORA-39014: One or more workers have exited.
ORA-39029: worker process "DW01" prematurely terminated.
ORA-31671: Worker process DW01 had an unhandled exception.ORAORA06600: internal error code, arguments: [upiRaBzlob], [kgcdd], [1], [0],
ORA-06512: at "SYS.WORKER", line 1342
ORA-06512: at line 2
Job "STRADMIN","SYS_IMPORT_FULL_02" stopped due to fatal error at 12:49:34
```

### 原因

导出时的默认设置为是 `COMPRESSION=METADATA_ONLY`，这会导致压缩的转储文件。这种压缩损坏了数据并导致 `ORA-00600` 错误，从而导入失败。在执行导出时指定 `COMPRESSION=NONE` 应该可以成功导入。

### 解决方案

一种变通方法是执行以下操作：

1. 执行导出时指定 `COMPRESSION=NONE`。
2. 将新创建的非压缩数据文件导入数据库。

### 10.6.2 准备执行 Data Pump

要的第一工作是在 z/OS 中创建一个用于导出和导入的目录。以 `oracle` 用户身份登录后，进入可写目录并创建目录：
`mkdir expdata`

我们使用 SQL 以系统用户登录数据库，并创建了用于转储文件和日志的目录：

### 10.7 运行 Data Pump 导出

我们以 `oracle` 用户身份登录 z/OS UNIX，并运行 Data Pump 导出命令导出全数据库，如示例 10-5 所示。

Example 10-5 Running the Pump export

```
ORACLE2 @ /u/oracle2>expdp trade/
dumpfile=mydata.dmp logfile=mydata.log compression=none

Export: Release 10.2.0.3.0 on Monday, 05 November, 12:19:58

Copyright (c) 2003, 2005, Oracle. All rights reserved.

Connected to: Oracle Database 10g Enterprise Edition Release 10.2.0.3.0 - Production

With the Partitioning, OLAP and Data Mining options

Starting "TRADE","SYS_EXPORT_SCHEMA_01": trade/
dumpfile=mydata.dmp logfile=mydata.log

Estimate in progress using BLOCKS method...

Processing object type SCHEMA_EXPORT/TABLE_DATA

Total estimation using BLOCKS method: 640 KB

Processing object type SCHEMA_EXPORT/USER

Processing object type SCHEMA_EXPORT/SYSTEM_GRANT

Processing object type SCHEMA_EXPORT/ROLE_GRANT

Processing object type SCHEMA_EXPORT/DEFAULT_ROLE

Processing object type SCHEMA_EXPORT/PRE_SCHEMA/PROCACT_SCHEMA

Processing object type SCHEMA_EXPORT/TABLE

Processing object type SCHEMA_EXPORT/INDEX

Processing object type SCHEMA_EXPORT/TABLE/CONSTRAINT

Processing object type SCHEMA_EXPORT/INDEX/STATISTICS

Processing object type SCHEMA_EXPORT/TABLE/COMMENT

Processing object type SCHEMA_EXPORT/TABLE/STATISTICS

* exported "TRADE".ORDEREJB" 152.6 KB

* exported "TRADE".HOLDINGEJB" 86.25 KB

* exported "TRADE".QUOTEEJB" 60.97 KB

* exported "TRADE".ACCOUNTEJB" 29.89 KB

* exported "TRADE".ACCOUNTPROFILEEJB" 43.86 KB

* exported "TRADE".KEYGENEJB" 5.289 KB

Master table "TRADE","SYS_EXPORT_SCHEMA_01" successfully loaded/unloaded

************************************************************************************

***

Dump file set for TRADE.SYS_EXPORT_SCHEMA_01 is:

/u/oracle2/tradeschema.dmp

Job "TRADE","SYS_EXPORT_SCHEMA_01" successfully completed at 12:20:25
```

Data Pump Export 完成完成后，我们执行了 `ls` 命令检查创建的文件；输出如示例 10-6 所示。

Example 10-6 Checking with the command

```
--rw-rw---- 1 HAIMO SYS1 524288 Oct 31 16:45 tradeschema.dump

--rw-rw-r-- 1 HAIMO SYS1 1981 Nov 5 12:20 tradeschema.log
```

