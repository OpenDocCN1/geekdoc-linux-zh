
# 第 3 章

## 事务

这里有一个简短但非常重要的话题，我们目前为止几乎没有提到过，那就是事务支持。在编写本文内容时，`PostgreSQL` 对事务的支持是其他开源数据库所缺乏的主要特征之一。

默认情况下，当我们在 `PostgreSQL` 上执行数据操纵语句时，每条语句都是独立执行的，要么成功要么失败。它绝不会出现“部分成功”的情况，因为 `PostgreSQL` 确保所有语句要么执行并成功完成，要么完全不改变任何数据。

有时，我们在几条不同的语句之间需要这种行为，特别是在通常情况下，即任何时候都可能有多个用户正在使用数据库。假设在我们的 DVD 店中，有一个“待售”区域，我们定期地将旧库存从租赁区域移动到销售区域。这可能涉及至少两条 SQL 语句：一个用于从租赁区域删除该 DVD，另一个用于将其添加到销售区域。如果应用程序在执行过程中发生了错误，这盘 DVD 可能会丢失，除非我们确保这两条 SQL 语句都成功，或者一个都不成功。

这是通过事务来实现的，在概念上非常简单。在执行第一条 SQL 数据操纵语句之前，我们执行 `BEGIN WORK`。在最后一条 SQL 命令之后，我们可以使用 `COMMIT` 语句让两条操作都成功，也可以使用 `ROLLBACK` 命令让它们都失败。

在底层，`PostgreSQL` 尽了大量工作来支持这个表面上简单的想法，但幸运的是，我们通常不需要担心它。然而，有一点你应该注意：如果另一个用户在第一条语句执行之后、`COMMIT` 或 `ROLLBACK` 之前查看数据库，数据看起来似乎已经发生了变化。如果执行了 `ROLLBACK`，数据将恢复到原先的值。但是，`PostgreSQL` 不允许你看到另一个进程正在插入但尚未提交的“新”数据。

针对高级用户的提示：`PostgreSQL` 默认的事务隔离级别允许非重复读和幻影读，但不允许脏读。

对于非高级用户，即我们大多数人，只需要注意到在多用户用户的情况下，偶尔数据可能会在出乎意料的情况下发生变化。这种看似奇怪行为的原因是为了最大化性能。在本章中，我们没有空间深入讨论事务级别这一复杂主题，以及 `PostgreSQL` 默认行为的优缺点。

以下是 `BEGIN`、`COMMIT` 和 `ROLLBACK` 运行的快速示例：

```
Dname= BEGIN WORK;

BEGIN

dname= INSERT INTO children (fname, age) VALUES ('Fred', '1');

INSERT 20479 1

dname= INSERT INTO children (fname, age) VALUES ('Freda', '2');

INSERT 20480 1

dname= ROLLBACK;

ROLLBACK

dname= SELECT * FROM children;

childno= fname age
```

![](img/930f7611cac03a5cd5573f4bb94fd7b_125_0.png)

## 数据库

| id | fname | age |
| :--- | :--- | :--- |
| 1 | Andrew | 10 |
| 2 | Jenny | 14 |
| 3 | Alex | 11 |
| 4 | Adrian | 5 |
| 5 | Allen | 4 |

(5 行) 如果我们想保存更改，我们将执行一个 `COMMIT`，如下所示：

```
Dbname=# BEGIN WORK;

BEGIN

Dbname=# INSERT INTO children (fname, age) VALUES ('Fred', '1');

INSERT 20481 1

Dbname=# INSERT INTO children (fname, age) VALUES ('Freda', '2');

INSERT 20482 1

Dbname=# COMMIT;

COMMIT

Dbname=# SELECT * FROM children;

childno|fname age
```
