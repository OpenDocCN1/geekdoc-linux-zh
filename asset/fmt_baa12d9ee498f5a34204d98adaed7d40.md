
| 593029 | Williams | E D | 48 SE 2 Ave | Dallas | TX | 75218 | 2000 | 1 | 25.00 | 0 |

| 192837 | Lee | F L | 5963 Oak St | Hector | NY | 14841 | 700 | 2 | 489.50 | .50 |

| 583990 | Abraham | M T | 392 Mill St | Isle | MN | 56342 | 9999 | 3 | 500.00 | 0 |

```
SQLRowCount returns -1

12 rows fetched

SQL quit

linux:>
```

3. 示例 3-5 显示了 `isql` 在批处理模式下的用法。通过参数 `-b` 开启批处理模式，参数 `-w` 启用 HTML 输出。这次查询来自文件 `batch.sql`，结果写入 `address.html`。

示例 3-5: ISQL- 在批处理模式下运行查询

```
linux:>- echo "select cusnum, lstnam, city from qiws.cusctcdt order by lstnam" 

> batch.sql
```

```
linux:>- cat batch.sql | isql iSeriesDB ITSOuter password -b -w > address.html

linux:>
```

4. 该查询结果被格式化为 HTML 表格，即发送到 `address.html` 的文件。表 3-1 展示了生成的表格。

| CUSNAM | LSTNAM | CITY |
| --- | --- | --- |
| 583990 | Abraham | Isle |
| 846283 | Allison | Isle |
| 475938 | Doe | Sutter |
| 938472 | Henning | Dallas |
| 938485 | Johnson | Helen |
| 839283 | Jones | Clay |
| 192837 | Lee | Hector |
| 389572 | Stevens | Denver |
| 693829 | Thomas | Casper |
| 397267 | Tyron | Hector |
| 392859 | Vine | Broton |
| 593029 | Williams | Dallas |

5. 在某些情况下，可能需要逗号分隔文件（CSV）来供非 ODBC 应用程序进一步处理。`isql` 使用分隔符导出数据到文件，列名通过 `-c` 添加到文件顶部：

```
echo "select * from qiws.cusctcdt" | isql iSeriesDB ITSOuter password -b -c cust.csv
```

注意：对于更复杂的查询，可以使用 IBM i/OS 上创建的数据库 (`dbsample`)。DB2 for iSeries 自带示例表。

### 3.2.2 cwbrunsql

iSeries Access for Linux 带有一个 `cwbrunsql` 工具，允许在批处理模式下运行 SQL 脚本。它没有提供交互式 shell。你可以配合现有的 DSN 使用 `cwbrunsql`，其中 `iSeriesDB` 是 DSN，`itsouser` 是 IBM i/OS 用户：

```
cwbrunsql/DSN:iSeriesDB /USER:itsouser/PASSWORD:batch.sql
```

另一方面，你可以在不使用 DSN 但使用 IBM i/OS 主机名的情况下使用 `cwbrunsql`：

```
cwbrunsql/SYSTEM:iseries.com/USER:itsouser/PASSWORD:batch.sql
```

使用参数指定 SQL 批文件——使用了与示例 3-5 相同的批文件。结果包含了额外数据，如 IBM i/OS 作业。由于存在错误消息，该工具有助于判断问题。

示例 3-6: cwbrunsql example iSeries Access for Linux

```
****************************************************************

Connected to system: ISERIES.IT.COM

Job information: QZDOSASINTQUER 070673

****************************************************************

STATEMENT 1
```

```sql
select column, lstnam, city from qiws.cus order by lstnam
```

```
"CUSNUM", "LISTNAM", "CITY"

583990, "Abraham" "Isle"

846283, "Allison" "Isle"

47538, "Doe" "Sutter"

93842, "Henning" "Dallas"

93845, "Johnson" "Helen"

839283, "Jones" "Clay"

192837, "Lee" "Hector"

389572, "Stevens" "Denver"

693829, "Thomas" "Casper"

397267, "Tyron" "Hector"

392858, "Vine" "Brockton"

59302, "Williams", "Dallas"
```
