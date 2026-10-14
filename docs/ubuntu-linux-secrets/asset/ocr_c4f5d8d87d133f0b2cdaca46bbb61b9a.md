Both MySQL and PostgreSQL use the CREATE TABLE statement to create a new table in the database you’re currently connected to. The CREATE TABLE statement defines the data field names and the data type for the data, along with any special features required for the data:

```
test> create table test1(
test> employeeid int primary key,
test> lastname varchar(20),
test> firstname varchar(20),
test> datehired date);
NOTICE: CREATE TABLE / PRIMARY KEY will create implicit index "test1_pkey" for table "test1"
CREATE TABLE
test> \dt
List of relations
Schema | Name | Type | Owner
--------+-------+-------+------
public | test1 | table | rich
(1 row)
test>
```

PostgreSQL automatically creates an index file for the primary key data field. The \dt command displays the new table in the database.

# Adding and Viewing Data

Once you’ve created a table in the database, you can use it to store your data. Use the SQL INSERT statement to specify the data set for each individual data record:

```
test> insert into test1 values ('1234,'Blum,'Rich,'01/01/09');
INSERT 0 1
test> insert into test1 values ('1234,'Blum,'Barbara,'01/15/09');
ERROR: duplicate key value violates unique constraint "test1_pkey"
test> insert into test1 values ('1235,'Blum,'Barbara,'01/15/09');
INSERT 0 1
test>
```

Notice that PostgreSQL wouldn’t allow me to add another data record that used the same primary key value.

After your data are entered, you’ll want to be able to extract the information from the tables. The SQL SELECT statement provides the interface for doing that:

```
test> select employeeid from test1 where firstname ~ 'Rich';
 employeeid
------------
 1234
(1 row)

test>
```

The WHERE clause defines a filter expression to test against each data record in the table. The SELECT statement returns only the data records that match the filter.