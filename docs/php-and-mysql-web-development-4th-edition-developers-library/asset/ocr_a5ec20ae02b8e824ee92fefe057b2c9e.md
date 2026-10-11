The `connect()` call is invoked as `DBI->connect()` because it’s a method of the DBI class. You don’t really have to know what that means; it’s just a little object-oriented jargon to make your head hurt. (If you do want to know, it means that `connect()` is a function that “belongs” to `DBI`.) `connect()` takes several arguments:

+   - The data source, also known as the “data source name,” or “DSN.” The DSN indicates which DBD module to use and possibly other parameters.
+   - The username and password for your MySQL account.
+   - An optional argument indicating additional connection attributes. If it is given, this argument should be passed as a reference to a hash that specifies connection attribute names and values.

Data source formats are determined by the requirements of the particular DBD module you want to use. For the MySQL driver, allowable DSN formats include either of the following:

`DBI:mysql:db_name`
`DBI:mysql:db_name:hostname`

The capitalization of `dbi` doesn’t matter, but `mysql` must be lowercase. `db_name` represents the name of the database you want to use and `host_name` indicates the host where the server is running. If you omit the hostname, it defaults to `localhost` (Section 8.2.9, “Specifying Connection Parameters,” discusses other allowable data source formats.)

The connection-attribute hash that we’ve specified as the value for `connect_attrs` enables the `RaiseError` attribute and disables `PrintError`. These settings cause DBI to check for database-related errors and exit with an error message if it detects one. (That’s why you don’t see error-checking code anywhere in the `dump_members.pl` script; DBI handles it all.) Section 8.2.3, “Handling Errors,” covers alternative methods of responding to errors.

The attribute hash also enables the `AutoCommit` attribute. Currently, this is not strictly necessary, but it does make explicit that the script enables autocommit mode for transaction handling. The script doesn’t include any explicit transactions, but there is some possibility that DBI will in the future require scripts to specify the `AutoCommit` attribute explicitly. Doing so in scripts now ensures that they are ready if such a change does occur.

To specify the connection attributes, you could instead provide the hash reference directly in the call to `connect()`:

```
my $dbh = DBI->connect( $dsn, $user_name, $password,
 { RaiseError => 1, PrintError => 0, AutoCommit => 1 } );
```

Different people find one style or the other easier to read or edit, but operationally both approaches are the same.

If the `connect()` call succeeds, it returns a database handle, which we assign to `$dbh`. By default, `connect()` returns `undef` if it fails. However, because the script enables `RaiseError`, DBI will exit after displaying an error message if something goes wrong in