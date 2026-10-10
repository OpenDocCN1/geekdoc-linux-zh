|  |  |  |  |  |  |  |  |
|---|---|---|---|---|---|---|---|
| 1 | template1 | 0 | 0 | 0 | 0 | 0 |  |
| 0 |  | 0 | 0 | 0 |  |  |  |
| 11563 | template0 | 0 | 0 | 0 | 0 | 0 |  |
| 0 |  | 0 |  |  |  |  |  |
| 11564 | postgres | 1 | 3876 | 0 |  | 116 |  |
| 61544 |  | 1075635 | 6775 | 0 |  | 0 |  |
(3 rows)

This example is from a default PostgreSQL install so the default databases are listed, but you would also see any databases you have created as well.

# pg_stat_all_tables

The pg_stat_all_tables table stores statistics on a per-table basis including sequential scan statistics, index scan statistics, and data about the number of other operations performed on that table. Since this stores data on all the existing tables, the default select will return a lot of data:

```
postgres=# select * from pg_stat_all_tables;
      relid |  schemaname  |     relname      | seq_scan | seq_tup_read | idx_scan | idx_tup_fetch | n_tup_ins | n_tup_upd | n_tup_del | n_tup_hot_upd | n_live_tup | n_dead_tup | last_vacuum | last_autovacuum | last_analyze | last_aut
oanalyze
```

|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 2753 | pg_catalog | pg_opfamily |  |  | 0 | 0 |  |  |  |  |  |  |  |  |  |
|  | 0 |  | 0 | 0 | 0 |  |  | 0 |  |  |  |  |  |  |  |
|  |  | 0 |  |  |  |  |  |  |  |  |  |  |  |  |  |
| 2617 | pg_catalog | pg_operator |  |  | 0 | 0 |  |  |  |  |  |  |  |  |  |
|  | 7 |  | 7 |  | 0 |  |  | 0 |  |  |  |  |  |  |  |
|  | 0 |  | 0 |  |  |  |  | 0 |  |  |  |  |  |  |  |
| ... |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| 2328 | pg_catalog | pg_foreign_data_wrapper |  |  | 0 | 0 |  |  |  |  |  |  |  |  |  |
|  | 0 |  | 0 | 0 | 0 |  |  | 0 |  |  |  |  |  |  |  |
|  | 0 |  | 0 |  |  |  |  |  |  |  |  |  |  |  |  |
(65 rows)

This is definitely an example where you might want to prune the output with specific SQL queries to get the data you want. Of course, it may just