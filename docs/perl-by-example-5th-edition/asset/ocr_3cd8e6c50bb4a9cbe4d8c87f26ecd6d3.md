Once the query has been sent to the database and a result set returned (reference to the result object), you can extract the data with special methods, such as `fetchrow_array()` and `fetchrow_hashref()`. These methods retrieve each record as a Perl array or a Perl hashref, respectively.

Finally, when you are done, the `finish()` method releases the result set returned from the `prepare()` method, and the `disconnect()` method ends the session by disconnecting from the database.

Now we will go through each of these five steps in detail.

# ### 15.4.4 Connecting to and Disconnecting from the Database

Once loaded, the DBI module is responsible for loading the appropriate driver for a given database. Then you will work with the database by using the methods provided by the module listed in the output shown from `perl`doc DBI. The first method we will use is the `connect()` method to get a connection to the database, and the last method, `disconnect()`, to break the connection.

The following example shows how to check for available database drivers for DBI.

```
EXAMPLE 15.22

```
1 use DBI;
2 my @drivers = DBI->available_drivers;
3 print join(" ", @drivers), "\n";
```

(Output for Windows)
DBM, ExampleP, File, Gofer, Proxy, SQLite, Sponge, mysql
```

**The `connect()` Method.** The `connect()` method establishes a connection to the specified database and returns an object called a database handle. You can make multiple connections to the same database or even to different databases in a program by using multiple `connect` statements. The `connect()` method takes several arguments:

```
```perl
"dbi:$driver:$database,$port,$username,$password" 
```
```

+   1.  The first argument is the DSN string (Data Source Name), the logical name for the database. Any attributes that define the data source are assigned to the DSN for retrieval by the driver. The DSN contains the name of the DBI module, `dbi`, followed by a colon and the database driver (MySQL, Sybase, Oracle), another colon and the name of the actual database for which the connection will be made, and/or the hostname (default is `localhost`), port, and so on, and is terminated with a semicolon.