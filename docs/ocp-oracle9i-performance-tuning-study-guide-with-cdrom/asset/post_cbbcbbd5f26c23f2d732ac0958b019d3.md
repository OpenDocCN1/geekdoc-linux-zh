
per Oracle block. If we have a 2048-byte (2K) Oracle block size, then this parameter indicates that we expect to get about two (2048/1000 ≈ 2.048) cluster keys per block. In other words, you expect to store the data for two teachers and all of their students in each Oracle block. Choosing the proper value for SIZE is difficult if all the cluster key values (teachers) don't have the same number of clustered records (students). However, setting this value properly is critical to gaining optimal cluster performance:

```
SQL> CREATE INDEX TEACHER_STUDENT_IDX
2  ON CLUSTER teacher_student
3  TABLESPACE apps_idx;
```

Index created.

Notice that the indexed column is not specified when creating an index on a cluster segment. The index is automatically created on the cluster key column, TEACHER_ID.

Now that the cluster structure exists, you can create the TEACHER and STUDENT tables in the cluster:

```
SQL> CREATE TABLE TEACHER
2  (teacher_id number,
3   last_name varchar2(20),
4   first_name varchar2(20),
5   room_number number)
6  CLUSTER teacher_student
7  (teacher_id);
```

Table created.

```
SQL> CREATE TABLE student
2  (student_id number,
3   last_name varchar2(20),
4   first_name varchar2(20),
5   teacher_id number)
6  CLUSTER teacher_student
7  (teacher_id);
```

Table created.

Note that no tablespace specification is given when creating the tables in the cluster. This is not because we want to use the default tablespace for the user, but because the cluster itself is the storage area for each table's data. In this way, any data inserted into the TEACHER or STUDENT table will be stored in the same physical blocks—the blocks of the cluster segment they are contained in. Figure 3.28 shows the relationship between two clustered tables, the cluster itself, the cluster index, and the tablespaces they are both stored in.

# **FIGURE 3.28** Index cluster and table relationship

![](img/832fbc6aca8b6075843ca6f2356c0a8d_225_0.png)

# **Hash Clusters**

*Hash clusters* are used in place of a traditional index to quickly find rows stored in a table. Like cluster indexes, the usefulness of Hash clusters is also limited to very specific situations. In general, Hash cluster tables should have these attributes:

-   - Have little or no DML activity performed on them after the initial load
-   - Have a uniform distribution of values in the indexed column
-   - Have a predictable number of values in the indexed column
-   - Be queried with SQL statements that utilize equality matches against the indexed column in their WHERE clauses

Rather than examine an index and then retrieve the rows from a table, a Hash cluster’s data is stored so queries against the cluster can use a hashing algorithm to determine directly where a row is stored with no intervening index required. In order to compare a Hash cluster and an index on a non–Hash cluster table, assume you issue the following query on the *EMPLOYEE* table:

```
SQL> SELECT *
2  FROM employee
3 WHERE emp_id = 100;
```

If the EMPLOYEE table were created as a non-Hash cluster table, a query like this would result in the following operations:

-   * Find the EMP_ID in the index on the EMP_ID column.
-   * Use the row ID value stored in the index to locate the row in the table.
-   * Read the row from the table, and return the information to the user.

This requires at least two I/Os to retrieve the row information, one (or more) on the index and one on the table. If, however, this table were created using a Hash cluster, then the query would involve these operations instead:

-   * The value in the WHERE clause (100) is passed through the same hashing algorithm that is used when inserting rows. This process occurs in memory and requires no I/O. The resulting value produced by the algorithm points directly to the location of the row in the table.
-   * The row is read, and the information is returned to the user.

In this case, only one I/O was required to retrieve the row, instead of the two or more with the traditional table/B-Tree index combination.

![](img/832fbc6aca8b6075843ca6f2356c0a8d_226_0.png)

Careful testing should be performed before implementing Index clusters and Hash clusters. Trying to apply them when the table data is not appropriate for their usage, or specifying their storage parameters incorrectly at cluster creation, can actually hinder performance instead of improve it.

# Comparing Physical Storage by Table Type

Now that you know of all the options available to the DBA for storing and accessing data, here is a brief recap comparing each of the physical table types with regard to how they actually store their rows. The list is from the least-ordered to the most-ordered structure:

-   * Heap Tables: Data is stored in the order in which the table's blocks are filled. As blocks come on and off the table's Freelist, the order in which the rows are stored becomes essentially random.
-   * Cluster Index: Related rows are stored together in related groupings, around the cluster key value. Between groupings there is no guarantee of the order of the data.
-   * Index-organized Table: Data is stored strictly in index order.

# **OLTP vs. DSS Tuning Requirements**

So far, you have examined the indexing techniques available to you for improving query execution. Now it is time to consider how the appropriateness of those options differs when considering the two primary types of database systems in use today: Online Transaction Processing Systems (OLTP) and Decision Support Systems (DSS).

# **Oracle Objective**

> List requirements for OLTP, DSS, and Hybrid Systems

# **Tuning OLTP Systems**

Online Transaction Processing (OLTP) systems tend to be accessed by large numbers of users doing short DML transactions. Order taking, inventory management, and scheduling systems are all examples of OLTP systems. Users of OLTP systems are primarily concerned with throughput: the total time it takes to place an order, remove an item from inventory, or schedule an appointment.

OLTP systems need enough B-Tree and Reverse Key indexes to meet performance goals but not so many as to slow down the performance of INSERT, UPDATE, and DELETE activity. Bitmap indexes are not a good choice for OLTP systems because of the locking issues they can cause.

Table and index statistics should be gathered regularly if the CBO is used because data volumes tend to change quickly in OLTP systems. OLTP indexes should also be rebuilt frequently if the data in the tables they are indexing is frequently modified.

# **Tuning DSS Systems**

Decision Support Systems (DSS) and data warehouses represent the other end of the tuning spectrum. These systems tend to have very little if any INSERT, UPDATE, and DELETE activity, except when data is mass loaded or purged at the end of the week, month, quarter, or year. Users of these systems are concerned with response time, which is the time it takes to get the results from their queries.

DSS makes heavy use of full table scans so the appropriate use of indexes and Hash clusters are important. Index-organized tables can also be important tuning options for large DSS systems. Bitmap indexes may be considered where the column data has low cardinality but is frequently used as the basis for queries. Thought should also be given to selecting the appropriate optimizer mode and gathering new statistics whenever data is loaded or purged. The use of histograms may also help improve DSS response time. Finally, consideration should be given to database block size, init. ora parameters related to sorting, and the possible use of the Oracle Parallel Query option.

As with OLTP systems, database statistics should also be gathered following each data load if the CBO is used.

# **Tuning Hybrid Systems: OLTP and DSS**

Some systems are a combination of both OLTP and DSS. These *hybrid* systems can present a significant challenge because the tuning options that help one type of system frequently hinder the other. However, through the careful use of indexing and resource management, some level of coexistence can usually be achieved. As the demands on each of these systems grows, you will probably ultimately have to split the two types of systems into two separate environments in order to meet the needs of both user communities.

# **Summary**

**U**nderstanding how to use TKPROF, Explain Plans, STATSPACK, and AUTOTRACE to analyze application SQL processing is important for every DBA. These tools allow you to understand not only how the application SQL is being executed, but also what resource costs are associated with those executions.

One major determinant of database performance is the extent to which the Oracle optimizer makes good SQL execution choices. These choices are influenced by the optimizer mode and the presence or absence of database statistics. These statistics can be gathered at the segment, schema, or database level. The statistics can also be moved between databases so that testing of optimizer behavior can be done with realistic data.

A variety of methods are available to improve application performance. These methods include stored outlines, materialized views, B-Tree indexes, Bitmap indexes, function-based indexes, compressed indexes, Reverse Key indexes, index organized tables, Index clusters, and Hash clusters. The appropriateness of these options varies with the type of system managed. OLTP systems have different indexing strategies than DSS environments.
