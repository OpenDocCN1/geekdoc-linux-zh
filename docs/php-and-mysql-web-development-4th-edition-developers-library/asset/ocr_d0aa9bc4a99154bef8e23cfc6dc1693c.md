# 1.3.3 PDOException Object Methods

By default, PDO throws an exception only for the PDO constructor (that is, when you call `new PDO()` to connect to a database server), and other PDO methods indicate failure by their return value. If you enable PDO exceptions after connecting, the PDO extension instead throws exceptions when its methods fail. PDOException objects contain the error information provided as a result of such exceptions.

To enable PDO exceptions, use the database handle:

```
$dbh->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
```

PDO supports three error mode values:

+   - `PDO::ERRMODE_SILENT`: PDO does nothing other than set the error information. This is the default error mode.

+   - `PDO::ERRMODE_WARNING`: This is similar to silent mode, but PDO emits a warning message in addition to setting the error information.

+   - `PDO::ERRMODE_EXCEPTION`: PDO raises an exception after setting the error information.

If exceptions are enabled, the error information becomes available when an error occurs via the `getCode()` and `getMessage()` methods of the exception object.

Exceptions terminate your script by default. To handle them yourself, use `try` and `catch`. In the catch block, you can access the exception's methods that return error information:

```
```
try
{
    $sth = $dbh->query ("SELECT * FROM no_such_table");
}
catch (PDOException $e)
{
    print ("getCode value: " . $e->getCode() . "\n");
    print ("getMessage value: " . $e->getMessage() . "\n");
}
```
```

+   - `integer` getCode (void)

Returns a five-character SQLSTATE value containing the error code. A return value equal to `PDO::ERR_NONE ("00000")` means "no error."

+   - `string` getMessage (void)

Returns a string containing the error message.