

大多数人应该让超过 95% 的数据从 RAM 中提供，虽然主要例外情况是如果你经常更新或删除行——MySQL 无法缓存不断变化的内容。如果你的站点主要是只读的，这个比例应约为 98%。较低的数值意味着你可能需要增加 key buffer 的大小。

如果遇到问题，下一步是检查当前 key buffer 有多少被使用。 使用 SHOW VARIABLES 命令并查找 key_buffer_size 变量的值。它可能类似于 8388600，也就是八百万字节，或 8MB。 现在，使用 SHOW STATUS 命令并查找 Key_blocks_used 的值。

你现在可以通过将 Key_blocks_used 乘以 1024，除以 key_buffer_size 再乘以 100 来确定 key buffer 的使用量。 例如，如果 Key_blocks_used 是 8000，你将其乘以 1024 得到 8192000；然后用你的 key_buffer_size（8388600）除它得到 0.97656，最后乘以 100 得到 97.656。 因此，几乎有 98% 的 key buffer 被使用。

现在，进入重要部分：你已经确定自己从磁盘读取了大量键，并且你现在也知道从磁盘读取的原因几乎可以肯定是因为你没有为 key buffer 分配足够的 RAM。 一个经验法则是将尽可能多的 RAM 分配给 key buffer，最高不超过系统 RAM 的 25%——在 512MB 的系统上，128MB 对于大量读取键的系统来说是理想的。 超过这个限度，你会看到性能急剧下降，因为系统必须为 key buffer 使用虚拟内存。

在文本编辑器中打开 /etc/my.cnf，并查找包含 key_buffer_size 的行。 如果你没有，可以创建一个新的——它应该在 [mysqld] 行之下。 设置新值时，不要随意选择一个很高的数字。 尝试将当前的值翻倍（如果没有现有行则尝试 16MB）；然后看看效果如何。 要将 key buffer 大小设置为 16MB，你需要类似这样的行：

```
[mysqld]
set-variable = key_buffer_size=16M
datadir=/var/lib/mysql
```

使用 service mysqld restart 重启你的 MySQL 服务器，然后再次进入 MySQL 运行 SHOW VARIABLES 以查看 key_buffer_size。 如果你将其设置为 16M，它应该是 16773120。 现在，由于 MySQL 刚刚被重置，其关于 key hits 等的所有值也将被重置。 你需要让它运行一段时间以便评估变化程度。 如果你有一个测试系统可以运行，现在是运行它的时候。

在数据库经过正常使用一段时间后（如果你访问频繁，这可能只有几分钟），重新计算 key buffer 的使用量。 如果你再次得到一个较高的分数，再次将大小加倍，重启并重新测试。 你应该一直重复此操作，直到看到 key buffer 使用率低于 50% 或发现你没有足够的 RAM 来进一步增加缓冲区——记住，你永远不应将超过系统 RAM 25% 分配给 key buffer。

## 使用查询缓存

MySQL 的较新版本允许你缓存查询结果，这样，如果进来新的查询使用完全相同的 SQL，结果就可以从 RAM 中提供。 在某种程度上查询缓存非常智能：如果例如由于另一个查询导致结果的一部分发生变化，已缓存的结果将被丢弃并在下次重新计算。 然而，在其他方面它非常简单。 例如，它仅在新查询与已缓存查询完全相同的情况下才使用缓存结果，甚至包括 SQL 的大小写。

查询缓存在大多数场景下工作良好。 如果你的站点读写混合相等，查询缓存会尽力而为但不会最优。 如果你的站点主要是读取且写入很少，更多查询将被缓存（并且缓存时间更长），从而提高整体性能。

首先，你需要找出是否启用了查询缓存。 为此，使用 SHOW VARIABLES 并查找 have_query_cache 的值。 一切正常的话，你应该得到 YES，表示查询缓存已启用。 接下来，查找 query_cache_size 和 query_cache_limit 的值——前者是分配给查询缓存的 RAM 字节数，后者是应被缓存的最大结果大小。 这两个值的良好起始值是 8388608（8MB）和 1048576（1MB）。

接下来，输入 SHOW STATUS LIKE 'Qcache%'; 以查看有关查询缓存的所有状态信息。 你应该得到类似这样的输出：

```
mysql> SHOW STATUS LIKE 'Qcache%';
+---------------+-------+
| Variable_name | Value |
+---------------+-------+
| Qcache_free_blocks | 1 |
| Qcache_free_memory | 169544 |
| Qcache_hits | 698 |
| Qcache_inserts | 38 |
| Qcache_lowmem_prunes | 20 |
| Qcache_not_cached | 0 |
| Qcache_queries_in_cache | 18 |
| Qcache_total_blocks | 57 |
+---------------+-------+
8 rows in set (0.00 sec)
```

从中，我们可以看到缓存中只有 18 个查询（Qcache_queries_in_cache），缓存中剩余 169544 字节的内存（Qcache_free_memory），698 个查询已从缓存中读取（Qcache_hits），38 个查询已插入缓存（Qcache_inserts），但其中 20 个因内存不足而被移除（Qcache_lowmem_prunes），得到之前的 18。 Qcache_not_cached 为 0，这意味着 0 个查询未被缓存——MySQL 已缓存它们全部。

从中，我们可以计算总共进来的查询数——它是 Qcache_hits、Qcache_inserts 和 Qcache_not_cached 的总和，为 736。 我们也可以通过将 Qcache_hits 除以该数字来计算查询缓存的使用效率，并

