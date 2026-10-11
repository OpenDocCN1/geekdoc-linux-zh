Alternatively, bind each value to its placeholder name before calling `execute()`:

```
`$stmt = "INSERT INTO member (last_name,first_name,expiration)\n         VALUES( :last_name, :first_name, :expiration)";\n$dbh = $dbh->prepare ($stmt);\n$dbh->bindValue (':last_name', 'O\'Malley');\n$dbh->bindValue (':first_name', 'Brian');\n$dbh->bindValue (':expiration', '2013-09-01');\n$dbh->execute ();`
```

One advantage of named placeholders is that it is easier to keep track of the association between placeholders and data values when there are large numbers of parameters.

# ## 9.1.8 Handling Errors

It’s essential to arrange to handle errors when you interact with MySQL. If you assume that every call will succeed, you’ll have a much more difficult time figuring out why your script doesn’t work when an error does occur.

When you attempt to connect to the database server by invoking `new PDO()`, an exception occurs if the attempt fails. Assuming that the attempt succeeds and you get back a valid database handle, PDO processes errors for subsequent operations that are based on that handle according to the PDO error mode. You can set the error mode as follows:

```
`$dbh->setAttribute (PDO::ATTR_ERRMODE, mode_value);`
```

PDO supports three error mode values:

+   - `PDO::ERRMODE_SILENT`: PDO does nothing other than set error information for the object that caused the error. This is the default error mode.
+   - `PDO::ERRMODE_WARNING`: This is similar to silent mode, but PDO emits a warning message in addition to setting the error information.
+   - `PDO::ERRMODE_EXCEPTION`: PDO raises an exception after setting the error information.

In all cases, if you know the object for which the error occurred, you can invoke its `errorCode()` or `errorInfo()` methods to obtain error information:

+   - `errorCode()` returns a five-character SQLSTATE value. A return value equal to `PDO::ERR_NONE` (“00000”) means “no error”.
+   - `errorInfo()` returns a three-element array containing the SQLSTATE value and a driver-specific code and message. For MySQL, the latter two values are a numeric error code and descriptive error message.

In silent or warning mode, error handling involves checking the result of each PDO operation that might fail. For example: