```
PARTITION BY LIST(sales_state)
    (PARTITION sales_north VALUES ('ME','VT','NH','MA','RI','CT')
        TABLESPACE ts_sales_north
    (PARTITION sales_east VALUES ('NJ','NY','PA','VA','NC','WV')
        TABLESPACE ts_sales_east,
    PARTITION sales_west VALUES ('CA','UT','NM','CO','MT','OR','WA')
        TABLESPACE ts_sales_west,
    PARTITION sales_south VALUES ('FL','TX','SC','AR','TN','KY')
        TABLESPACE ts_sales_south,
    PARTITION sales_midwest VALUES ('IA','IL','IN','MI','MO','NE','OH')
        TABLESPACE ts_sales_midwest
    PARTITION others VALUES (DEFAULT ) TABLESPACE ts_default);
```

> **NOTE**
> *List partitioning can have only one partitioning column.*

# ## Index Partitioning Options

*Index partitioning allows for indexes on larger table structures to be broken into smaller units and distributed across multiple tablespaces. There are two types of partitioned indexes: locally partitioned and globally partitioned indexes.*

Indexes that use the table's partitioning parameters are called *locally partitioned* indexes. These indexes have the same partitioning key, number of tablespaces, and partitioning parameters as the table the index is associated with. They can index the partitioning key value or one or more (composite key) different columns in the table, and still follow the partitioning and tablespace assignment rules used by the underlying table. Listing 17-9 illustrates the syntax for a locally partitioned index. Notice the `LOCAL` syntax and that there is no `PARTITION BY RANGE` or `PARTITION BY LIST` clause. Listing 17-10 illustrates a nonprefixed locally partitioned index syntax example. Note that the index is being built on a different key value from the partitioning key of the underlying table. Both of these indexes would be on any of the preceding partitioned table examples (those in Listing 17-5). Notice that these syntax examples have the same number of partitions as in the syntax in Listing 17-5.

# ### Listing 17-9: A local prefix partition index syntax example

```
CREATE INDEX SALES_DATE_PT_IDX ON sales (sales_date)
LOCAL
(PARTITION sales_idx_q1_03 TABLESPACE ts_sales_idx_q1_03,
PARTITION sales_idx_q2_03 TABLESPACE ts_sales_idx_q2_03,
PARTITION sales_idx_q3_03 TABLESPACE ts_sales_idx_q3_03,
PARTITION sales_idx_q4_03 TABLESPACE ts_sales_idx_q4_03);
```