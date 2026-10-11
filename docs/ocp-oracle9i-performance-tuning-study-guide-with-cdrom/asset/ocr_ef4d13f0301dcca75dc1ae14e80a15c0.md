By examining trace files and Explain Plans, you have determined that a B-Tree index on the LAST_NAME column of the table will likely help performance of querying against the EMPLOYEE table:

```
SQL> CREATE INDEX employee_last_name_idx
2  ON employee (last_name)
3  TABLESPACE APPL_IDX;
```

The resulting index would store the values for the LAST_NAME column, along with the row IDs for those values, in a B-Tree structure as shown in Figure 3.13.

# FIGURE 3.13 Index contents and structure for B-Tree index on LAST_NAME column of EMPLOYEE

![](bbox=[0.25, 0.37, 0.87, 0.58])

By first searching the index, which is arranged in the multileveled tree structure, and then accessing the required table data by row ID, costly full-table scan operation is avoided and query performance is enhanced. B-Tree indexes are very useful when executing queries that will return only a small number of the overall rows found in a table. As a rule of thumb, Oracle recommends considering a B-Tree indexing strategy whenever queries frequently return less than 5 percent of the total rows in the table. The best candidates for B-Tree indexes are those columns having high cardinality in their data. These columns should also be frequently used in SQL statement WHERE clauses.

By design, B-Tree indexes are always balanced. This is true because the Oracle Server continually splits full index blocks as new values are added to the table that the index is built on. However, as insert and delete activity occurs on a table, its associated indexes can develop many levels. This tends to degrade the efficiency of the B-Tree index because it takes the Oracle Server longer to work its way from the root, or starting block, down to the