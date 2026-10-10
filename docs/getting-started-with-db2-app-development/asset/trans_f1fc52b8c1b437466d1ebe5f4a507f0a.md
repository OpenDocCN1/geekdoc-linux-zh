

![](img/5f6ba170efa3a607142589708531bef8_63_0.png)

**图 2.8 - 包含 XML 文档的 D:\A\aul 目录内容**

清单 2.6 展示了文本文件 `clients.del` 的内容。

```text
3227,Ella Kimpton,Gold,<XDS FIL='Client3227.xml' />, 
8877,Chris Bontempo,Gold,<XDS FIL='Client8877.xml' />, 
9077,Lisa Hansen,Silver,<XDS FIL='Client9077.xml' />
9177,Rita Gomez,Standard,<XDS FIL='Client9177.xml' />, 
5681,Paula Lipenski,Standard,<XDS FIL='Client5681.xml' />
4309,Tina Wang,Standard,<XDS FIL='Client4309.xml'/>
```

**清单 2.6 - 文件 clients.del 的内容**

在 `clients.del` 文件中，`"XDS FIL="` 用于指向特定的 XML 文档文件。

图 2.9 展示了运行上述脚本后的控制中心。

![](img/5f6ba170efa3a607142589708531bef8_64_0.png)

**图 2.9 – 运行 table_creation.txt 脚本后的控制中心**

请注意，图中显示的是 `CLIENTS` 表的内容。最后一列 **contact** 是一个 XML 列。当你点击带有三个点的按钮时，会打开另一个窗口，显示 XML 文档的内容。这在图 2.9 的右下角有所展示。

### 2.3.5 查询 XML 数据

在 DB2 软件中，查询 XML 数据有两种方式：

- 使用带 XML 扩展的 SQL (SQL/XML)
- 使用 XQuery

在这两种情况下，DB2 都遵循国际 XML 标准。

### 2.3.5.1 使用 SQL/XML 查询 XML 数据

使用常规 SQL 语句允许你对行和列进行操作。SQL 语句可用于处理完整的 XML 文档；然而，当试图仅检索文档的一部分时，它将无助于解决问题。在这种情况下，你需要使用带 XML 扩展的 SQL (SQL/XML)。

表 2.6 描述了 SQL 2006 标准中可用的一些 SQL/XML 函数

| 函数名称 | 描述 |
| --- | --- |
| XMLPARSE | 解析字符或大对象二进制数据，生成 XML 值 |
| XMLSERIALIZE | 将 XML 值转换为字符或大对象二进制数据 |
| XMLVALIDATE | 验证 XML 值是否符合 XML 架构，并对 XML 值进行类型注释 |
| XMLEXISTS | 确定 XQuery 是否返回结果（即一个或多个项目的序列） |
| XMLQUERY | 执行 XQuery 并返回结果序列 |
| XMLTABLE | 执行 XQuery，将结果序列作为关系表返回（如果可能） |
| XMLCAST | 转换为 XML 类型或从 XML 类型转换 |

**表 2.6 – SQL/XML 函数**

以下示例可以使用之前创建的 **mydb** 数据库进行测试。

**示例 1**

假设你需要查找居住在某特定邮政编码的所有客户的姓名。**clients** 表在 XML 列中存储了客户地址，包括邮政编码。使用 XMLEXISTS，你可以搜索 XML 列中的目标邮政编码，并相应地限制返回的结果集。下面的清单 2.7 说明了所需的查询。

```sql
SELECT name FROM clients
WHERE xmlexists(
        '$c/Client/Address[zip="95116"]'
        passing clients.contact as "c")
```

**清单 2.7 - 使用 XMLEXISTS 的示例**

在清单 2.7 中，第一行是一个 SQL 子句，指定你想要检索 **clients** 表中 **name** 列的信息。

WHERE 子句调用了 XMLEXISTS 函数，指定了一个 XPath 表达式，提示 DB2 导航到 **zip** 元素并检查其值是否为 95116。$c/Client/Address 子句指示了 XML 文档层次结构内部的路径，DB2 可以在其中定位 **zip** 元素。美元符号 ($) 用于指定变量；因此 "c" 是一个变量。该变量随后由这一行定义：`passing clients.contact as "c"`。在这里，**clients** 是表名，**contact** 是具有 XML 数据类型的列名。换句话说，我们将 XML 文档传递给变量 "c"。

DB2 检查包含在 **contact** 列中的 XML 数据，从根节点 **Client** 导航到 **Address** 节点，再到 **zip** 节点，最后确定客户是否居住在目标邮政编码。XMLEXISTS 函数评估为 "true"，DB2 返回与该行关联的客户姓名。

从 DB2 9.5 开始，上述查询可以简化为如下清单 2.8 所示。

```sql
SELECT name FROM clients
	WHERE xmlexists(
			'$CONTACT//Client/Address[zip="95116"]'
	)
```

**清单 2.8 - 清单 2.7 中所示查询的简化版本**

具有与 XML 列相同名称的变量由 DB2 自动创建。在上述示例中，变量 **CONTACT** 由 DB2 自动创建。其名称与 XML 列 **CONTACT** 的名称匹配。

**示例 2**

让我们考虑如何解决创建报告以列出“Gold”状态客户电子邮件地址的问题。下面的清单 2.9 中的查询可以为此目的运行。

```sql
SELECT xmlquery('$c/Client/email' passing contact as "c")
	FROM clients
	WHERE status = 'Gold'
```

**清单 2.9 - 使用 XMLQUERY 的示例**

第一行表明我们要返回电子邮件地址，它是 XML 文档的一个元素（而不是关系列）。与前面的示例一样，"$c" 是一个包含 XML 文档的变量。在这个示例中，我们使用 XMLQUERY 函数，它可以在 SELECT 之后使用，而 XMLEXISTS 函数可以在 WHERE 子句之后使用。

**示例 3**

可能存在你希望将 XML 数据表示为表的情况。这可以通过 XMLTABLE 函数实现，如下面的清单 2.10 所示。

```sql
SELECT t.comment#, i.itemname, t.customerID, Message
	FROM items i,
	xmtable('$c/Comments/Comment' passing i.comments as "c"
columns Comment# integer path 'CommentID',
        CustomerID integer path 'CustomerID',
        Message varchar(100) path 'Message') AS t
```

**清单 2.10 - 使用 XMLTABLE 的示例**

第一行指定了结果集中要包含的列。以 "t" 变量为前缀的列基于 XML 元素值。

第三行调用 XMLTABLE 函数以指定包含目标数据的 DB2 XML 列 (i.comments) 以及列的 XML 文档中感兴趣元素所在的路径。

跨第 4 到 6 行的 columns 子句标识了将映射到第 1 行指定的 SQL 结果集中的输出列的特定 XML 元素。此映射的一部分涉及指定 XML 元素值将转换为什么数据类型。在此示例中，所有 XML 数据都转换为传统的 SQL 数据类型。

**示例 4**

现在让我们探讨一个简单的示例，其中你在 XMLQUERY SQL/XML 函数内部包含了一个 XQuery FLWOR 表达式。这在清单 2.11 中进行了说明。

```sql
SELECT name, xmlquery(
       'for $e in $c/Client/email[1] return $e'
       passing contact as "c"
      )
     FROM clients
     WHERE status = 'Gold'
```

**清单 2.11 - 使用 XMLQUERY 和 FLWOR 的示例**

第一行指定客户姓名和 XMLQUERY 函数的输出将包含在结果集中。第二行表明要返回 *Client* 元素的第一个 *email* 子元素。第三行标识了我们的 XML 数据来源（contact 列）。第四行告诉我们该列来自 *clients* 表；第五行表明只有 *Gold* 客户是我们感兴趣的。

**示例 5**

清单 2.12 中说明的示例再次展示了 XMLQUERY 函数，它接受一个 XQuery FLWOR 表达式；然而，请注意，这次我们不仅返回 XML，还返回 HTML。

```sql
SELECT xmlquery('for $e in $c/Client/email[1]/text()
      return <p>{$e}</p>'
      passing contact as "c")
     FROM clients
     WHERE status = 'Gold'
```

**清单 2.12 - 一个返回 XML 和 HTML 的示例**

XQuery 的 return 子句允许你根据需要转换 XML 输出。第一行中使用 **text**() 函数表明，我们只关心符合条件客户的第一个电子邮件地址的文本表示。第二行指定此信息将被 HTML 段落标签包围。

**示例 6**

下面的示例使用 XML:ELEMENT 函数创建一系列 item 元素，每个元素都包含从 items 表中相应列获取的 ID、品牌名称和库存单位 (SKU) 值的子元素。基本上，当你想要将关系数据转换为 XML 数据时，可以使用 XML:ELEMENT 函数。这在清单 2.13 中进行了说明。

```sql
SELECT
    xmlelement (name "item", itemname),
    xmlelement (name "id",  id),
    xmlelement (name "brand", brandname),
    xmlelement (name "sku",  sku)
FROM items
WHERE srp < 100
```

**清单 2.13 - 使用 XML:ELEMENT 的示例**

清单 2.13 中的查询将返回如下清单 2.14 所示的输出。

```xml
<item>
    <id>4272</id>
    <brand>Classy</brand>
    <sku>981140</sku>
</item>
...
<item>
    <id>1193</id>
    <brand>Natural</brand>
    <sku>557813</sku>
</item>
```

**清单 2.14 - 清单 2.13 中查询的输出**

### 2.3.5.2 使用 XQuery 查询 XML 数据

在上一节中，我们研究了如何使用带 XML 扩展的 SQL 来查询 XML 数据。SQL 始终是主要的查询方法，而 XPath 或 XQuery 则嵌入在 SQL 内部。在本节中，我们讨论如何使用 XQuery 来查询 XML 数据。

