```
3  $sth->execute();
    print qq(\n\nContents of "coaches" table\n or
    die "Couldn't execute statement" . $sth->errstr;

4  $sth->dump_results(); # Display results of the execute

5  $sth->finish();
6  $dbh->disconnect();
```

(Output)

Contents of "coaches" table

'1', 'John Doe', 'Chico Hardheads', 'Head Coach', '2002-12-10'
'2', 'Jack Watson', 'Cardinals', 'Offensive Coach', '2004-10-05'
'3', 'Bud Wilkins', 'Premont Tigers', 'Head Coach', '1999-09-06'
'4', 'Joe Hayes', 'Premont Tigers', 'Defensive Coach', '1998-06-16'
'5', 'George Jones', 'Bangor Rams', 'Offensive Coach', '2003-09-03'
'6', 'Jerry O'Connell', 'Portland Penguins', 'Head Coach', '2006-02-22'
6 rows

+   EXPLANATION
+   1  A connection is made to the MySQL database called sample_db and a database handle is returned called $dbh. It is the object that represents the connection. Now we have access to the database.
+   2  The prepare method is used to prepare the SQL query. It returns a statement handle, an object that encapsulates the query and prepares it for execution: (Note that the SQL statement does NOT end with a semicolon.)
+   3  The execute method causes the query to actually be executed. Now we are ready to retrieve the results of the query.
+   4  The dump_results method is called on the statement handle and prints the results of the query.

Select, Execute, and Fetch a Row As an Array. When the fetchrow_array() method is called, the database will return the first row of results as an array, where each field is an element in the array. Each successive call to the fetchrow_array() method yields the next row of results, until there are no more results and the call yields a value of undef.

In the following example, we will connect to the database, prepare the query, execute the query, and fetch the data with the fetchrow_array() method. As in this example, we can use a while or for loop to fetch all the rows. (An important point to remember is that when the fields are fetched, they are assigned in the order they were listed in the SQL query.)