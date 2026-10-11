**The `disconnect()` Method.** As you may remember from Chapter 10, “Getting a Handle on Files,” after we opened a file with a user-defined filehandle, we closed it with the built-in `close` function when finished. Unless lexically scoped, (three-part argument to `open`) if we forgot to close the file, it would be left up to the operating system to do so when the Perl script exited. The same thing is true when closing a database. After you are finished using the database, it is always a good idea to close the connection with the `disconnect` method. Of course, because the database handle is an object, Perl will automatically remove the reference to it once the program exits or the object goes out of scope. You would use the `disconnect` method, like so:

```
$dbh->disconnect();
```

# 15.4.5 Preparing a Statement Handle and Fetching Results

The SQL `select` statement is probably the statement used most when querying a database. When preparing a `select` statement for the database, the query is sent as a string argument to the DBI `prepare` method. The query is just as you would type it in the MySQL console but minus the semicolon. The database handle calls the `prepare` method. The database determines how it will execute the query (creates a “plan”), and DBI returns a statement handle containing the details on how the query will be executed. The statement handle (represented as `$sth`) encapsulates individual SQL statements to be executed within the database and calls the `execute` method.

This `execute` method tells the database to *perform* the SQL statement (execute its “plan”) and to return the results back to the program. An *undef* is returned if an error occurs. A successful execute always returns true regardless of the number of rows affected, even if zero rows were affected. The number of statement handles that can be created and executed is basically unlimited.

Even though you have executed the plan, you can’t see the results unless you use another DBI method to retrieve it, such as `dump_results()`, `fetchrow_array()`, or `fetch()`. 

Select, Execute, and Dump the Results. The DBI `dump_results` method gets all the rows from the statement handle object and prints the results in one simple statement. In the following example, we will connect to the database, prepare the query, execute the query, and print the results.

![](bbox=[0.05, 0.76, 0.95, 0.91])