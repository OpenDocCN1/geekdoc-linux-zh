```
PARTITION BY HASH (invoice_no)
(PARTITION p1 TABLESPACE SALES_p1,
PARTITION p2 TABLESPACE SALES_p2,
PARTITION p3 TABLESPACE SALES_p3,
PARTITION p4 TABLESPACE SALES_p4);
```

# ## Composite Partitioning

Composite partitioning is a combination of both range and hash partitioning. Listing 17-7 illustrates the syntax for composite partitioning. Notice that there is a RANGE clause and then the SUBPARTITION BY HASH. The table will be partitioned by the range partition key, and then evenly distributed across the subpartitions using the hash value of the key. In this example, the STORE IN clause identifies the tablespaces, and within each tablespace there will be four partitions. This example shows four partitions (P1–P4), each of which has four subpartitions.

# **Listing 17-7: A composite partitioning syntax example**

```
CREATE TABLE sales
(invoice_no NUMBER,
sales_amount NUMBER(7, 2),
sales_date DATE)
PARTITION BY RANGE(sales date)
SUB PARTITION BY HASH (invoice_no)
SUB PARTITIONS 4
STORE IN (TS SALES P1, TS SALES P2, TS SALES P3, TS SALES P4)
(PARTITION p1 VALUES LESS THAN ('01-APR-2000'),
PARTITION p2 VALUES LESS THAN ('01-JUL-2000'),
PARTITION p3 VALUES LESS THAN ('01-OCT-2000'),
PARTITION p4 VALUES LESS THAN (MAXVALUE));
```

# ## List Partitioning

List partitioning assigns rows to partitions according to character values. The syntax illustrated in Listing 17-8 looks much like the IN clause of a SQL statement WHERE clause. The OTHER clause is used to define a default tablespace for values that do not meet any of the other partition requirements. If this option is omitted, then an error will be returned to the application/user if a value is presented that is not in one of the partition's lists.

# **Listing 17-8: A list partitioning syntax example**

```
CREATE TABLE sales
(invoice_no NUMBER(6),
sales_amt NUMBER(7,2),
sales_date VARCHAR(2),
sales_date DATE)
```