+   Flashback Transaction Query
+   Flashback Table
+   Flashback Drop
+   Flashback Database

This can be a very powerful tool when used correctly, and can save you hours of restoration and recovery time.

# Flashback Query

The flashback query feature allows you to query the database regarding how it looked at some point in the past. It's run by using the AS OF clause. The AS OF clause can take either a timestamp or an SCN, as shown next:

```
SELECT * FROM scott.emp AS OF TIMESTAMP
  TO_TIMESTAMP('2004-05-16 08:00:00', 'YYYY-MM-DD HH:MI:SS')
  WHERE ename = 'SCOTT';
```

You can actually reset the data in question to its past value by using the flashback query within an insert statement. Keep in mind, however, that if this record still exists in the database, you may be unable to insert the data due to a unique constraint.

```
INSERT INTO scott.emp
  (SELECT * FROM scott.emp AS OF TIMESTAMP
   TO_TIMESTAMP('2004-05-16 08:00:00', 'YYYY-MM-DD HH:MI:SS')
   WHERE ename = 'SCOTT');
```

The flashback query feature can help you avoid the situation where you have to restore a table to a secondary system in order to restore data that a user has inadvertently changed or dropped. This feature lets you restore a table, a set of tables, or a particular row in a table that has been mistakenly changed or deleted, and allows you to do this without having to go through a full media restore (assuming the data is still available in the UNDO tablespace).

# The Flashback Version Query

By selecting flashback data as part of your query and using the VERSIONS BETWEEN clause, you are able to view changes that have occurred to a particular record or set of records in the database. In the following example, I have selected a timeframe where I have changed the salary for employee Miller in the scott.emp table. The following SQL script called fversion.sql is used to display this data.

```
set linesize 256
set pagesize 100
```