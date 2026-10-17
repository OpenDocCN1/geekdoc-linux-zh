
表空间备份允许你在数据库在线运行时备份单个表空间。通过通知 Oracle 你将对该表空间执行备份，你将导致采取特殊操作，这在后面的章节“OS 设施：在线备份”中有介绍。一旦表空间被标记为备份，使用操作系统或第三方实用程序备份组成该表空间的一个或多个数据文件。

![](img/9479df2d00f5e62b87366b125224950f_316_0.png)

> 注意
> *无论你是进行在线还是离线备份，如果你正在从 OCFS 分区备份数据文件，请确保你使用支持 `O_DIRECT` 的实用程序。从 www.ocfs.org 可以获得常见程序（如 `cp`、`mv` 和 `cpio`）的 OCFS 感知版本。在该网站上，你将能够找到适用于你的应用程序和平台的正确软件包。*

当你将表空间标记为备份时，Oracle RDBMS 将知道此在线备份已发生，如果需要恢复，它将知道如何恢复数据库。在下一节中，你将学习执行此类备份的实际机制。

## 增量备份

仅在使用 RMAN 或第三方备份应用程序（如 Legato、NetBackup 或 Veritas）时才可能进行增量备份；较旧的备份系统的外部方法只允许你备份整个数据文件。数据文件的内容对操作系统是未知的；因此，增量备份不起作用。使用 RMAN，你可以只备份自上一次备份以来更改的数据。

有两种类型的增量备份。差异增量备份备份自上一次增量备份以来更改的所有数据。累积增量备份备份自上一次完全备份以来更改的所有数据。

### 差异增量备份

*差异增量*备份取自上次完全备份或上次增量备份以来更改的数据，并备份这些数据。由于仅备份更改的数据，因此备份的数据量最小化。然而，由于仅备份更改的数据，为了将数据恢复到故障点，必须恢复完全备份和自完全备份以来的所有差异增量备份。这可能非常耗时，需要更多的工作。图 11-1 中显示了一个差异增量备份。正如你所看到的，每个备份只取自上次完全备份或增量备份以来所做的更改。

![](img/9479df2d00f5e62b87366b125224950f_317_0.png)

图 11-1. 差异增量备份

### 累积增量备份

使用累积增量备份时，自上次完整备份以来发生的所有更改都会被备份。每个累积增量备份占用的空间都比差异增量备份多，但如果在恢复时，只需要应用完整备份和最后一个累积增量备份即可。此过程如图 11-2 所示。

## 如何备份数据库

Oracle 数据库有多种不同的备份方式。这些方法包括：

- 恢复管理器 (`RMAN`)
- 自动基于磁盘的备份和恢复（闪恢复区）
- 操作系统工具
- 导出和数据泵 (`Export and Data Pump`)
- 市售备份实用程序

这些实用程序中的每一个都能执行有效的备份。通常，决定使用哪一种方法取决于您个人的偏好。

![](img/9479df2d00f5e62b87366b125224950f_318_0.png)

![](img/9479df2d00f5e62b87366b125224950f_318_1.png)

## 恢复管理器 (RMAN)

恢复管理器 (`RMAN`) 是 Oracle 提供的用于执行备份和恢复操作的工具，并与许多第三方工具集成以用于备份 Oracle 数据库。`RMAN` 自 Oracle 7.3 版本就已存在，并成为执行 Oracle 备份的首选方法之一。它是 Oracle Server 的一部分，因此不需要单独的许可证。

**提示**

*`RMAN` 可以通过可执行文件 `rman` 来运行。在 Linux 等某些操作系统中，存在一个与 Oracle 无关的额外 `rman` 命令。为了确保执行的是正确的 `rman` 命令，您可能需要使用命令 `$ORACLE_HOME/bin/rman` 来调用它。*

### 设置恢复管理器

在使用恢复管理器之前，必须创建恢复目录。恢复目录位于自己的表空间中，通常称为 *`rvcata`*，除了目录本身，还必须先创建目录的模式（schema）和所有者。使用以下 SQL 语句创建表空间、模式、所有者和目录。

1. 连接到 DBMS。

   ```sql
   SQL> connect / as sysdba
   ```

2. 为恢复目录创建表空间、模式和用户。

   ```sql
   SQL> SPOOL recovery_log
   SQL> CREATE TABLESPACE rvcata DATAFILE
     '/opt/oracle/product/10.1.0/oradata/rvcata01.dbf'
     SIZE 512m AUTOEXTEND ON NEXT 32m MAXSIZE UNLIMITED
     EXTENT MANAGEMENT LOCAL AUTOALLOCATE
     SEGMENT SPACE MANAGEMENT AUTO;
   SQL> CREATE USER rman IDENTIFIED BY rman
     TEMPORARY TABLESPACE temp
     DEFAULT TABLESPACE rvcata QUOTA unlimited ON rvcata;
   ```

   用户已创建。

3. 将 `RECOVERY_CATALOG_OWNER` 角色授予模式所有者。此角色提供维护并查询恢复目录所需的所有权限。

   ```sql
   SQL> GRANT RECOVERY_CATALOG_OWNER TO rman;
   Grant succeeded.
   SQL> exit;
   Disconnected from Oracle Database 10g Enterprise Edition Release 10.1.0.2.0 - Production
   With the Partitioning, OLAP and Data Mining Options
   ```

4. 创建目录所有者后，使用 RMAN `CREATE CATALOG` 命令创建目录表。该命令在目录所有者的默认表空间中创建目录。

   ```bash
   [oracle@pt6c admin]$ $ORACLE_HOME/bin/rman CATALOG rman/rman
   ```

   ```text
   Recovery Manager: Release 10.1.0.2.0 - Production

   Copyright (c) 1995, 2004, Oracle. All rights reserved.
   connected to recovery catalog database
   recovery catalog is not installed

   RMAN> CREATE CATALOG
   recovery catalog created

   RMAN>
   ```

   这将创建恢复目录。一旦创建目录，就可以使用 RMAN 备份数据库。

   > **注意**
   > *恢复目录应在其独立的数据库中创建。如果您要备份的数据库损坏，恢复目录也会损坏。*

## 使用 RMAN

恢复管理器 (`RMAN`) 可以配合或不配合恢复目录或存储库使用。然而，为了充分利用恢复管理器，您应该使用恢复目录。一旦按照前一节所示创建了恢复目录，您可以使用以下命令连接：

1. 如果目标数据库未装载，请将其装载或打开。

   ```sql
   SQL> STARTUP MOUNT;
   ```

   ```bash
   [oracle@spc6 admin]$ $ORACLE_HOME/bin/rman TARGET / CATALOG rman/rman
   ```

   ```text
   Recovery Manager: Release 10.1.0.2.0 - Production

   Copyright (c) 1995, 2004, Oracle. All rights reserved.

   connected to target database: ORCL (DBID=1955397586)
   connected to recovery catalog database
   RMAN>
   ```

   > **注意**
   > *此代码假设环境变量中已设置目标数据库的 `ORACLE_SID`、`ORACLE_HOME`、`LD_LIBRARY_PATH` 和 `PATH`，且引用该数据库的 Oracle 主目录；如果未设置 `ORACLE_SID`，您必须使用数据库的 TNS 别名如下：*

   ```bash
   [oracle@spc6 admin]$ $ORACLE_HOME/bin/rman TARGET sys/<password>@*target_database*> CATALOG rman/rman
   ```

2. 调用 RMAN 实用程序后，必须在恢复目录中注册目标数据库，以便对其进行备份。这是通过 RMAN 内部的 `REGISTER DATABASE` 命令完成的。
