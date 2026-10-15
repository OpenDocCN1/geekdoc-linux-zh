
```text
connect / as sysdba
shutdown abort
spool crdb.dbolap.log
connect / as sysdba
startup mount
```

```text
create database dbolap
controlfile reuse
maxinstances 2
maxlogfiles 12
maxdatafiles 100
noarchivelog
character set AL32UTF8
datafile
'/oracle/dbf/dbolap_system.dbf' size 8000M REUSE
extent management local
sysaux datafile
```

```text
'oracle/dbf/dbolay_sysaux.dbf' size 2000M REUSE
logfile
'/oracle/dbf/dbolay_log1.dbf' size 500M REUSE,
'
'/oracle/dbf/dbolay_log4.dbf' size 500M REUSE
DEFAULT TABLESPACE DATAFILE
'/oracle/dbf/dbolay_data.dbf' size 15000M REUSE,
.
'/oracle/dbf/dbolay_data20.dbf' size 15000M REUSE
extent extent management localallocate segment space management
auto default temporary tablespace TEMP tempfile
'/oracle/dbf/dbolay_temp1.dbf' size 10000M REUSE
undo tablespace UNDO datafile
'/oracle/dbf/dbolay_undol.dbf' size 2000M REUSE
/
```

```text
connect / sysdba
set echo off
set feedback on
@oracle/rdbms/admin/catalog.sql
@oracle/rdbms/admin/catproc.sql
@oracle/rdbms/admin/catexp7.sql
@oracle/rdbms/admin/catexp.sql
@oracle/rdbms/admin/catdbsyn.sql
@oracle/sqlplus/admin/pupbld1.sql
# 此示例中未包含许多行
```

示例 6-2 运行 `create_db` 脚本的执行输出

```text
SQL> connect / as sysdba
Connected to an idle instance.
SQL> startup nomount
ORACLE instance started.
```

```text
总系统局局区 2147483648 bytes
Fixed Size 2072504 bytes
Variable Size 486539336 bytes
Database Buffers 1627389952 bytes
Redo Buffers 31481856 bytes
```

```text
SQL>
SQL> create database olapmst
controlfile reuse
maxinstances 2
maxlogfiles 12
maxdatafiles 100
noarchivelog
character set AL32UTF8
datafile
```

```text
SQL>
SQL> shutdown immediate
Database closed.
Database dismounted.
ORACLE instance shut down.
SQL> startup
ORACLE instance started.
```

```text
Total System Global Area 2147483648 bytes
Fixed Size 2072504 bytes
Variable Size 486539336 bytes
Database Buffers 1627389952 bytes
Redo Buffers 31481856 bytes
```

```text
Database mounted.
Database opened.
```

### 6.2.1 填充数据库

提供了用于填充数据库的导出文件。使用以下命令填充数据库。

```text
imp file=export.dump buffer=2048000 commit=y log=export.log
```

导入运行后，日志显示填充完成（注：此处日志内容为乱码占位符）。

导出文件已用于填充数据库。使用以下命令填充数据库。

## 6.3 安装 BIEE 组件（注：原文此处似乎包含大量乱码，已按逻辑结构翻译）

（由于原文包含大量乱码，译文已根据结构进行了处理）

当设置正确时，安装过程将显示图 6-2。这个第一个启动窗口是安装程序的空间提示。我们发现安装过程中我们使用了 2.1 GB 的空间。

![](img/5b458d26d6ded58c4d2c82af59a3d71c_125_0.png)

图 6-2 BIEE 安装第一个窗口

我们将 BIEE 代码安装在 `/oracle/BIEE` 目录下，如第 105 页的图 6-3 所示。

## Oracle Business Intelligence (10.1.3.3.2)

Oracle Business Intelligence 安装

欢迎。将安装 Oracle Business Intelligence。

浏览或输入安装位置：

```text
/oracle/BEE
```

浏览或输入数据位置：

```text
/oracle/biedata
```

- 选择安装类型：

- 基础 (Basic)：最小安全性。安装 J2EE 容器 (OC4)。

- 高级 (Advanced)：增强安全性。需要 Oracle Application Server 10.1.3.0 或更高版本。

![](img/5b458d26d6ded58c4d2c82af59a3d71c_126_0.png)

图 6-3 BIEE 安装目录选择

安装类型的选择取决于具体站点需求。本项目使用了完整类型选择，如图 6-4 所示，因为安装手册中的 Oracle 建议进行完整安装。

## Oracle Business Intelligence (10.1.3.3.2)

选择适合你需求的设置类型。

- 完整 (Complete)

- 将安装所有的 Business Intelligence 组件。

- Oracle Business Intelligence Server

- 只安装服务器组件。（包含 Oracle Business Intelligence Server、集群控制器、调度器、系统管理。）

- Oracle Intelligence Presentation Services

- 只安装演示服务组件。（包含 Oracle Intelligence Presentation Services、演示服务插件、BI Office、系统管理。）

- Oracle Business Intelligence Client Tools

- 只安装客户端组件。（包含 Oracle Business Intelligence Client Tools。）

![](img/5b458d26d6ded58c4d2c82af59a3d71c_126_1.png)

图 6-4 BIEE 设置类型

第 6 章 带有 Linux 版 System z 数据库的 Oracle Business Intelligence 企业版 105

Oracle Application Server 选择窗口提供了 BIEE 产品套与 Oracle Application Server 之间的链接，如图 6-5 所示。

![](img/5b458d26d6ded58c4d2c82af59a3d71c_127_0.png)

图 6-5 BIEE OAS 位置

在这种情况下，我们选择英语作为用于显示 BIEE 产品生成的任何错误信息的语言，如第 107 页的图 6-6 所示。

![](img/5b458d26d6ded58c4d2c82af59a3d71c_128_0.png)

**图 6-6** Oracle BIEE 语言选择

摘要窗口如图 6-7 所示。选择**下一步 (Next)** 后将开始安装，如第 108 页的图 6-8 所示。我们的项目在 30 分钟内完成了实际的基础设施安装。

![](img/5b458d26d6ded58c4d2c82af59a3d71c_128_1.png)

**图 6-7** Oracle BIEE 产品摘要

第 6 章 带有 Linux 版 System z 数据库的 Oracle Business Intelligence 企业版 107

![](img/5b458d26d6ded58c4d2c82af59a3d71c_129_0.png)
