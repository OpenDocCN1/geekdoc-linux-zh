
| `-g` | 指定是否按块或按语句报告计时。ON 表示对整个块拍摄快照，且仅在摘要表中报告块计时。OFF 表示对块中执行的每个语句拍摄快照并报告摘要表计时。| |

| `-iso` | 指定隔离级别，该级别决定了在访问数据时事务如何被锁定以及与其它进程隔离。默认情况下，`db2batch` 使用可重复读 (`RR`) 隔离级别。 |

| `-v` | 表示 `db2batch` 将以详细模式运行。（处理期间会将信息发送到标准错误输出。） |

| `-s` | 指定当发生非关键错误时 `db2batch` 是否应停止运行。 |

| `-q` | 指定如何返回查询结果。OFF 表示返回标准输出 (`stdout`) 和所有相关信息。ON 表示仅以未定义的 ASCII 格式返回查询结果。DEL 表示仅以定义的 ASCII 格式返回查询结果。 |

| `-h`|`-u`|`-?` | 显示帮助信息。当指定此选项时，将忽略所有其他选项，仅显示帮助信息。 |

使用 `db2batch` 实用程序进行基准测试简单的方法是构建包含一个或多个代表典型工作负载查询的文件，并将该文件的内容作为输入提供给 `db2batch` 命令。此类文件可能如下：

```
-- 文件名: wkload.sql
-- 执行命令:
  db2batch -d sample -f test.sql -r results.txt
```

```
--SET PER DETAIL 1
--SET ROWS OUT 5
-- 此查询列出了员工、其部门名称，以及对于分配了多个活动但少于全职的员工，其分配的活动数量。
```

### #COMMENT 查询 1

```sql
SELECT lastname, firstname,
deptname, count(*) AS num_act
FROM employee, department, emp_act
WHERE employee.workdept = department.deptno AND
employee.empno = emp_act.empno AND
emp_act.empty < 1
GROUP BY lastname, firstname, deptname
HAVING count(*) > 2;
```

一旦创建了此类文件，就可以执行类似下面的 `db2batch` 命令来进行基准测试（假设包含工作负载的文件名为 WKLO.SQL，且工作负载针对名为 SAMPLE 的数据库运行）：

```
db2batch -d sample -f test.sql -r results.txt
```

当执行此命令时，`db2batch` 收集的结果将记录在名为 RESULTS.TXT 的文件中，并可以在每次基准运行后进行审查。

## 设计顾问 (Design Advisor)

之前，我们看到了如何使用 `RUNSTATS` 实用程序更新系统目录统计信息，并强制 DB2 优化器使用这些统计信息提供优化计划。影响访问的另一个因素是适当索引的存在（或不存在）。那么，你如何决定索引何时会有益？设计顾问是一个特殊的工具，可以识别创建哪些索引、物化查询表 (`MQTs`) 或多维聚集表 (`MDC`) 可以提高性能。通过执行以下命令调用设计顾问：

```
db2advis [-d DatabaseName] [-w WorkloadName] [-s SQLStatement] [-i InFile] [-u UserID] [-p Password] [-k AdviseType] [-l DiskLimit] [-t MaxAdviseTime] [-o OutFile]
```

其中：

- `DatabaseName`: 与设计顾问交互的数据库。
- `WorkloadName`: 要分析的工作负载名称。
- `SQLStatement`: 要分析的单个 SQL 语句。
- `InFile`: 要分析的 语句集。
- `UserID`: 使用的身份 ID（用户 ID）。
- `Password`: 将使用的密码。
- `AdviseType`: 设计顾问分析的建议类型。有效值包括 `I`（索引）、`M`（物化查询表）、`C`（标准表转换为多维聚集表）和 `P`（重新分区）。
- `DiskLimit`: 所有 `MQTs` 可用的存储空间（兆字节）。
- `MaxAdviseTime`: 允许进行分析的最大时间（分钟）。当达到此时间限制时，设计顾问将停止。
- `OutFile`: 写入建议创建索引所需的 DDL 文件名。

此命令显示的所有其他选项均在表 6.6 中描述。

| 表 6.6 db2advis 命令选项 |

| 选项 | 含义 |

|---|---|

| `-q` | 表示从动态 SQL 快照中检索构成工作负载的 SQL 语句。如果与 `-p` 参数结合，则 SQL 语句将保存在 `ADVISE_WORKLOAD` 表中。 |

| `-op` | 指定工作负载来自 Query Patroller。 |

| `-k` | 指定工作负载的压缩程度。压缩是为了允许顾问降低执行复杂度，同时获得顾问在考虑完整工作负载时可以提供的结果。`HIGH` 表示顾问将集中在工作负载的小子集上。`MED` 表示顾问将集中在中等子集上。`LOW` 表示顾问将集中在较大的子集上。`OFF` 表示不进行任何压缩，并考虑每个查询。 |

| `-p` | 指定在运行设计顾问期间生成的计划将保留在解释表中。此选项导致 `-op` 和 `-g` 的工作负载保存在 `ADVISE_WORKLOAD` 表中，并将使用最终建议的工作负载查询计划保存在解释表中。 |

| `-h` | 显示帮助信息。当指定此选项时，将忽略所有其他选项，仅显示帮助信息。 |

确定索引、`MQT` 和/或 `MDC` 是否能提高工作负载的性能最简单的方法是创建一个包含一个或多个代表典型工作负载查询的文件，并将该文件的内容作为输入提供给 `db2advis` 命令。此类文件可能看起来如下所示：

- 文件名：`wkload.sql`
- 执行命令：`db2advis -d sample -i db2advis.sql -t 5`
- 对以下语句集执行 100 次评估

`#SET FREQUENCY 100`

`SELECT COUNT(*) FROM employee;`

`SELECT * FROM employee WHERE lastname='HAAS';`

- 对以下语句执行一次评估

`#SET FREQUENCY 1`

`SELECT AVG(bonus), AVG(salary) FROM employee`

`GROUP BY workload ORDER BY workload`

一旦创建创建了这样的文件，就可以通过执行类似所示的 `db2advis` 命令来进行分析（假设包含工作负载的文件名为 WKLOAD.SQL，且要在名为 SAMPLE 的数据库上运行该工作负载）：

```
db2advis -d sample -i db2advis.sql -t 5
```

当执行此命令时，产生的结果可能如下所示：

使用用户 ID 作为默认时间戳名称。使用 `-n` 选项指定架构

执行开始时间戳 2007-05-13-10.27.28.134000

从输入文件中找到 [3] SQL 语句

正在建议索引...

初始集合所需的总磁盘空间 [ 0.017 ] MB

总磁盘空间限制为 [ 11.439 ] MB

- 正在尝试解决方案的变体。

优化完成。

- 当前解决方案中有 1 个索引

[1520.9002] timerons（无建议）

[820.9002] timerons（带有当前解决方案）

改进了 [46.03%]

- 推荐索引的列表

============================

index[1], 0.017MB

CREATE INDEX "RSANDERS".IDX7051331427300000" ON "RSANDERS".EMPLOYEE"

# 522 第 6 章：DB2set

```
("LASTNAME" ASC, "COMM" ASC, "BONUS" ASC, "SALARY"
ASC, "BIRDATE" ASC, "SEX" ASC, "EDLEVEL" ASC, "JOB"
ASC, "HIREDATE" ASC, "PHONENO" ASC, "WORKDEPT" ASC
MIDINIT" ASC, "FIRSTNAME" ASC, "EMPNO" ASC) ALLOW
REVERSE SCANS;
COMMIT WORK;
RUNSTATS ON TABLE "RSANDERS".EMPLOYEE" FOR INDEX
"RSANDERS".IDX705131427300000";
COMMIT WORK;
```

-- 推荐的现有索引

=====================================

-- RUNSTATS ON TABLE "RSANDERS".EMPLOYEE" FOR INDEX "RSANDERS".XEMP2"

-- COMMIT WORK;

-- 未使用的现有索引

=====================================

--

--

顾问评估了 31 种解决方案

DB2 工作负载性能顾问工具已完成。
