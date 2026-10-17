
## CUBE 算子示例

| TX01 | | DB2 | 应用开发 | 4 |
| TX01 | | DB2 | 基础 | 9 |

选中了 25 条记录。

图 7–36 CUBE 算子的结果

`CUBE` 操作产生的结果中包含一些未出现但很有用的分组。这些分组包括仅按测试中心参加的考试次数，或仅按考试编号参加的考试次数。

`CUBE` 操作可以获取分组列表中可以形成的所有分组组合。`CUBE` 操作分组列表中列出的分组将进行排列，以计算该列表中所有可能的分组。这创建了构建数据立方体所需的所有聚合。

生成的立方体可以在多个维度上进行切片和分析，允许用户对 `DB2` 中存储的数据进行多维分析。

现在使用 `CUBE` 操作生成以下分组：

- 按国家参加的考试
- 按测试中心参加的考试
- 按考试编号参加的考试
- 所有中间分组

你可以编写一个如图 7–35 所示的语句。

```
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

图 7–35 使用 CUBE 算子

| 国家 | TCID | 考试名称 | 参加次数 |
|---|---|---|---|
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

图 7–36 CUBE 算子的结果
