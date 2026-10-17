
使用 `mysqld restart` 重启你的 MySQL 服务器，然后回到 MySQL 运行 `SHOW VARIABLES` 查看你的 `key_buffer_size`。如果你将其设置为 16M，它应该是 16,773,120。现在，由于 MySQL 刚刚被重置，你所有的键命中数等指标的值也会被重置。你需要让它运行一段时间，以便评估变化了多少。如果你有一个可以运行的测试系统，现在就是运行它的时机。

在数据库以正常用量访问了一段时间后（如果访问频繁，可能只有几分钟），重新计算键缓冲区的使用率。如果你得到另一个高分，再次将大小翻倍，重启并测试。你应该不断重复，直到你的键缓冲区使用率低于 50%，或者你发现没有足够的 RAM 来进一步增加缓冲区。记住，你永远不应该为键缓冲区分配超过系统 RAM 25% 的内存。

## 使用查询缓存 (Query Cache)

新版本的 MySQL 允许你缓存查询结果，这样当使用相同 SQL 的新查询进来时，就可以从 RAM 提供结果。在某些方面，查询缓存是智能的；例如，如果结果由于另一个查询而发生变化，缓存的结果将被丢弃并在下次运行时重新计算。但在其他方面，它又非常简单。例如，只有当新查询与缓存查询完全相同时（甚至包括 SQL 的大小写）时，它才会使用结果。

查询缓存在许多场景下工作。如果你的网站读写比例均衡，查询缓存会尽力而为但并非最优。如果你的网站以读为主、写较少，会有更多的查询被缓存（缓存时间更长），从而提高整体性能。

## MySQL 425

首先，你需要确定是否开启了查询缓存。运行 `SHOW VARIABLES` 并查找 `have_query_cache` 的值。一切顺利的话，你应该得到 `YES`，这意味着查询缓存已启用。接下来查看 `query_cache_size` 和 `query_cache_limit` 的值。第一个是分配给查询缓存的 RAM 大小（字节），第二个是应该被缓存的最大结果大小。这两个值的良好起始值是 8,388,608 (8MB) 和 1,048,576 (1MB)。

接下来，输入 `SHOW STATUS LIKE 'qcache'` 查看关于查询缓存的所有状态信息。你应该得到如下输出：

```
mysql> SHOW STATUS LIKE 'qcache'

|--------------------------------------|

| Variable_name | Value |

|--------------------------------------|

| Qcache_free_blocks | 1 |

| Qcache_free_memory | 169544 |

| Qcache_hits | 698 |

| Qcache_inserts | 38 |

| Qcache_lowmem_prunes | 20 |

| Qcache_not_cached | 0 |

| Qcache_queries_in_cache | 18 |

| Qcache_total_blocks | 57 |

|--------------------------------------|

8 rows in set (0.00 sec)
```

从这里，你可以看到缓存中只有 18 个查询 (`Qcache_queries_in_cache`)，缓存中你有 169,544 字节的空闲内存 (`Qcache_free_memory`)，698 个查询从缓存中读取 (`Qcache_hits`)，有 38 个查询被插入缓存中 (`Qcache_inserts`)，但其中 20 个因为内存不足被移除 (`Qcache_lowmem_prunes`)，`Qcache_not_cached` 为 0，意味着 0 个查询未被缓存；MySQL 缓存了所有内容。

通过所有这些，你可以计算查询缓存命中次数：它是 `Qcache_hits`、`Qcache_inserts` 和 `Qcache_not_cached` 的和，结果为 736。你还可以通过将 `Queries_hits` 除以数量并乘以 100 来计算查询缓存的使用情况。在这种情况下，94.84% 的查询是从缓存中提供的。

在某些情况下，可以通过编辑 `/etc/my.cnf` 文件并在 `[mysqld]` 部分添加如下行来更改设置：

```
set-variable = query_cache_size=32M
```
