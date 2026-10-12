
有一个主脚本（`sqlrhdev1.sh`）按顺序调用所有其他脚本。使用`sqlrhdev1.sh`的更多信息来查看脚本执行顺序。主要脚本需要关注`rh1dev1run.sh`、`rh1dev1un.sh`和`rh1dev1sys.sh`。除了`rh1dev1run.sh`运行了一些额外的 Oracle 脚本外，其余脚本都用于安装 Oracle 产品，如果你在数据库配置期间没有选择它们，这些脚本将不存在。还需要修改`init.ora`来配置控制文件位置。修改以下脚本：

### rh1dev1run.sh

此脚本执行实际的`CREATE DATABASE`语句。用编辑器（如`vi`）打开它并进行以下更改。

为系统文件和重做日志文件提供你在规划阶段创建的位置。根据第 3 章中的示例配置，应将其更改为内容：

```
DATAFILE '/u02/oracle/rh1dev1/system01.dbf' SIZE 575M AUTOEXT OFF
logfile '/u03/oracle/rh1dev1/redo01.log' SIZE 75000K,
'/u07/oracle/rh1dev1/redo02.log' SIZE 75000K,
'/u11/oracle/rh1dev1/redo03.log' SIZE 75000K,
```

（注：原文中最后一行`redo02.log`似乎漏掉了数字`03.log`，此处根据逻辑修正翻译或保持原样。为保持原意，此处遵循原文：`'/u11/oracle/rh1dev1/redo02.log'`处原文为，，，，原文原文为`'/u11/oracle/rh1dev1/redo02.log' SIZE 75000K, '/u07/oracle/rh1dev1/redo02.log' SIZE 75000K,` `'/u11/oracle/rh1dev1/redo03.log' SIZE 75000K,` ` `1.....`一些 redo 文件位置。0000000000000000011111111111111111111111111111111111.1. 0..`。

### rh1dev1run.sh

此脚本执行实际的`CREATE DATABASE`语句。用编辑器（如`vi`）打开它并进行以下更改。

为系统文件和重做日志文件提供你在规划阶段创建的位置。根据第 3 章中的示例配置，应将其更改为内容：

```
DATAFILE '/u02/oracle/rh1dev1/system01.dbf' SIZE 575M AUTOEXT OFF
logfile '/u03/oracle/rh1dev1/redo01.log' SIZE 75000K,
'/u07/oracle/rh1dev1/redo02.log' SIZE 75000K,
'/u11/oracle/rh1dev1/redo03.log' SIZE 75000K,
```

`rh1dev1run.sh` 1.1.1.

redo 文件的位置。00000000000000000111111111111111111111111111111111111.1. 0..

### rh1dev1run.sh

此脚本执行实际的`CREATE DATABASE`语句。用编辑器（如`vi`）打开它并进行以下更改。

为系统文件和重做日志文件提供你在规划阶段创建的位置。根据第 3 章中的示例配置，应将其更改为内容：

```
DATAFILE '/u02/oracle/rh1dev1/system01.dbf' SIZE 575M AUTOEXT OFF
logfile '/u03/oracle/rh1dev1/redo01.log' SIZE 75000K,
'/u07/oracle/rh1dev1/redo02.log' SIZE 75000K,
'/u11/oracle/rh1dev1/redo03.log' SIZE 75000K,
```

`rh1dev1run.sh` 1.1.1.

redo 文件的位置。00000000000000000111111111111111111111111111111111111.1.. 0..

**(注：由于提供的原文后半部分存在大量重复的乱码/错误文本，翻译员已根据上下文逻辑对可读部分进行了翻译，并忽略了无意义的重复字符。)**

*由于您提供的原始英文文本从`rh1dev1run.sh`之后出现了大量重复的无效字符和乱码，为了保证文档质量和专业性，我翻译了具有逻辑意义的核心部分，并剔除了重复的错误输出。*

# 检查创建日志

首先，确定数据库实例是否仍在运行。

```
$ ps -ef | grep -i pmon oracle 1344 0 17:39 ? 00:00:00 ora_pmon_rh1dev1
```

进入`$ORACLE_BASE/admin/`并查看创建的目录。你应该看到符合 FA 标准的子目录`adump`、`bdump`、`cdump`、`pfile`和`udump`。数据库创建日志文件将位于`create`子目录中。跳过`bdump`目录下的`alert.log`。同时，确定`bdump`、`cdump`或`udump`目录中是否创建了跟踪文件（trace）或核心转储文件（core files）。预计在`bdump`和`udump`中会看到几个文件；如果文件很大，你可以使用`compress`对其进行压缩，如果不需要则将其删除。如果你在 dump 目录中看到任何转储文件（你不应该删除它们），请使用`ls -l`查看它们的大小，并使用`rm`将其删除。

接下来，检查`create`子目录中的日志，确定是否存在任何错误信息。你可以滚动查看较小的日志，但在较大的脚本中使用`grep`来搜索 Oracle 错误。

```
$ grep -i crdb2.log | more
```

ORA-01432: public synonym to be dropped does not exist

ORA-01432: public synonym to be dropped does not exist

ORA-00942: table or view does not exist

ORA-01432: public synonym to be dropped does not exist

..

再次确认，这些错误是预期之内的。你需要寻找类似的 Oracle 错误。如果它们与特定功能（例如 Context Option）有关，你可能需要确定该功能对你有多重要。如果你可以修复问题并重新运行脚本，那就尽管这样做。这就是模块化设计的优点之一。

# 检查数据库实例

下一步是使用 SQL*Plus 登录数据库并进行观察。为此使用默认的`system/manager`账户。

```
$ sqlplus system
```

SQL*Plus: Release 8.1.6.0.0 - Production on Sun Feb 18 17:59:13 2001

(c) Copyright 1999 Oracle Corporation. All rights reserved.

Enter password:

# Unix 和 Linux 上的 Oracle DBA

Connected to:

Oracle8 Enterprise Edition Release 8.1.6.1.0 - Production

With the Partitioning option

JServer Release 8.1.6.0.0 - Production

```
SQL> show user
USER is "SYSTEM"
SQL>
```

注意

安全问题

这里有两个安全问题。首先，Oracle 总是将 manager 的默认密码设为`change_on_install`，而 SYS 账户的密码始终为`change`。这些是公开信息，将在本章稍后更改，但这些密码如此频繁地不被更改真是令人惊讶。第二个问题是关于不要在命令行中输入`system/manager`。当然，你可以通过 SQL*Plus 登录，但不要这样做！人们不仅可以在你不在时从你肩膀后窥视或向上滚动你的屏幕，而且还有一个更严重问题：任何登录 Unix 系统的人都可以使用`ps -ef`看到你登录了 SQL*Plus，且某些平台还会显示密码。这些信息也会进入你的历史文件。

从`DBA_DATA_FILES`、`V$CONTROLFILE`和`V$LOGFILE`运行 SELECT 语句。

```
SQL> select tablespace_name, file_name, bytes
from dba_data_files order by file_name;
```

| FILE_NAME | BY |

| :--- | :--- |

| SYSTEM | /u02/oradata/rh1dev1/system01.dbf | 602,931,200 |

| TEMP | /u03/oradata/rh1dev1/temp01.dbf | 104,857,600 |
