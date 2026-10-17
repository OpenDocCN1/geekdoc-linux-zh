
| 执行次数 > 1 的 SQL %: | 53.78 | 58.42 |

| SQL/执行占内存 %: | 63.47 | 79.74 |

STATPACK 还包含第二个部分，标题为“数据库库缓存（Library Cache for DB）”，它显示了与上一节中 VLIBRARYCACHE 查询中相同的无效化和重加载信息。图 4.4 显示了来自名为 PROD 数据库的示例 STATPACK 输出。

# 图 4.4 显示库缓存无效化和重加载的 STATPACK 输出

| 数据库: PROD 的库缓存活动: 实例快照: 1 -2 | | |

| ->"Pct Misses（缺失率）" 应该非常低 | |

| 命名空间 (Namespace) | 获取请求 (Get Requests) | 获取缺失 (Get Miss) | P 请求 (P Requests) | 缺失 (Miss) | 重加载 (Reloads) | 无效化 (Invalidations) |

|---|---|---|---|---|---|---|

| 体 (BODY) | 7 | 0.0 | | 0.0 | | 0 |

| SQL AREA | 72 | 2.8 | | 428 | 11.4 | 20 |

| 表格/过程 (TABLE/PROCEDURE) | 219 | 0.5 | | 390 | 16.9 | 0 |

STATPACK 的这一部分还显示了关于库缓存获取率（Get ratio）的信息。然而，在 STATPACK 输出中，性能是用缺失率而不是所述的命中率来表示的。图 4.4 显示 SQL AREA 命名空间 Get Requests 活动的 Pct Miss 值为 2.8 或 2.8%。相反，这意味着库缓存的 SQL AREA 部分在监控期间的命中率为 97.2%——远高于 Oracle 建议的 90% 指南。

## 使用 REPORT.TXT 监控库缓存

运行 `UTLBSTAT.SQL` 和 `UTLESTAT.SQL` 生成的 `REPORT.TXT` 文件也包含一个显示库缓存 GETHITRATIO、PINHITRATIO、RELOADADS 和 INVALIDATIONS 信息的部分。图 4.5 显示了 `REPORT.TXT` 文件的相关部分。

共享池性能测量 215

# 4.5 显示库缓存统计的 REPORT.TXT 输出

```
SQL column library format al2 trunc;
SQL column pinhitratio heading 'PINHITRAT';
SQL column gethitratio heading 'GETHITRAT';
SQL column invalidations heading 'INVALIDAT';
SQL set number with id;
SQL item select Library cache statistics. The pin hit rate should be
1 library;
2 gets;
3 decode(gethits,0.1,0,0,0,0)
4 pinhitratio;
5 decode(pins,0.1,0,0,0)
6 pinhitratio;
7 invalidations
8 from
9
```

| 库 (LIBRARY) | 获取次数 (GETS) | 获取命中率 (GETHITRAT) | 针命中率 (PINHITRAT) | 重加载次数 (RELOADS) | 无效化 (INVALIDATIONS) |

|---|---|---|---|---|---|

| 体 (BODY) | 10 | .1 | 10 | 0 |

| 簇 (CLUSTER) | 176 | .989 | 258 | 0 |

| 索引 (INDEX) | 0 | 0 | 0 | 0 |

| 数据 (DATA) | 0 | 0 | 0 | 0 |

| 资源 (RESOUR) | 0 | 0 | 0 | 0 |

| 源 (SOURCE) | 0 | 0 | 0 | 0 |

| 管道 (PIPE) | 0 | 0 | 0 | 0 |

| SQL | 3669 | .993 | 836 | 0 |

| 表格/过程 (TABLE/PROCEDURE) | 1224 | .859 | 763 | 0 |

| 触发器 (TRIGGER) | 82 | .89 | 82 | 0 |

（注：原文中 SQL 块内容由于存在乱码或占位符，根据“代码块不需要翻译”原则保留，但原文提供的 SQL 块内容较为混乱，此处保持结构逻辑。由于原文提供的 SQL 块中包含不完整的逻辑，翻译部分主要修正了表格对应的对应关系）

## 衡量共享池（Shared Pool）的性能 219

DB 统计信息。STATPACK 报告该部分的示例输出如图 4.9 所示。

### 图 4.9 显示数据字典缓存命中率 STATPACK 输出

```
dictionary Cache Stats for DB: PROD. Instance: prod. Snaps: 1 -2
>>"Misses" 应该较低（大多数情况下小于 2%）
>>"Cache Usage" 是正在被使用的缓存条目数
>>"SGA" 是该缓存总大小的比例
Cache | Get Requests | Miss | Scan | Reqs | Scan Miss | Mod | Reqs | Final Usage | SGA |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| dc_free_extents | 4 | 0.0 | 0 | 0 | 0 | 0 | 30 | 88 | |
| dc_object_ids | 39 | 0.0 | 0 | 0 | 0 | 0 | 40 | 99 | |
| dc_objects | 83 | 1.2 | 0 | 0 | 0 | 0 | 63 | 111 | |
| dc_profiles | 80 | 0.0 | 0 | 0 | 0 | 0 | 21 | 91 | |
| dc_rollback_segments | 56 | 0.0 | 0 | 0 | 0 | 0 | 180 | 94 | |
| dc_segments | 6 | 0.0 | 0 | 0 | 0 | 0 | 9 | 60 | |
| dc_tables | 10 | 0.0 | 0 | 0 | 0 | 0 | 15 | 81 | |
| dc_user_requests | 28 | 0.0 | 0 | 0 | 0 | 0 | 17 | 81 | |
| dc_users | 45 | 0.0 | 0 | 0 | 0 | 0 | 19 | 86 | |
```

与库缓存（Library Cache）类似，数据字典缓存性能的 STATPACK 输出也是以缺失率的形式表示。图 4.9 显示，数据字典缓存每个组件（例如 `dc_free_extents`、`dc_object_ids`）的 P Miss 值范围在 0 到 3.6% 的缺失率之间。相反，这意味着在监控期间，数据字典缓存的命中率为 96.4% 和 100%。

![](img/c36db8fbb4893c630ad429a99bfd63e3_258_0.png)

> Oracle 建议，如果 STATPACK 输出显示数据字典缓存任何单个组件（例如 `dc_free_extents`、`dc_object_ids`）的命中率在大多数组件中低于 98%，则应考虑对共享池进行调优。

## 使用 REPORT.TXT 监控数据字典缓存

数据字典信息也包含在 `UTLSTAT.SQL` 和 `UTLESTAT.SQL` 生成的 `REPORT.TXT` 中。像 STATPACK 一样，`REPORT.TXT` 会为每个缓存的组件单独显示数据字典缓存统计信息。然后，你需要在计算总命中率之前手动添加 GET_RE 和 GET_MISS 列。图 4.10 显示了 REPORT TX 文件的相关部分。

## 220 第 4 章 · 调优共享池

### 图 4.10 显示数据字典缓存统计信息的 REPORT.TXT 输出
