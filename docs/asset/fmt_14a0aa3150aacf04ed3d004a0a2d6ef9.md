
| NAME | EXTENTS | RSSIZE | Active-actions WAITS | GETS | OPTIMIZE | STATUS |
|---|---|---|---|---|---|---|
| SYSTEM | 7 | 581632 | 0 | 389 | | ONLINE |
| RBS0 | 20 | 20963328 | 0 | 494 | 20971520 | ONLINE |
| RBS1 | 20 | 20963328 | 0 | 413 | 20971520 | ONLINE |
| RBS2 | 20 | 20963328 | 0 | 377 | 20971520 | ONLINE |
| RBS23 | 20 | 20963328 | 0 | 364 | 20971520 | ONLINE |
| RBS24 | 20 | 20963328 | 0 | 338 | 20971520 | ONLINE |

26行已。

## Unix 和 Linux Oracle DBA

在处理回滚段时，需要监控的下一个领域是回卷（`wraps`）和扩展（`extends`）。
`wraps`的存在意味着你的区太小了。`extends`超过`MINTEXTENTS`的数量表示区太小和或区的数量太少。记住，每当 Oracle 拥有一个区时，磁盘上就会分配新的空间，这会对性能产生影响。此外，尽量避免过度的收缩（`shrinks`），这是区太少且`OPTIMAL`值过低的迹象。以下查询显示了`wraps`、`extents`以及其他诊断信息。

```
SQL> select name, extents, extends, optsize
2 hmwsize, wraps, extents, curext
3 from v$roll name, v$stat stat
4 where name.umn = stat.stat
5 /
```
