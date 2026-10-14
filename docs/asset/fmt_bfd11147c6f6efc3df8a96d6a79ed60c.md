
| Variable_name | Value |
|---|---|
| back_log | 5 |
| connect_timeout | 5 |
| basedir | /usr/ |
| datadir | /var/mysql/ |
| delayed_insert_limit | 100 |
| delayed_insert_timeout | 300 |
| delayed_queue_size | 1000 |
| join_buffer | 131072 |
| flush_time | 0 |
| key_buffer | 8388600 |
| language | /usr/share/mysql/english/ |
| log | OFF |
| log_update | OFF |
| long_query_time | 10 |
| low_priority_updates | OFF |
| max_allowed_packet | 1048576 |
| max_connections | 100 |
| max_connect_errors | 10 |
| max_delayed_insert_threads | 20 |
| max_join_size | 4294967295 |
| max_sort_length | 1024 |
| net_buffer_length | 16384 |
| port | 3306 |
| protocol-version | 10 |
| record_buffer | 131072 |
| skip_locking | ON |
| socket | /tmp/mysql.sock |
| sort_buffer | 2097144 |
| table_cache | 64 |
| thread_stack | 65536 |
| tmp_table_size | 1048576 |
| tmpdir | /tmp/ |
| version | 3.22.21 |
| wait_timeout | 28800 |

34 rows in set (0.00 sec)

## 表优化

在执行大量更新或删除大量记录后，优化表很重要。只有当表包含具有可变大小字段的列时才需要优化，例如`varchar`、`blob`或`text`。优化将维护删除操作产生的未使用空间。假设`course`表包含一个名为`name`的列，其类型为`varchar`。如果删除了大量行，优化表以节省磁盘空间会很好。以下示例展示了如何优化`course`表：

```
mysql>optimize table course;
```

## 表锁定

尽管 MySQL 中的所有操作都是原子的，但你可能希望对某些操作进行锁定以按顺序执行。MySQL 不是事务环境，因此当你的更新相互依赖时应小心。你可以通过输入以下命令对表施加读锁或写锁：

```
mysql> lock tables student read, course write;
```

对表执行你想要的操作，然后使用以下命令解锁表：

```
mysql> unlock tables;
```

## 调用编辑器

有时当你想编写一个很长的 SQL 脚本时，你不想使用 MySQL 解释器。在这种情况下，你可以调用编辑器。编辑器可以用以下命令调用：

```
mysql>edit;
```

默认编辑器是系统 shell 中`$EDITOR`变量定义的编辑器。你可以通过输入以下内容使用 bash 将此变量重新定义为 pico：

```
bash$export EDITOR=pico
```

## 杀死线程

杀死线程意味着将用户从数据库服务器断开。每个连接都使用一个线程，因此，当你杀死特定线程时，你实际上是在关闭连接，如下所示：

```
mysql>kill thread_id
```

你可以通过列出当前使用 MySQL 的进程来获取`thread_id`。这是通过`show processlist`命令完成的：

```
mysql> show processlist;
```

| Id | User | Host | db | Command | Time | State | Info |
|---|---|---|---|---|---|---|---|
| 9 | root | localhost | mysql | Sleep | 18857 | NULL | NULL |
| 17 | joeadlib | localhost | trial | Query | 0 | NULL | show processlist |

2 rows in set (0.00 sec)

## MySQL 中的注释

MySQL 中的注释与大多数数据库 shell 中的注释不同，使用起来很容易。MySQL 支持两种类型的注释：
- 井号 (`#`)
- C 风格注释 (`/* */`)

以下是它们用法的示例：

```
mysql> select * from student;  #select all students in table

mysql>select * '/we are going to select all/'

  from student; /*the students in the table */
```

如你所见，你可以在查询语句的主体中插入 C 风格注释 (`/* */`)。

> 注意 MySQL 不支持大多数数据库使用的`--`注释。这种注释风格无法与 MySQL 配合使用，因为它无法被 MySQL 轻松解释。由于可能引起的问题，没有计划支持它。如果你有一个包含此类型注释的 SQL 文件，你可以使用 MySQL 附带的`replace`命令轻松将其更改为 MySQL 注释风格：

```
bash$replace ".." "#" -- file.sql
```

## 解析 MySQL 文件

你可以将所有想要的查询写在一个文本文件中并解析它，以便一次性由 MySQL 执行。这是通过先编辑文件并保存它，然后执行以下命令来完成的：

```
bash$mysql < mysql_file.sql
```

## 你会错过的东西

不幸的是，MySQL 缺少一些尚未实现的重要功能。其中大多数都在 MySQL 的待办事项列表上，但直到它们实现之前，你将不得不绕过它们：
- 子查询—你不能使用以下任何类型的内容：
- `select ..from .. where .. in (select .. from .. where ..)`

在大多数情况下，你可以通过使用`join`或逻辑`and`来解决这个问题。以下是使用`join`执行子查询的示例：

以下查询

```
select * from course where sid in (select id from student);
```

可以写成

```
select course.* from course left join student

on course.sid=student.id where student.id is not null;
```

- 选择到表—你不能使用以下任何类型的内容：
- `select ..from .. into table ..`

MySQL 不支持此格式。但是，这可以通过使用以下方法来完成：

```
insert into table select .. from ..
```
