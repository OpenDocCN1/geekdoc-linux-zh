
| TR01 | DB2 Fundamentals | 1 |

| TX01 | DB2 Administration | 2 |

| TX01 | DB2 Application Development | 2 |

| TX01 | DB2 Fundamentals | 2 |

选中了 7 条记录。

**7–28** 结果 `GROUPING SETS` 规范通过列出 `TEST_taken` 表的 `TCID` 列来计算第一个需求，即每个测试中心参加的测试次数。然后，通过列出 `TEST_TABLE` 表的 `TCID` 列和 `TEST` 表的 `name` 列计算第二个需求，即按测试中心和名称的测试次数。这种第二次分组与使用 `GROUP BY TT.TCID,T.NAME` 编写的标准分组相同。

如图 7–28 所示的结果集，分组集可以由一个或多个列形成。

# 添加总计

使用 `GROUPING SETS` 规范，你可以为查询添加总计。图 7–27 所示的示例没有显示所有测试中心参加的测试总数。这可以通过向集合列表添加总计组来计算。

随着组的创建，在特定组中没有值的列将添加 `null` 值。这样一来，总计行除总计本身外，所有列都将显示 `null` 值。

让我们下一个示例。一个与图 7–27 所示的示例类似。这次我们包含一个总计组，并将空生成的

DB2 提供了 `GROUPING` 函数，通过赋予它们一个值来识别那些由空生成的值。

## OLAP 特性

注意：`GROUPING` 函数返回 1 或 0。值 1 表示该值是生成的，值 0 表示不是。

让我们看下一个示例。一个与图 7–27 所示的示例类似。这次我们包含一个总计组，并将空生成的

```sql
SELECT 
  CASE WHEN GROUPING(tt.tcid)=1 THEN 'ALL' ELSE tt.tcid END AS TCID,
  CASE WHEN GROUPING(t.name)=1 THEN 'ALL' ELSE t.name END AS NAME,
  count(*)
FROM db2cert.test_taken tt, db2cert.test t
WHERE tt.number=t.number
GROUP BY GROUPING SETS (tt.tcid,t.name)
```

图 7–31 使用分组函数识别空

| TCID | NAME | COUNT |

|---|---|---|

| ALL | ALL | 9 |

| TR01 | | 3 |

| TX01 | | 6 |

| TR01 | DB2 Application Development | 2 |

| TR01 | DB2 Fundamentals | 1 |

| TX01 | DB2 Administration | 2 |

| TX01 | DB2 Application Development | 2 |

| TX01 | DB2 Fundamentals | 2 |

选中了 8 条记录。

**7–32** 分组函数的结果

# 第 7 章 高级 SQL

`GROUPING` 函数通过赋予一个值来识别那些空生成的值。值 1 表示该值是生成的，值 0 表示不是。

让我们看下一个示例。一个与图 7–27 所示的示例类似。这次我们包含一个总计组，并将空生成的

# ROLLUP

`GROUP BY` 子句中的 `GROUPING SETS` 规范用于在单个 SQL 语句中生成多个聚合组。该功能用于根据不同的分组标准生成聚合数据。使用 `GROUPING SETS`，可以计算出原本需要集合操作（如 `UNION`）来合并不同结果集的聚合值。

假设你需要一份显示以下内容的报告：

- 每个国家参加了多少次测试？
- 每个国家每个测试中心参加了多少次测试？
- 每个国家、测试中心和测试名称参加了多少次测试？
- 测试总数是多少？

为了解决这个需求，我们将使用 `ROLLUP` 分组，它将生成请求的聚合。SQL 语句如图 7–33 所示。

```sql
SELECT
  country,
  tt.tcid,
  substr(t.name,1,27) as test_name,
  count(*) as tests_taken
FROM db2cert.test_taken tt,db2cert.test t,db2cert.candidate c
WHERE tt.number=t.number AND tt.tcid=c.cid
GROUP BY ROLLUP (c.country,tt.tcid,t.name)
ORDER BY c.country,tt.tcid,t.name
```

图 7–33 使用 `ROLLUP` 运算符

生成的报告允许你向上汇总信息并深入分析信息。你可以从总计级别到国家、测试中心和测试名称对报告进行分析。

## OLAP 特性

| 国家 | TCID | 考试名称 | 参加次数 |

| --- | --- | --- | --- |

| 加拿 | TX01 DB2 | 管理 | 2 |

| 加拿 | TX01 DB2 | 应用开发 | 2 |

| 加拿 | TX01 DB2 | 基础 | 6 |

| 加拿 | TX01 - | | 6 |

| 德国 | TR01 DB2 | 应用开发 | 2 |

| 德国 | TR01 DB2 | 基础 | 1 |

| 德国 | TR01 - | | 3 |

| 德国 | - | - | 9 |

选中了 10 条记录。

**图 7–34 ROLLUP 算子的结果**

> `ROLLUP` 操作不是交换的；你指定分组的顺序非常重要。`ROLLUP(COUNTRY, TCID, NAME)` 产生的集合与 `ROLLUP(TCID, COUNTRY, NAME)` 不同。

像 `ROLLUP` 这样的超级操作是基于 `GROUPING SET` 操作构建的。图 7-33 所示的 `ROLLUP` 等同于 `GROUPING SET ((COUNTRY, TCID, NAME), (COUNTRY, TCID), COUNTRY, ())`。这就是为什么它们被视为超级分组操作。

# CUBE

从图 7–33 所示的 `ROLLUP` 操作获得的答案中，还有一些未出现但很有用的分组。这些分组包括仅按测试中心参加的考试次数，或仅按考试编号参加的考试次数。

`CUBE` 操作可以获取分组列表中可以形成的所有分组组合。`CUBE` 操作分组列表中列出的分组将进行排列，以计算该列表中所有可能的分组。这创建了构建数据立方体所需的所有聚合。

生成的立方体可以在多个维度上进行切片和分析（sliced and diced），允许用户对 DB2 中存储的数据进行多维分析。

现在使用 `CUBE` 操作生成以下分组：

- 按国家参加的考试
- 按测试中心参加的考试
- 按考试编号参加的考试
- 所有中间分组

你可以编写一个如图 7–35 所示的语句。

```sql
SELECT c.country,tt.tcid,
SUBSTR(t.name,1,27) AS test_name,
COUNT(*) AS tests_taken
FROM db2cert.test_taken tt,
db2cert.test t,
db2cert.candidate c
WHERE tt.number=t.number
AND tt.cid=c.cid
GROUP BY
CUBE (c.country,tt.tcid,t.name)
ORDER BY c.country,tt.tcid,t.name
```

图 7–35 使用 `CUBE` 算子

| 国家 | TCID | 考试名称 | 参加次数 |

|---|---|---|--| 

| 加拿 | TX01 | DB2 | 管理 | 2 |

| 加拿 | TX01 | DB2 | 应用开发 | 2 |

| 加拿 | TX01 | DB2 | 基础 | 6 |

| 加拿 | | DB2 | 管理 | 2 |

| 加拿 | | DB2 | 应用开发 | 2 |

| 加拿 | | DB2 | 基础 | 6 |

| 德国 | TR01 | DB2 | 应用开发 | 2 |

| 德国 | TR01 | DB2 | 基础 | 1 |

| 德国 | | DB2 | 管理 | 3 |

| 德国 | | DB2 | 应用开发 | 1 |

| 德国 | | DB2 | 基础 | 3 |

| 德国 | TR01 | DB2 | 应用开发 | 2 |

| 德国 | TR01 | DB2 | 基础 | 3 |

| 德国 | | DB2 | 管理 | 2 |

| 德国 | | DB2 | 应用开发 | 6 |

| 德国 | | DB2 | 基础 | 4 |

| TX01 | | DB2 | 管理 | 2 |

| TX01 | | DB2 | 应用开发 | 4 |

| TX01 | | DB2 | 基础 | 9 |

选中了 25 条记录。

图 7–36 `CUBE` 算子的结果

| 国家 | TCID | 考试名称 | 参加次数 |

|---|---|---|--|
