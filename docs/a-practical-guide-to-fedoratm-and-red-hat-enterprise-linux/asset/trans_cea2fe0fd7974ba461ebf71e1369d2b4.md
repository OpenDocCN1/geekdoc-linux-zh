
即使可能并非必要，同时指定表和列（如下例所示）也能使代码和注释更加清晰。

### 表别名
表的别名是表的一个另一个（通常更短的）名称。别名可以使 SELECT 语句更易读。你在查询的 FROM 子句中声明表别名。例如，下面的子句声明 **p** 为表 **people** 的别名，**s** 为表 **stores** 的别名。

```
FROM people p JOIN stores s
```

有了这些别名后，你可以在查询的其余部分中将表 **people** 简称为 **p**，将表 **stores** 简称为 **s**。

下一个示例重写了一个使用别名和 JOIN 关键字的早期查询。这种语法使用关键字 JOIN 代替表（及别名）名称之间的逗号。它使用 ON 代替 WHERE。指定 **p.store** 和 **s.number** 清楚地表明，是表 **people** 中的列 **store** (**p.store**) 与表 **stores** 中的列 **number** (**s.number**) 进行连接。此查询返回的结果与前一个查询相同。

```
SELECT * FROM people p JOIN stores s ON p.store = s.number;
```

### 外连接
外*连接*可以返回公共列的值在两个表中都存在的行。你可以指定 LEFT OUTER JOIN（或简写为 LEFT JOIN）或 RIGHT OUTER JOIN（或简写为 RIGHT JOIN）。左和右分别指关键字 JOIN 左侧和右侧指定的表。

下一个示例演示了一个右外连接。外表是 **stores**，它在一个列 **number** 中具有一个值，该值在表 **people** 的 **store** 列中没有匹配项。SQL 在连接的行中（其中没有匹配项，即 **stores.number = 5**）从表 **people** 中插入 null 值到相应的列中。

```
MariaDB [maxdb]> SELECT * FROM people p RIGHT JOIN stores s ON p.store = s.number;
```

| name | hired | store | hourly | name | number | city |
|:---|:---|:---|:---|:---|:---|:---|
| topsy | 2012-11-01 | 4 | 1 | headquarters | 4 | new york |
| max | 2012-02-12 | 4 | 0 | headquarters | 4 | new york |
| zach | 2009-03-24 | 6 | 0 | west coast | 6 | san francisco |
| sam | 2008-01-28 | 6 | 1 | west coast | 6 | san francisco |
| NULL | NULL | NULL | NULL | midwest | 5 | chicago |

5 rows in set (0.00 sec)

下面的查询执行内连接，以列出每个人工作的城市。右外连接将显示没有人工作的城市。左外连接将显示未分配到任何商店的人。

```
MariaDB [maxdb]> SELECT p.name,
    ->           city
    ->     FROM   people p JOIN stores s
    ->         ON p.store = s.number;
+-------+-------------+
| name  | city        |
+-------+-------------+
| topsy | new york    |
| max   | new york    |
| zach  | san francisco |
| sam   | san francisco |
+-------+-------------+
4 rows in set (0.00 sec)
```

### 子查询
子查询是位于另一个 SELECT 语句 WHERE 子句中的 SELECT 语句。子查询返回一个或多个限制主查询的值。

在下一个示例中，子查询从表 **stores** 中返回列 **number** 的值，条件是列 **city** 的值为 **new york**。主查询返回表 **people** 中列 **name** 的值，条件是列 **store** 的值等于子查询返回的值。结果是一个返回在纽约工作的人名的查询。

```
$ cat sel4
use maxdb;

SELECT       name
             FROM   people
             WHERE store =
                   (SELECT   number
                    FROM     stores
                    WHERE    city = 'new york'
                   );

$ mysql < sel4
name
topsy
max
```

最后一个示例是一个 **bash** 脚本，它查询在本章中创建的 MariaDB 数据库。如果你没有运行前面的示例命令，它将无法工作。首先，脚本检查用户是否知道数据库密码。然后，它显示员工列表，并询问用户感兴趣的是哪位员工。它查询数据库中关于该员工的信息，并显示该员工工作的商店名称以及商店所在的城市。

```
$ cat employee_info
#!/bin/bash

# 
# Script to display employee information
# 

# Make sure user is authorized: Get database password
#
echo -n "Enter password for maxdb database: "
stty -echo
read pw
stty echo
echo

# Check for valid password
#
mysql -u max -p$pw maxdb >/dev/null 2>&1 </dev/null
if [ $? -ne 0 ]
then
  echo "Bad password."
  exit 1
fi

# Display list of employees for user to select from
#
echo "The following people are employed by the company:"
mysql -u max -p$pw --skip-column-names maxdb <<<\
"SELECT name FROM people ORDER BY name;"
echo
echo -n "Which employee would you like information about? "
read emp

# Query for store name
#
storename=$(mysql -u max -p$pw --skip-column-names maxdb <<<\
"SELECT stores.name FROM people, stores WHERE store = number AND people.name = '$emp';")

# if null then user entered bad employee name
#
if [ "$storename" = "" ]
then
  echo "Not a valid name."
  exit 1
fi

# Query for city name
#
storecity=$(mysql -u max -p$pw --skip-column-names maxdb <<<\
"SELECT city FROM people, stores WHERE store = number AND people.name = '$emp';")

# Display report
#
echo $emp works at the $storename store in $storecity

```

## 章节摘要

系统管理员经常被要求设置和运行 MariaDB 数据库。MariaDB/MySQL 是世界上最流行的开源 RDBMS（关系型数据库管理系统）。它速度极快，并被互联网上访问量最大的网站之一所使用。许多编程语言提供了对 MariaDB 的接口和绑定，包括 C、PHP、Python 和 Perl。你也可以直接从 shell 脚本调用 MariaDB，或者在命令行管道中使用它。MariaDB 是流行的 LAMP（Linux, Apache, MariaDB, PHP/Perl/Python）开源企业软件堆栈的核心组件。

## 练习

- 1. 列出两种你可以指定用户访问 MariaDB 密码的方法。

- 2. 交互式使用 MariaDB，创建一个名为 **dbsam** 的数据库，允许名为 **sam** 的用户修改并授权。将 Sam 的密码设置为 **porcupine**。名为 **root** 的 MariaDB 用户的密码为 **five22four**。

- 3. 什么是表？什么是行？什么是列？

- 4. 你会使用哪些命令在 **dbsam**（在练习 2 中创建）中设置一个名为 **shoplist** 的表，其中包含以下指定类型的列：**day** [DATE]、**store** [CHAR(20)]、**lettuce** [SMALLINT]、**soupkind** [CHAR(20)]、**soupnum** [INTEGER] 和 **miso** [VARCHAR(40)]？

- 5. 你可以在哪里找到你之前运行过的 MariaDB 命令列表？

## 高级练习

- 6. 列出两种你可以指定要操作的特定 MariaDB 数据库名称的方法。

- 7. 连接（join）的作用是什么？什么时候使用连接是有用的？

- 8. 假设你正在处理本章中描述的 **maxdb** 数据库中的 **people** 表。编写一个查询，按姓名顺序列出所有人员的姓名及其入职日期。

- 9. 假设你正在处理本章中描述的 **maxdb** 数据库中的 **people** 和 **stores** 表。编写一个查询，分别为表 **people** 和 **stores** 设置别名 **q** 和 **n**。让查询使用表 **people** 中的 **store** 列与表 **stores** 中的 **number** 列连接这两个表。从左到右，让查询显示该人员工作所在城市的名称、该人员的姓名以及该人员的入职日期。按城市名称排序输出。

