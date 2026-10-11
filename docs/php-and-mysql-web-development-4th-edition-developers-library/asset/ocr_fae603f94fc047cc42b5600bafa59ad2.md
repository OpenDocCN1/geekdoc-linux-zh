```
else if (!$sth->execute ())
    die ('Cannot execute statement: ' . $sth->errorCode () . "\n");
```

Note that $\textit{errorCode}()$ is invoked using the handle for which the error occurred. The same is true for $\textit{errorInfo}()$.

If you enable exceptions, PHP throws a \textit{PDOException} when an error occurs for a PDO operation. If no error occurs, the operation succeeded. Otherwise, the exception causes PHP to terminate your script unless you catch the error. To do so, put the code that might fail into a \textit{try} block and the error-processing code in the corresponding \textit{catch} block:

```
try
{
    # ... perform a database operation ...
}
catch (PDOException $e)
{
    # ... handle the error ...
}
```

The exception object ($\textit{e}$ in the example) has its own methods that provide error information:

+   - $\textit{getCode}()$ returns an error code.
+   - $\textit{getMessage}()$ returns a string containing an error message.

The following example enables exceptions and shows how to display error information when a statement fails to execute:

```
$dbh->setAttribute (PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
try
{
    $dbh->exec('DELETE FROM non_existent_table');
}
catch (PDOException $e)
{
    # Print error information from exception object
    print ('getCode value: ' . $e->getCode () . "\n");
    print ('getMessage value: ' . $e->getMessage () . "\n");
    # Print error information from database handle
    print ('errorCode value: ' . $dbh->errorCode () . "\n");
    print ('errorInfo value: ' . join ('.', $dbh->errorInfo ()) . "\n");
}
```

The example displays information from the exception object ($\textit{e}$), and also from the database-handle object ($\textit{dbh}$). That's possible here because the only PDO handle used in the \textit{try} block is \textit{dbh}. Were you using multiple handles in the \textit{try} block, you wouldn't know in the \textit{catch} block which of them caused the error, so you'd need to rely only on