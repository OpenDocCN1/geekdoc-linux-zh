
## Listing 17-5: A range partitioning syntax example

```sql
CREATE TABLE sales
(
    invoice_no    NUMBER,
    sales_amount  NUMBER(7,2),
    sales_date    DATE)
PARTITION BY RANGE (sales_date)
(PARTITION sales_q1_03 VALUES LESS THAN ('01-APR-2003')
  TABLESPACE ts_sales_q1_03,
 PARTITION sales_q2_03 VALUES LESS THAN ('01-JUL-2003')
  TABLESPACE ts_sales_q2_03,
 PARTITION sales_q3_03 VALUES LESS THAN ('01-OCT-2003')
  TABLESPACE ts_sales_q3_03,
 PARTITION sales_q4_03 VALUES LESS THAN (MAXVALUE)
  TABLESPACE ts_sales_q4_03);
```

> **NOTE**
> *Each partition can have its own storage clause parameters.*

The MAXVALUE clause specifies the default partition for values that do not meet the other partitions’ requirements. If an application will be adding partitions with a new range (for example, data organized in partitions by a quarterly date), don’t use the MAXVALUE clause.

> **NOTE**
> *If the MAXVALUE clause is not used, an error is returned if the data does not match the requirements for any of the partitions.*

## Hash Partitioning

Hash partitioning takes the partition key and applies a mathematical calculation to derive a unique number known as the *hash value*. Hash values are randomly distributed throughout the range of all possible values, so this value can be used to evenly distribute the rows across the assigned tablespaces. Listing 17-6 illustrates the hash partitioning syntax. The MAXVALUE clause is not applicable to hash partitioning.

## Listing 17-6: A hash partitioning syntax example

```sql
CREATE TABLE sales
(
    invoice_no    NUMBER,
    sales_amount  NUMBER(7,2),
    sales_date    DATE)
PARTITION BY HASH (invoice_no)
(PARTITION p1 TABLESPACE SALES_p1,
 PARTITION p2 TABLESPACE SALES_p2,
 PARTITION p3 TABLESPACE SALES_p3,
 PARTITION p4 TABLESPACE SALES_p4);
```

## Composite Partitioning

Composite partitioning is a combination of both range and hash partitioning. Listing 17-7 illustrates the syntax for composite partitioning. Notice that there is a RANGE clause and then the SUBPARTITION BY HASH. The table will be partitioned by the range partition key, and then evenly distributed across the subpartitions using the hash value of the key. In this example, the STORE IN clause identifies the tablespaces, and within each tablespace there will be four partitions. This example shows four partitions (P1–P4), each of which has four subpartitions.

## Listing 17-7: A composite partitioning syntax example

```sql
CREATE TABLE sales
(invoice_no NUMBER,
 sales_amount NUMBER(7, 2),
 sales_date DATE)
PARTITION BY RANGE(sales_date)
SUBPARTITION BY HASH (invoice_no)
SUBPARTITIONS 4
STORE IN (TS_SALES_P1, TS_SALES_P2, TS_SALES_P3, TS_SALES_P4)
(PARTITION p1 VALUES LESS THAN ('01-APR-2000'),
 PARTITION p2 VALUES LESS THAN ('01-JUL-2000'),
 PARTITION p3 VALUES LESS THAN ('01-OCT-2000'),
 PARTITION p4 VALUES LESS THAN (MAXVALUE));
```

## List Partitioning

List partitioning assigns rows to partitions according to character values. The syntax illustrated in Listing 17-8 looks much like the IN clause of a SQL statement WHERE clause. The OTHER clause is used to define a default tablespace for values that do not meet any of the other partition requirements. If this option is omitted, then an error will be returned to the application/user if a value is presented that is not in one of the partition's lists.

## Listing 17-8: A list partitioning syntax example

```sql
CREATE TABLE sales
(invoice_no NUMBER(6),
 sales_amt NUMBER(7,2),
 sales_date VARCHAR(2),
 sales_state CHAR(2))
PARTITION BY LIST(sales_state)
    (PARTITION sales_north VALUES ('ME','VT','NH','MA','RI','CT')
        TABLESPACE ts_sales_north,
    PARTITION sales_east VALUES ('NJ','NY','PA','VA','NC','WV')
        TABLESPACE ts_sales_east,
    PARTITION sales_west VALUES ('CA','UT','NM','CO','MT','OR','WA')
        TABLESPACE ts_sales_west,
    PARTITION sales_south VALUES ('FL','TX','SC','AR','TN','KY')
        TABLESPACE ts_sales_south,
    PARTITION sales_midwest VALUES ('IA','IL','IN','MI','MO','NE','OH')
        TABLESPACE ts_sales_midwest,
    PARTITION others VALUES (DEFAULT) TABLESPACE ts_default);
```

> **NOTE**
> *List partitioning can have only one partitioning column.*

## Index Partitioning Options

*Index partitioning allows for indexes on larger table structures to be broken into smaller units and distributed across multiple tablespaces. There are two types of partitioned indexes: locally partitioned and globally partitioned indexes.*

Indexes that use the table's partitioning parameters are called *locally partitioned* indexes. These indexes have the same partitioning key, number of tablespaces, and partitioning parameters as the table the index is associated with. They can index the partitioning key value or one or more (composite key) different columns in the table, and still follow the partitioning and tablespace assignment rules used by the underlying table. Listing 17-9 illustrates the syntax for a locally partitioned index. Notice the `LOCAL` syntax and that there is no `PARTITION BY RANGE` or `PARTITION BY LIST` clause. Listing 17-10 illustrates a nonprefixed locally partitioned index syntax example. Note that the index is being built on a different key value from the partitioning key of the underlying table. Both of these indexes would be on any of the preceding partitioned table examples (those in Listing 17-5). Notice that these syntax examples have the same number of partitions as in the syntax in Listing 17-5.

### Listing 17-9: A local prefix partition index syntax example

```sql
CREATE INDEX SALES_DATE_PT_IDX ON sales (sales_date)
LOCAL
(PARTITION sales_idx_q1_03 TABLESPACE ts_sales_idx_q1_03,
 PARTITION sales_idx_q2_03 TABLESPACE ts_sales_idx_q2_03,
 PARTITION sales_idx_q3_03 TABLESPACE ts_sales_idx_q3_03,
 PARTITION sales_idx_q4_03 TABLESPACE ts_sales_idx_q4_03);
```

### Listing 17-10: A local nonprefixed partition index syntax example

```sql
CREATE INDEX SALES_INVOICE_PT_IDX ON sales (invoice_no)
LOCAL
(PARTITION sales_idx_q1_03 TABLESPACE ts_sales_idx_q1_03,
 PARTITION sales_idx_q2_03 TABLESPACE ts_sales_idx_q2_03,
 PARTITION sales_idx_q3_03 TABLESPACE ts_sales_idx_q3_03,
 PARTITION sales_idx_q4_03 TABLESPACE ts_sales_idx_q4_03);
```

If a partitioned index’s key value is the same as its partitioning value, this is known as a *prefixed* partitioned index. A nonprefixed partitioned index key column is not the same column as the partition key.

Local indexes do not have to have a PARTITION clause. If this clause is not used, Oracle will generate partition names and assign the index partitions to the same tablespaces as the underlying table. This might not give the best SQL performance.

> **NOTE**
> I would always list the PARTITION clause, since I don’t like Oracle taking defaults (they can change with releases) and I like to separate the indexes from the tables.

Globally partitioned indexes can have their own partitioning values (PARTITION BY RANGE or PARTITION BY LIST clause) and their own individual tablespace assignments. Globally partitioned indexes are always prefixed indexes, as Oracle 10g does not support nonprefixed globally partitioned indexes. Listing 17-11 illustrates the syntax of a possible globally partitioned index on any of the earlier table syntax examples, but this illustration uses Listing 17-5 specifically. Notice that this index has its own range clause/list clause.

### Listing 17-11: A global partitioned index syntax example

```sql
CREATE INDEX sales_invoice_pt_idx ON sales (invoice_no)
GLOBAL
(PARTITION BY RANGE(sales_date)
(PARTITION sales_idx_p1 VALUES LESS THAN '01-JUL-03'
 TABLESPACE ts_sales_idx_p1,
 PARTITION sales_idx_p2 VALUES LESS THAN '01-JAN-04'
 TABLESPACE ts_sales_idx_p2,
 PARTITION sales_idx_p3 VALUES LESS THAN (MAXVALUE)
 TABLESPACE sales_idx_p3));
```

## IOT Partitioning Options

IOTs can also be partitioned, and the overflow tablespace can be partitioned as well. IOTs support RANGE, HASH, and LIST partitioning, but not composite partitioning. Listing 17-12 illustrates the syntax for a RANGE partitioning example of an IOT. Notice that individual overflow tablespaces can be defined at the partition level.

### Listing 17-12: A partitioned IOT syntax example

```sql
CREATE TABLE sales
       (
         invoice_no   NUMBER,
         sales_amount NUMBER(7,2),
         sales_date   DATE,
         PRIMARY KEY (invoice_no) )
  ORGANIZATION INDEX
       INCLUDING sales_amount
       OVERFLOW TABLESPACE ts_sales_q1_03_overflow
  PARTITION BY RANGE (sales_date)
  (
    PARTITION sales_q1_03 VALUES LESS THAN ('01-APR-2003')
      TABLESPACE ts_sales_q1_03,
    PARTITION sales_q2_03 VALUES LESS THAN ('01-JUL-2003')
      TABLESPACE ts_sales_q2_03 OVERFLOW ts_sales_q2_03_overflow,
    PARTITION sales_q3_03 VALUES LESS THAN ('01-OCT-2003')
      TABLESPACE ts_sales_q3_03 OVERFLOW ts_sales_q3_03_overflow,
    PARTITION sales_q4_03 VALUES LESS THAN (MAXVALUE)
      TABLESPACE ts_sales_q4_03 OVERFLOW ts_sales_q4_03_overflow );
```

IOT partitions must all have the same block size. The overflow tablespaces can have a different block size from that used by the IOT itself, but all overflow tablespaces must have the same block size.

## Using Partitioned Indexes for Performance

Oracle provides several methods of partitioning for various application needs. There won't be any performance gain with any of the partitioning options if the partitioning key is not referenced in the WHERE clause of the SQL statement. Hash partitioning
