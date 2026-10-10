
### 2.3.2 XPath 基础

XPath 是一种可用于查询 XML 文档的语言。清单 2.1 展示了一个 XML 文档，而图 2.7 则以解析分层（也称为“节点”或“叶子”）格式展示了同一文档。我们将使用解析分层格式来解释 XPath 的工作原理。

```xml
<dept bldg="101">
   <employee id="901">
      <name>John Doe</name>
      <phone>408 555 1212</phone>
      <office>344</office>
   </employee>
   <employee id="902">
      <name>Peter Pan</name>
      <phone>408 555 9918</phone>
      <office>216</office>
   </employee>
</dept>
```

清单 2.1 – 一个 XML 文档

![](img/5f6ba170efa3a607142589708531bef8_57_0.png)

图 2.7 – 清单 2.1 中 XML 文档的解析分层表示

快速学习 XPath 的方法是将其与 MS-DOS 或 Linux/UNIX 中的 `change directory`（`cd`）命令进行比较。使用 `cd` 命令时，你按如下方式遍历目录树：

```bash
cd /directory1/directory2/...
```

同样，在 XPath 中，你使用斜杠在 XML 文档内部从一个元素移动到另一个元素。例如，使用 *清单 2.1* 中的文档，在 XPath 中可以使用此查询检索所有员工的姓名：

```xpath
/dept/employee/name
```

#### 2.3.2.1 XPath 表达式

XPath 表达式使用完全限定路径来指定元素和属性。“@”符号用于指定属性。若要检索元素的值（文本节点），请使用 `text()` 函数。*表 2.2* 展示了使用 *清单 2.1* 中 XML 文档的 XPath 查询及其相应结果。

| XPath | 结果 |
| :--- | :--- |
| `/dept/@bldg` | 101 |
| `/dept/employee/@id` | 901<br>902 |
| `/dept/employee/name` | `<name>John Doe</name>`<br>`<name>Peter Pan</name>` |
| `/dept/employee/name/text()` | John Doe<br>Peter Pan |

表 2.2 – XPath 表达式示例

#### 2.3.2.2 XPath 通配符

XPath 中有两个主要的通配符：

- `*` 匹配任何标签名
- `/` 是“后代或自身”通配符

*表 2.3* 提供了使用 *清单 2.1* 中 XML 文档的更多示例

| XPath | 结果 |
| :--- | :--- |
| `/dept/employee/*/text()` | John Doe<br>408 555 1212<br>344<br>Peter Pan<br>408 555 9918<br>216 |
| `/dept/*/ @id` | 901<br>902 |
| `//name/text()` | Peter Pan<br>John Doe |
| `/dept//phone` | `<phone>408 555 1212</phone>`<br>`<phone>408 555 9918</phone>` |

表 2.3 – XPath 通配符示例

#### 2.3.2.3 XPath 谓词

谓词包含在方括号 [ ] 中。打个比方，你可以将它们视为 SQL 中 WHERE 子句的等效物。例如 `[@id="902"]` 可以读作：“WHERE 属性 id 等于 902”。一个 XPath 表达式中可以包含多个谓词。要指定位置谓词，请使用 [n]，这意味着将选择第 n 个子元素。例如，`employee[2]` 表示应选择第二个员工。*表 2.4* 提供了更多示例。

| XPath | 结果 |
| :--- | :--- |
| `/dept/employee[@id="902"]/name` | `<name>Peter Pan</name>` |
| `/dept[@bldg="101"]/employee[office>"300"]/name` | `<name>John Doe</name>` |
| `//employee[office="344" or office="216"]/@id` | 901<br>902 |
| `/dept/employee[2]/@id` | 902 |

表 2.4 – XQuery 谓词示例

#### 2.3.2.4 父轴

类似于 MS-DOS 或 Linux/UNIX，你可以使用“.”（点）在表达式中表示你正在引用当前上下文，并使用“….”（双点）引用父上下文。*表 2.5* 提供了更多示例。

| XQuery | 结果 |
| :--- | :--- |
| `/dept/employee/name[.. /@id="902"]` | `<name>Peter Pan</name>` |
| `/dept/employee/office[. >"300"]` | `<office>344</office>` |
| `/dept/employee[office > "300"]/office` | `<office>344</office>` |
| `/dept/employee[name=. "John Doe"]/.. /@bldg` | 101 |
| `/dept/employee[name[.= "John Doe"]/.. /.. /@bldg` | 101 |

表 2.5 – XQuery 父轴

### 2.3.3 XQuery 基础

XQuery 是为 XML 创建的查询语言。XQuery 支持路径表达式以导航 XML 层次结构。事实上，XQuery 是 XPath 的超集；因此，我们之前关于 XPath 所学的一切也适用于 XQuery。XQuery 支持类型化和非类型化数据。由于 XML 文档省略缺失或未知数据，XQuery 缺少空值。XQuery 和 XQuery 表达式对大小写敏感，并且 XQuery 返回 XML 数据序列。

XQuery 支持 FLWOR 表达式。如果我们以 SQL 做类比，它等效于 SELECT-FROM-WHERE 表达式。下一节将更详细地描述 FLWOR。

#### 2.3.3.1 XQuery: FLWOR 表达式

FLWOR 代表：

- **FOR**：遍历序列，将变量绑定到项目
- **LET**：将变量绑定到序列
- **WHERE**：消除迭代中的项目
- **ORDER**：重新排列迭代中的项目
- **RETURN**：构建查询结果

它是一个允许操纵 XML 文档的表达式，使你能够返回另一个表达式。例如，假设你有一个具有此定义的表：

```sql
CREATE TABLE dept (deptID CHAR(8), deptdoc XML);
```

并且清单 2.2 中的 XML 文档被插入到 deptdoc 列中：

```xml
<dept bldg="101">
    <employee id="901">
        <name>John Doe</name>
        <phone>408 555 1212</phone>
        <office>344</office>
    </employee>
    <employee id="902">
        <name>Peter Pan</name>
        <phone>408 555 9918</phone>
        <office>216</office>
    </employee>
</dept>
```

清单 2.2 - 一个示例 XML 文档

然后，可以使用 FLWOR 表达式运行清单 2.3 中的 XQuery 语句：

```xquery
xquery
for $d in db2-fn:xmlcolumn('dept.deptdoc')/dept
let $emp := $d/employee/name
where $d/@bldg > 95
order by $d/@bldg
return
    <EmpList>
    {$d/@bldg, $emp}
    </EmpList>
```

清单 2.3 - 使用 FLWOR 表达式的示例 XQuery 语句

这将返回清单 2.4 中显示的输出：

```xml
<EmpList bldg="101">
    <name>
        John Doe
    </name>
    <name>
        Peter Pan
    </name>
</EmpList>
```

清单 2.4 - 运行清单 2.3 中的 XQuery 语句后的输出

### 2.3.4 插入 XML 文档

向 DB2 数据库中插入 XML 文档可以使用 SQL INSERT 语句或 IMPORT 实用程序执行。XQuery 不能用于此目的，因为标准中尚未定义。

让我们检查一下清单 2.5 下方显示的脚本 `table_creation.txt`，可以使用以下语句从 DB2 命令窗口或 Linux shell 中运行：

```bash
db2 -tvf table_creation.txt
```

```sql
-- (1)
drop database mydb
;

-- (2)
create database mydb using codeset UTF-8 territory US
;

-- (3)
connect to mydb
;

-- (4)
create table items (
       id         int primary key not null,
       brandname  varchar(30),
       itemname   varchar(30),
       sku        int,
       srp        decimal(7,2),
       comments   xml
);

-- (5)
create table clients(
       id         int primary key not null,
       name       varchar(50),
       status     varchar(10),
       contact    xml
);

-- (6)
insert into clients values (77, 'John Smith', 'Gold',
      '<addr>111 Main St., Dallas, TX, 00112</addr>')
;

-- (7)
IMPORT FROM "D:\Raul\clients.del" of del xml from "D:\Raul" INSERT INTO
CLIENTS (ID, NAME, STATUS, CONTACT)
;

-- (8)
IMPORT FROM "D:\Raul\items.del" of del xml from "D:\Raul" INSERT INTO
ITEMS (ID, BRANDNAME, ITEMNAME, SKU, SRP, COMMENTS)
;
```

清单 2.5 - 文件 table_creation.txt 的内容

请注意，此脚本文件和相关文件提供在本书随附的压缩文件 **Exercise_Files_DB2_Application_Development.zip** 中。随着我们描述清单 2.5 中脚本的每一行，请跟随阅读。

1.  删除数据库 **mydb**。这通常在脚本文件中执行以进行清理。如果 **mydb** 之前不存在，你将收到错误消息，但这没关系。
2.  使用代码集 UTF-8 创建数据库 **mydb**。这会创建一个 Unicode 数据库。pureXML 在 Unicode 和非 Unicode 数据库中均受支持。
3.  连接到新创建的数据库 **mydb**。这是创建数据库内部对象所必需的。
4.  创建表 **items**。注意，该表的最后一列（列 **comments**）使用新的 XML 数据类型定义为 XML 列。
5.  我们创建表 **clients**。注意，该表的最后一列（列 **contact**）也使用新的 XML 数据类型定义。
6.  使用此 SQL INSERT 语句，你可以将 XML 文档插入 XML 列。在 INSERT 语句中，你传递作为用单引号括起来的字符串的 XML 文档。
7.  使用 IMPORT 命令，你可以将多个 XML 文档连同关系数据一起插入或导入到数据库中。在 (7) 中，你正在从 *clients.del* 文件（分隔的 ascii 文件）导入数据，并且你还指示该 *clients.del* 文件引用的 XML 数据所在的位置（在此示例中，位于 D:\Raul）。

我们将更仔细地查看文件 *clients.del*，但首先，让我们看看目录 D:\Raul 的内容。*图 2.8* 提供了这些信息。

