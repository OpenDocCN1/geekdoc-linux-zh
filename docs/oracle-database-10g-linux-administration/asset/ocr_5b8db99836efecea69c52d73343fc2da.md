# **Listing 17-2: An IOT example syntax**

```
```
CREATE TABLE emp_iot
(empno        number,
 ename       varchar2(20),
 salary      number(9,2) Not Null,
 comm        number,
 CONSTRAINT pk_emp_iot_index PRIMARY KEY (empno))
ORGANIZATION INDEX
tABLESPACE users
OVERFLOW TABLESPACE users_overflow
PCTTHRESHOLD 20 INCLUDING ename;
```
```

![](bbox=[0.04, 0.34, 0.14, 0.4])

> **NOTE**
> There is a distinct performance advantage when Oracle does not need to access the table, because all of the needed data items are in the index. IOTs came to be because all the required data items had to be stored in the b-tree index structure. Under such circumstances, why even have a table to maintain?

The advantage of an IOT is not having to store the data items twice if the table object doesn’t need to ever be referenced. Remember that Oracle will not go to the underlying table if the index satisfies the SQL statement’s request for data.

The objective with an IOT is to get as many rows into the index structure as possible. The more rows in the leaf blocks, the faster Oracle will be able to process the IOT structure on range scans.

IOTs are completely transparent to the application and are useful for reference tables or tables with a low number of columns. They can also be partitioned.

![](bbox=[0.04, 0.66, 0.14, 0.72])

> **TIP**
> I have used IOTs to reference long or blob columns, putting the key values in the index and letting the long datatype column go to the overflow tablespace.

+   · The overflow tablespace holds the less-frequently-accessed columns or, perhaps, holds a long column that the index key values make reference to. The USING clause in the IOT syntax is useful to tell Oracle which columns will be frequently accessed or used for access, and which columns are only needed when requested. For example, put the WHERE clause columns in the leaf block and put the SELECT columns in the overflow tablespace. The exception to this rule is an amount field that might have a sum function applied. This would fall into the frequently required field and should be in the leaf block as well.