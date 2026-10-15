
通过以下步骤设置在引导启动时调用 `dbstart` 和 `dbshut`：

1. 编辑 `/etc/oratab` 文件，其条目格式为：

`ORACLE_SID:ORACLE_HOME:(Y|N)`

其中 `Y` 或 `N` 分别指定使用或不使用 `dbstart` 和 `dbshut` 来启动和关闭数据库。对于你不希望自动启动和关闭链接到操作系统的数据库，将其值改为 `Y`。

2. 如果文件不存在，在 `/etc/rc.d/init` 目录下创建一个名为 `dbora` 的文件。

3. 在 `dbora` 文件的末尾，放置类似于示例所示所示条目。确保使用完整路径。

# Set ORA_HOME to the location of

`ORACLE_HOME`=`/u01/app/oracle/product/8.0.5`

`ORACLE_SID`=`oracle`

```bash
## Test for the presence of dbstart
if [ ! -f $ORACLE_HOME/bin/dbstart ]; then
  echo "Oracle startup: cannot start"
  exit
fi

# Assuming dbstart is in the right place
case "$1" in
  'start')
    # Start the Oracle databases
    su oracle -c $ORACLE_HOME/bin/dbstart &
    ;;
  'stop')
    # Or, stop the Oracle databases in background
    su oracle -c $ORACLE_HOME/bin/dbshut &
    ;;
esac
```

# Link dbora to operating system startup with a command

`-s /etc/rc.d/init.dbora /etc/rc.d`

指定启动和关闭选项后，你作为 root 的工作完成。

## 总结

准备 Linux DBMS 意味着：

- 理解并使用有效的模式设计，这反需要规范化理论
- 清明确目标平台的资源，以及这些资源如何增长以适应数据库
- 掌握并正确使用安装任何 DBMS 所需的基础 Linux 概念和命令（如 `chmod` 和 `groupadd`）
- 查看特定特定的安装说明

## 第10 章：与数据库交互

## 第11 章：Linux 数据库工具

## 与数据库交互

作为 Linux 数据库管理员，你将以多种方式与 DBMS 交互。本节讨论了三种常见但同样关键的操作：

- 导出数据库
- 导入文本文件
- 显示数据库摘要信息

## 与 MySQL 交互

MySQL 提供了命令行工具，通过这些工具你可以导出一个或多个数据库的内容；将文本导入 MySQL 数据库以填充表；以及显示数据库、表和字段名称。

## 导出数据库

你必须使用 `mysqldump` 工具导出一个或多个 MySQL 数据库，以便备份或传输到另一个 MySQL 服务器。此类导出可以包含创建或填充表所需的 MySQL 语句。

以下三个命令都是 `mysqldump` 工具泛化语法的示例。

```
# mysqldump [OPTIONS] database [tables]
# mysqldump [OPTIONS] --databases [OPTIONS]
DB1 DB2 DB3...
# mysqldump [OPTIONS] --all-databases
[OPTIONS]
```

表 10-1 总结了此语法。

### 表 10-1

`mysqldump` 语法

| 语法 | 效果 |
|---|---|
| # mysqldump [OPTIONS] database [tables] | 根据给定的选项，导出指定数据库和表的内容 |
| mysqldump [OPTIONS] --databases [OPTIONS] DB1 [DB2 DB3..] | 根据给定的选项，导出指定数据库的内容 |
| mysqldump [OPTIONS] --all-databases [OPTIONS] | 导出所有数据库的内容 |

如果你不提供表名，或者使用 `--databases` 或 `--all-databases` 选项，`mysqldump` 将输出每个数据库中的所有内容。

以下是我认为最有用的 `mysqldump` 选项列表：

- `mysqldump --add-locks`——在每次导出期间前锁定表，在导出后解锁；可提供更快的插入速度。
- `mysqldump -A` 或 `mysqldump --all-databases`——导出所有数据库。
- `mysqldump --allow-keywords`——创建包含关键字的列名；其工作原理是使 `mysqldump` 的每个列名都以相应的表名开头。
- `mysqldump -C` 或 `mysqldump --compress`——压缩客户端和服务器之间传输的所有信息；假设客户端和服务器都支持压缩。
- `mysqldump -B` 或 `mysqldump --databases`——导出多个数据库，需要提供表名，因为所有参数都被视为数据库名。
- `mysqldump -F` 或 `mysqldump --flush-logs`——在开始导出之前刷新所有 MySQL 日志文件。
- `mysqldump -f` 或 `mysqldump --force`——即使在导出过程中发生 SQL 错误也完成导出。
- `mysqldump -h` 或 `mysqldump --host=` 命名主机——从活动 MySQL 服务器导出到命名的主机；`host` 参数的默认值是 `localhost`。
- `mysqldump -l` 或 `mysqldump --lock-tables`——在开始导出之前锁定所有表。
- `mysqldump -d` 或 `mysqldump --no-data`——不写入行信息；当只需要导出表结构时非常有用。
- `mysqldump --password` 或 `mysqldump --password=password`——在开始导出之前，使用提供的密码允许的权限连接到 `mysql` 服务器。
- `mysqldump -q` 或 `mysqldump --quick`——不带缓存执行导出；直接导出到标准输出。
- `mysqldump -u username` 或 `mysqldump --user=username`——在执行导出前以指定的用户连接到 MySQL 服务器；`username` 的默认值是当前用户的操作系统登录名。
- `mysqldump -w` 或 `mysqldump --where="condition"`——仅导出由子句中条件指定的记录，该子句需要单引号。

可以使用 `mysqldump` 选项来显示具有特定特征的记录，同时将这些记录传输到另一个 MySQL 数据库，语法如下：

```
mysqldump --database_of_gardening \
where=plant_name='zinnia' | mysql \
--host=far_away_machine -C db_of_gardening
```

## 文本文件

MySQL `LOAD DATA` 语句的命令行界面是 `mysqlimport`。该实用接受的大多数选项与该语句的选项相同。

使用以下通用语法启动 `mysqlimport`：

```
# mysqlimport [options] database ASCII file 1 [ASCII file 2] \
[ASCII file 3]
```

在命名或决定 `mysqlimport` 可能处理的文件时要小心。该工具会剥离导入文件名的任何扩展名，并使用结果来决定指定数据库中的哪个表将接收文件内容。因此，如果你想将名为 `vegetables.txt` 的文件导入到 `gardening` 数据库中的 `collectibles` 表，你必须先将文本文件重命名为 `collectibles.txt`。否则，`mysqlimport` 将导入结果放在名为 `veggies` 的新表中。

表 10-2 总结了 `mysqlimport` 最有用的选项。

### 表 10-2

`mysqlimport` 选项

| 选项 | 效果 |
|---|---|
| -C 或 --compress | 在客户端和服务器之间移动时压缩所有信息；假设双方支持压缩。 |
| -d 或 --delete | 在导入文本文件之前删除表中所有现有数据 |
| -f 或 --force | 忽略错误，例如文本文件在数据库中没有对应的预存表。这使 `mysqlimport` 尝试导入下一个文本文件（如果有）。如果没有此选项，当不存在接收文件内容的表时，`mysqlimport` 将退出。 |
| -h host_name 或 --host=host_name | 将数据导入到主机指定的主机上的 MySQL 服务器 |
