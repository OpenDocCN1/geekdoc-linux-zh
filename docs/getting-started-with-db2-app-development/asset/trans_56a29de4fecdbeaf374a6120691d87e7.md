
# 2.3.5 使用 XQuery 进行查询

这一次，XQuery 将成为主要的查询方法，在某些情况下，我们将在 XQuery 内部嵌入 SQL（使用 **db2-fn:sqlquery** 函数）。在使用 XQuery 时，我们将调用一些函数，并且还会使用 FLWOR 表达式。

## 示例 1

这是一个简单的 XQuery，用于返回客户联系数据。在示例中，**CONTACT** 是 XML 列的名称，而 **CLIENTS** 是表的名称。

```sql
xquery db2-fn:xmlcolumn('CLIENTS.CONTACT')
```

务必在任何 XQuery 表达式前加上 **xquery** 命令前缀，以便 DB2 知道必须使用 XQuery 解析器，否则 DB2 会假设你试图执行的是 SQL 表达式。**db2-fn:xmlcolumn** 函数是一个用于检索指定参数列中 XML 文档的函数。它等价于以下 SQL 语句，因为它检索的是整个列的内容：

```sql
SELECT contact FROM clients
```

## 示例 2

在*清单 2.15*中展示的示例里，我们使用 FLWOR 表达式来检索客户传真数据。

```xml
xquery
for $y in db2-fn:xmlcolumn('CLIENTS.CONTACT')/Client/fax
return $y
```

### 清单 2.15 - XQuery 和 FLWOR 表达式

第一行调用了 XQuery 解析器。第二行指示 DB2 遍历包含在 **CLIENTS.CONTACT** 列中的传真子元素。每个 fax 元素都绑定到变量 `$y`。第三行表示，对于每次迭代，返回的值都是 "$y"。

此查询的输出如*清单 2.16*所示（我们在输出中省略了命名空间，否则由于可能跨越多行，阅读难度会增加）：

```xml
<fax>4081112222</fax>
<fax>5559998888</fax>
```

### 清单 2.16 - 清单 2.15 中查询的输出

## 示例 3

*清单 2.17*中的示例查询 XML 数据并返回 HTML 格式的结果。

```xml
xquery
<ul> {
    for $y in db2-fn:xmlcolumn('CLIENTS.CONTACT')/Client/Address
    order by $y/zip
    return <li>{$y}</li>
}
</ul>
```

### 清单 2.17 - 使用 FLWOR 表达式返回 HTML 的 XQuery 语句

返回的示例 HTML 看起来像*清单 2.18*中所示的内容。

```html
<ul>
<li>
<address>
    <street>9407 Los Gatos Blvd.</street>
    <city>Los Gatos</city>
    <state>ca</state>
    <zip>95302</zip>
</address>
</li>
<li>
<address>
    <street>4209 El Camino Real</street>
    <city>Mountain View</city>
    <state>CA</state>
    <zip>95302</zip>
</address>
</li>
...
</ul>
```

### 清单 2.18 - 在清单 2.17 中执行的查询输出

## 示例 4

以下示例展示了如何使用 **db2-fn:sqlquery** 函数在 XQuery 内部嵌入 SQL。**db2-fn:sqlquery** 函数执行 SQL 查询，并仅返回选定的 XML 数据。传递给 **db2-fn:sqlquery** 的 SQL 查询必须仅返回 XML 数据。然后，此 XML 数据可以进一步由 XQuery 进行处理。这一点在*清单 2.19*中有所说明。

```xml
xquery
    for $y in
        db2-fn:sqlquery(
            'select comments from items where srp > 100')
    /Comments/Comment
    where $y/ResponseRequested='Yes'
    return (
        <action>
            {$y/ProductID}
            {$y/CustomerID}
            {$y/Message}
        </action>
    )
```

### 清单 2.19 - db2-fn:sqlquery 函数在 XQuery 中嵌入 SQL 的示例

在示例中，SQL 查询基于条件筛选行，即 **srp** 列的值大于 100。从筛选出的这些行中，它会选择 **comments** 列，即 XML 列。接下来，应用 XQuery（或 XPath）以到达子元素。

> **注意：**
> SQL 对大小写不敏感，且 DB2 软件默认将所有表和列名存储为大写。另一方面，XQuery 对大小写敏感。上述函数是 XQuery 接口函数，因此应将这些函数中的表和列名以大写字母形式传递。如果以小写形式传递对象名称，可能会导致未定义对象名称错误。

## 2.3.6 使用 SQL/XML 进行连接

本节描述如何在不同表的两个 XML 列之间，或在一个 XML 列和一个关系列之间执行 JOIN 操作。假设你已经使用*清单 2.20*中显示的语句创建了两个表：

```sql
CREATE TABLE dept (unitID CHAR(8), deptdoc XML)
CREATE TABLE unit (unitID CHAR(8) primary key not null,
                     name CHAR(20),
                     manager VARCHAR(20),
                     ...)
```

### 清单 2.20 - 用于 JOIN 示例的表 DDL

你可以通过两种方式之一执行 JOIN 操作。第一种方法如*清单 2.21*所示。

```sql
SELECT u.unitID
   FROM dept d, unit u
  WHERE XMLEXISTS (
         '$e//employee[name = $m]'
   passing d.deptdoc as "e", u.manager as "m")
```

### 清单 2.21 - 使用 SQL/XML 执行 JOIN 的第一种方法

上述清单语句的第 4 行表明，JOIN 操作发生在元素 **name**（它是表 **dept** 中 **deptdoc** XML 列的子元素）和表 **unit** 中的关系列 **manager** 之间。

清单 2.22 展示了执行 JOIN 的第二种方法。

```sql
SELECT u.unitID
FROM dept d, unit u
    WHERE u.manager = XMLCAST(
            XMLQUERY('$e//employee/name'
                passing d.deptdoc as "e")
                AS char(20))
```

### 清单 2.22 - 使用 SQL/XML 执行 JOIN 的第二种方法

在这种第二种方法中，关系列位于等式的左侧。如果关系列位于等式的左侧，则可以使用关系索引而不是 XML 索引。

## 2.3.7 使用 XQuery 进行连接

假设已经创建了以下表：

```sql
CREATE TABLE dept(unitID CHAR(8), deptdoc XML)
CREATE TABLE project(projectDoc XML)
```

如果我们使用 SQL/XML，JOIN 看起来如清单 2.23 所示。

```sql
SELECT XMLQUERY (
    '$d/dept/employee'
    passing d.deptdoc as "d")
    FROM dept d, project p
    WHERE XMLEXISTS (
        '$e/dept[@deptID=$p/project/deptID]'
        passing d.deptdoc as "e", p.projectDoc as "p")
```

### 清单 2.23 - 使用 SQL/XML 进行 JOIN

使用 XQuery 的等效 JOIN 如清单 2.24 所示。

```xml
xquery
    for $dept in db2-fn:xmlcolumn("DEPT.DEPTDOC")/dept
    for $proj in db2-fn:xmlcolumn("PROJECT.PROJECTDOC")/project
    where $dept/@deptID = $proj/deptID
    return $dept/employee
```

### 清单 2.24 - 使用 XQuery 进行 JOIN

第二种方法更易于解释 —— 变量 $dept 保存表 dept 中 XML 列 deptdoc 的 XML 文档。变量 $proj 保存表 project 中 XML 列 projectdoc 的 XML 文档。然后，第 4 行在第一个 XML 文档的一个属性和第二个 XML 文档的一个元素之间执行 JOIN 操作。

## 2.3.8 更新和删除操作

对 XML 数据的更新和删除操作可以通过以下两种方式进行：

- 使用 SQL UPDATE 和 DELETE 语句
- 使用 TRANSFORM 表达式

对于使用 SQL UPDATE 和 DELETE 语句的第一种方式，更新或删除发生在文档级别：也就是说，整个 XML 文档会被更新后的文档替换。例如，在下面清单 2.25 中的 UPDATE 语句中，如果你只想更改 `<state>` 元素，实际上整个 XML 文档都会被替换。

```sql
UPDATE clients SET contact=(
        xmlparse(document
        '<Client>'
            '<address>'
            '<street>5401 Julio ave.</street>'
            '<city>San Jose</city>'
            '<state>CA</state>'
            '<zip>95116</zip>'
            '</address>'
            '<phone>'
            '<work>4084633000</work>'
            '<home>4081111111</home>'
            '<cell>4082222222</cell>'
            '</phone>'
            '<fax>4087776666</fax>'
            '<email>newemail@someplace.com</email>'
        '</Client>')
    )
    WHERE id = 3227
```

### 清单 2.25 - SQL UPDATE 的示例

对于第二种方式，你可以使用 TRANSFORM 表达式执行子文档更新，这要高效得多。这允许你替换、插入、删除或重命名 XML 文档中的节点。你也可以在不替换节点本身的情况下更改节点的值，通常是为了更改元素或属性值——这是一种非常常见的更新类型。此支持功能在 DB2 9.5 中添加。

TRANSFORM 表达式是 XQuery 语言的一部分；你可以在通常使用 XQuery 的任何地方使用它，例如在 FLWOR 表达式中或在 SQL/XML 语句中的 XMLQUERY 函数中。最典型的用法是在 SQL UPDATE 语句中修改 XML 列中的 XML 文档。

清单 2.26 展示了 TRANSFORM 表达式的语法。

```text
>>-transform--| copy clause |--| modify clause |--| return clause -->
```
