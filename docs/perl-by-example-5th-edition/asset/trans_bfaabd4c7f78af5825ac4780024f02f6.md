

与英语及其众多方言类似，SQL 也发展出了许多不同的“风味”。当今的 SQL 基于 IBM 最初的实现版本，并在此基础上增加了相当多的内容。制定标准的目的是帮助规范语言中应支持哪些功能。1986 年，ANSI 制定了 SQL 标准。随后在 1989 年、1992 年和 1999 年进行了修订。目前最常用的标准是 SQL92，它代表了原始规范（SQL2）的第二次修订。大多数商业数据库（MySQL、Oracle、Sybase、Microsoft Access 和 Microsoft SQL Server）都支持完整的 SQL2，并声称 100% 符合该标准。然而，该标准相当复杂，就像英语的不同方言一样，各个供应商在其版本的 SQL 中添加了自己的扩展功能，这使得很难保证应用程序能在所有 SQL 服务器数据库上运行。

在本附录中，我们重点关注基本 SQL 语言，并探讨诸如创建表、插入、删除和选择数据等概念。

### B.1.2 执行 SQL 语句

由于本书讨论的数据库管理系统是 MySQL，因此以下示例中使用的服务器是 MySQL 数据库服务器，大多数 SQL 命令将在 mysql 命令行客户端执行，尽管你可能更倾向于使用 MySQL 查询浏览器。一旦连接到数据库，你只需在 mysql 控制台（命令行窗口；见图 B.1）中输入命令即可，具体方法在第 15 章中有说明。

![](img/8556abcb353c0991f12099420ec28735_753_0.png)

**图 B.1** *mysql* 控制台。

**MySQL 查询浏览器。** 要在 MySQL 查询浏览器中运行 SQL 命令，请在应用窗口顶部的框中输入命令，然后单击“执行”按钮。一旦单击“执行”按钮（查询窗口右侧的绿色按钮），结果将以 ResultSet 选项卡的形式显示在应用的中心位置（见图 B.2）。

![](img/8556abcb353c0991f12099420ec28735_754_0.png)

### B.1.3 关于 SQL 命令/查询

SQL 是一种计算机语言，与大多数语言一样，SQL 有其规则、语法以及一组特殊或保留字。多年来，不同的关系型数据库供应商为了竞争，提供了额外的数据操作功能，因此该语言演变出了不同的变体。本节涵盖了基本的 SQL 命令和语法。由于 SQL 命令众多，它们被分为两大类：用于操纵表中数据的命令和用于操纵数据库本身的命令。网上有许多优秀的教程涵盖了所有 SQL 命令及其用法。参见 http://www.w3schools.com/sql/default.asp。

**类英语语法。** 当你创建 SQL 语句时，它会以语句的形式向数据库发起请求或“查询”，类似于英语祈使句的结构，例如“选择你的搭档”、“展示你的物品”或“描述那个恶霸”。SQL 语句的第一个词是一个英语动词，即被称为命令的动作词，例如 *show*、*use*、*select*、*drop* 等等。命令后面跟随一组名词性的词，例如 *show databases*、*use database* 或 *create databases*。语句中可能包含介词，例如 *in* 或 *from*。例如：

```
show tables in database
```

或者

```sql
select phones from customer_table
```

该语言还允许你添加条件子句以细化查询，例如：

```sql
select companyname from suppliers where supplierid > 20;
```

在查询中列出多个项目时，与英语一样，项目之间用逗号分隔；例如，在下面的 SQL 语句中，所选列表中的每个字段都用逗号分隔：

```sql
select companyname, phone, address from suppliers;
```

如果查询非常长且复杂，你可能希望将其输入到你喜欢编辑器中，因为一旦执行了查询，它就会丢失。通过在编辑器中保存查询，你可以将其复制并粘贴回 MySQL 浏览器或命令行中，而无需重新输入。最重要的是，请确保你的查询是合理的，并且不会给重要数据库造成破坏。MySQL 提供了一个 *test* 数据库供练习使用。

### 分号终止 SQL 语句

当在 Google 上搜索“SQL query”时，排名靠前的结果之一是一个名为 *thinkgeek.com* 的网站，该网站销售 T 恤和服装、电子产品、小工具以及家庭办公室和计算用品。其“SQL query”T 恤的广告写着：

黑色 T 恤，正面印有白色 SQL 查询 *SELECT * FROM users WHERE clue > 0*。不幸的是，随后返回了零行结果——哎呀。而且嘿！这个查询末尾没有该死的分号，因为世界上并不是每个人都使用相同的数据库和相同的控制台/外壳——并且“条条大路通罗马”（意即方法不止一种）。明白了吗？明白了。

分号是终止每个查询语句的标准方式。某些数据库系统不要求使用分号，但 MySQL 要求使用（例外是 USE 和 QUIT 命令），如果你忘记了分号，你会看到一个二级提示符，并且执行将暂停，直到你添加分号为止，如图 B.3 所示。

![](img/8556abcb353c0991f12099420ec28735_755_0.png)

```
mysql> show databases
      >
      >;

Database
mysql
northwind
phpmysqladmin
test
4 rows in set (0.0 sec)
```

**图 B.3** 缺少分号及二级提示符。

**命名约定。** 当使用良好的命名约定时，数据库及其表格更易于阅读。

例如，将表名设为复数，将字段/列名设为单数是很合理的。为什么？因为名为 *Shippers* 的表通常保存不止一个发货人，但用于描述每个发货人的字段名称是单个值，例如 *Company_Name*、*Phone* 等。表或字段名的第一个字母通常是大写的。

复合名称，例如 *Company_Name*，通常使用下划线分隔，且每个单词的首字母大写。

数据库中的任何名称都不允许使用空格和连字符。

**保留字。** 所有语言都有一组具有特殊含义的保留字列表。SQL 保留字列在表 B.1 中。本附录将使用其中大多数单词。（完整的保留字列表请参见 MySQL 文档。）

| **表 B.1** | SQL 保留字 |
|---|---|
| ALTER | JOIN |
| AND | LEFT JOIN |
| AS | LIKE |
| CREATE | LIMIT |
| CROSS JOIN | ON |
| DELETE | OR |
| DROP | ORDER BY |
| FROM | RIGHT JOIN |
| FULL JOIN | SELECT |
| GROUP BY | SET |
| INSERT | UPDATE |
| INTO | WHERE |

**大小写敏感性。** 如果你使用 UNIX，数据库和表名是区分大小写的；但如果你使用 Windows，则不区分。一种惯例是对数据库及其表始终使用小写名称。

SQL 命令不区分大小写。例如，以下 SQL 语句都是有效的：

```
show databases;
SHOW DATABASES;
```

虽然 SQL 命令不区分大小写，但根据惯例，为了提高清晰度，SQL 关键字会大写，而字段、表和数据库名称仅首字母大写。

```
SELECT * FROM Persons WHERE FirstName='John'
```

如果使用 `LIKE` 和 `NOT LIKE` 命令进行模式匹配，则在 MySQL 中，要搜索的模式是区分大小写的。

### 结果集

结果集只是另一个用于保存 SQL 查询结果的表。大多数数据库软件系统甚至允许你对结果集使用函数执行操作，例如 `Move-To-First-Record`、`Get-Record-Content`、`Move-To-Next-Record` 等。在图 B.4 中，结果集是通过要求 *mysql* 显示名为 *shippers* 的表中所有字段而创建的表。

```sql
mysql> show fields in shippers;
+-------------+-----------+------+-----+---------+----------------+
| Field       | Type      | Null | Key | Default | Extra          |
+-------------+-----------+------+-----+---------+----------------+
| ShipperID   | int(11)   |      | PRI | NULL    | auto_increment |
| CompanyName | varchar(40)|     |     |         |                |
| Phone       | varchar(24)| YES |     | NULL    |                |
+-------------+-----------+------+-----+---------+----------------+
3 rows in set (0.0 sec)
```

**图 B.4** 结果集只是由查询产生的表。

### B.1.4 SQL 与数据库

数据库服务器可以支持多个数据库。例如，Oracle 或 MySQL 数据库服务器可以为会计提供一个数据库，为人事提供一个数据库，为电子商务应用提供第三个数据库，等等。要查看可用的数据库，SQL 提供了 *show* 命令。

### show databases 命令

要查看数据库服务器上可用的数据库，请使用 *show databases* 命令。你机器上的数据库列表可能有所不同，但安装 MySQL 时会提供 *mysql* 和 *test* 数据库。*mysql* 数据库是必需的，因为它描述了用户访问权限；*test* 数据库如其名称所示，是作为测试功能如何工作的练习数据库提供的。

### 格式

```
SHOW DATABASES;
```

