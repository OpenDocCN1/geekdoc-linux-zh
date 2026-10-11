host where the server is running and the database to select as the default database. The DSN shown indicates that the MySQL server host and default database are localhost and sample. Both parameters following the colon are optional. The default value for host is localhost, so this parameter actually could have been omitted. If you omit dbname, no default database is selected. (The DSN can take other forms, and other parameters are allowed. For details, see Appendix I [online].)

Perhaps it makes you nervous that the username and password are embedded in the script for all to see. And, indeed, it should. It’s true that the name and password don’t appear in the resulting Web page that is sent to the client, because the script’s contents are replaced by its output. Nevertheless, if the Web server becomes misconfigured somehow and fails to recognize that your script needs to be processed by PHP, it will send the script as plain text, which exposes the connection parameters. We’ll deal with this problem in Section 9.1.2, “Using PHP Library Files for Code Encapsulation.”

The database handle returned by new PDO( ) becomes the means for further interaction with the MySQL server, such as issuing SQL statements to be executed. After a successful connection, the default error mode for PDO calls is to fail silently, which requires that you check for errors explicitly. To make it easier to handle problems, the script enables exceptions for PDO errors:

```
```
$dh->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
```
```

With exceptions enabled, a try/catch construct can be used to “route” errors to an exception handler without explicit tests. If you don’t use try/catch, exceptions terminate your script.

The script next sends the member-counting query to the server by invoking the database handle’s query( ) method, and then extracts and displays the result:

```
```
$sth = $dh->query (*'SELECT COUNT(*) FROM member'*);
$count = $sth->fetchColumn(0);
print (*"<p>The League currently has $count members.</p>"*);
```
```

The query( ) method sends the query to the server to be executed. Note that the query string contains no terminating semicolon character or \r or \n sequence, in contrast to the way you issue statements from within the mysql program. query( ) is used for statements that return rows. (Use a different method, exec( ), for statements that modify rows.) query( ) returns a PDOStatement object that is a statement handle for manipulating the result set.

For the query shown, the result set consists of a single row with a single column value representing the membership count. The script invokes the $sth object’s fetchColumn( ) method to fetch the row and extract the first column (column 0).

After printing the count, the script closes the connection to the server by setting the database handle to NULL. This is optional. If you don’t close the connection, PHP closes it when the script terminates.

The code for interacting with MySQL occurs within a try block so that any exception raised for an error can be caught and handled by the corresponding catch block.