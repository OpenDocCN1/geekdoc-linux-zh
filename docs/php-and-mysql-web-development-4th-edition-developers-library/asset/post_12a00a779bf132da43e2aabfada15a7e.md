
`fetchrow_array()` returns an array containing the column values of the current row, or an empty array when there are no more rows. Thus, the loop fetches successive rows returned by the `SELECT` statement and prints each one with tabs between column values.

`NULL` values in the database are returned as `undef` values to the Perl script, but these print as empty strings, not as the word “`NULL`.” `undef` column values also have another effect when you run the script; they result in warnings like this from the Perl interpreter:

```
Use of uninitialized value in join at dump_members.pl line `n`.
```

These warnings are triggered by the inclusion of the `use warnings` statement. If you remove the statement and run the script again, the warnings will go away. However, warnings mode is useful for discovering problems (such as printing uninitialized variables), so a better way to eliminate the warnings is to detect and deal with `undef` values. Section 8.2.5, “Handling Statements That Return a Result Set,” discusses some techniques for doing so.

In the `print` statement, note that the tab and newline characters (represented as the `\t` and `\n` sequences, respectively) are enclosed in double quotes. In Perl, escape sequences are interpreted only when they occur within double quotes, not within single quotes. If single quotes had been used, the output would be full of literal instances of `\t` and `\n`.

After the row-fetching loop terminates, the call to `finish()` indicates that the statement handle is no longer needed and that any temporary resources allocated to it can be freed. In this script, the call to `finish()` is for illustrative purposes only. It need not actually be invoked here, because the row-fetching call will do so automatically when it encounters the end of the result set. `finish()` is more useful in situations where you `fetch` only part of the result set and do not reach its end (for example, if you `fetch` only the first row). Examples from this point on do not use `finish()` unless it’s necessary.

Having printed the membership list, we’re done, so we can disconnect from the server before exiting:

```
$dbh->disconnect();
```

`dump_members.pl` illustrates a number of concepts that are common to most DBI programs, and at this point you could probably start writing your own DBI programs without knowing anything more. For example, to write out the contents of some other table, all you’d need to do is change the text of the `SELECT` statement that is passed to the `prepare()` method. And in fact, if you want to see some applications of this technique, you can skip ahead immediately to the part of Section 8.3, “Putting DBI to Work,” that discusses how to generate the member list for the Historical League’s annual meeting program and the League’s printed directory. However, DBI provides many other useful capabilities. The next sections cover some of these in more detail so that you can see how to do more than run simple `SELECT` statements in your Perl scripts.

## 8.2.3 Handling Errors

dump\_members.pl turned on the RaiseError error-handling attribute when it invoked the connect() method so that errors would automatically terminate the script with an error message rather than just returning error codes. It’s possible to handle errors in other ways. For example, you can check for errors yourself rather than having DBI do it. To see how to control DBI’s error-handling behavior, let’s take a closer look at the connection attribute hash passed as the final argument to connect():

```
# data source name, username, password, connection attributes
my $dsn = "DBI:mysql:sampdb:localhost";
my $user_name = "sampur";
my $password = "secret";
my $conn_attrs = {RaiseError => 1, PrintError => 0, AutoCommit => 1};

# connect to database
my $dbh = DBI->connect ($dsn, $user_name, $password, \%conn_attrs);
```

The two attributes relevant for error handling are RaiseError and PrintError:

- If RaiseError is enabled (set to a non-zero value), DBI raises an exception when an error occurs in a DBI method. By default, this results in a call to die() to print a message and exit the script.
- If PrintError is enabled, DBI calls warn() to print a message when a DBI error occurs, but the script continues executing.

By default, RaiseError is disabled and PrintError is enabled. In this case, if the connect() call fails, DBI prints a message but continues executing. Thus, with the default error-handling behavior that you get if you omit the fourth argument to connect(), you might check for errors like this:

```
my $dbh = DBI->connect ($dsn, $user_name, $password) or exit (1);
```

In this case, if an error occurs, connect() returns undef to indicate failure, and that triggers the call to exit(). You need not print an error message because DBI already will have printed one.

If you were to explicitly specify the default values for the error-checking attributes, the settings passed to connect() would look like this:

```
my $conn_attrs = {RaiseError => 0, PrintError => 1, AutoCommit => 1};
my $dbh = DBI->connect ($dsn, $user_name, $password, \%conn_attrs)
    or exit (1);
```

That’s more work to write out, but it’s also more obvious to the casual reader what the error-handling behavior is.

To check for errors yourself and print your own messages, disable both `RaiseError` and `PrintError`:

```
my %conn_attrs = {RaiseError => 0, PrintError => 0, AutoCommit => 1};
my $dbh = DBI->connect ($dsn, $user_name, $password, \%conn_attrs);
or die "Could not connect to server: $DBI::err ($DBI::errstr)\n";
```

The `$DBI::err` and `$DBI::errstr` variables used in the code just shown are useful for constructing error messages. They contain the MySQL error code and error string, much like the `mysql_errno()` and `mysql_error()` C API functions. If no error occurred, `$DBI::err` will be 0 or undef, and `$DBI::errstr` will be the empty string or undef. (In other words, both variables will be false.)

If you want DBI to handle errors for you so that you don't have to check for them yourself, enable `RaiseError` and disable `PrintError`:

```
my %conn_attrs = {RaiseError => 1, PrintError => 0, AutoCommit => 1};
my $dbh = DBI->connect ($dsn, $user_name, $password, \%conn_attrs);
```

This is by far the easiest approach, and it is how almost all scripts presented in this chapter are written. The reason for disabling `PrintError` when enabling `RaiseError` is to prevent the possibility of having error messages being printed twice. (If both attributes are enabled, the DBI handlers for both might be called under some circumstances.)

Enabling `RaiseError` may not be appropriate if you want to execute some sort of cleanup code of your own when the script exits, although in this case you might be able to do what you want by redefining the `SIG(__DIE__)` signal handler. Another reason you might want to avoid enabling the `RaiseError` attribute is that DBI prints technical information in its messages, like this:

```
disconnect (DBI::db:HASH(0x197aae4)) invalidates 1 active statement. Either destroy statement handles or call finish on them before disconnecting.
```

That's useful information for a programmer, but it could be the kind of thing you want to avoid presenting to the everyday user. In that case, it can be better to check for errors yourself so that you can display messages that are more meaningful to the people you expect to be using the script. Or you might consider redefining the `SIG(__DIE__)` handler here, too. That could be useful because you can enable `RaiseError` to simplify error handling, but replace the default error messages that DBI presents with your own messages. To provide your own `__DIE__` handler, do something like the following before executing any DBI calls:

```
$SIG(__DIE__) = sub { die "Sorry, an error occurred\n"; };
```

You can also define a subroutine in the usual fashion and set the signal handler value using a reference to the subroutine:

```
sub die_handler
{
    die "Sorry, an error occurred\n";
}
```
