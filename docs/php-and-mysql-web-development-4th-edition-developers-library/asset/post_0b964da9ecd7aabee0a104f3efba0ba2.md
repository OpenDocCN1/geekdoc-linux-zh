
## 8.2 Perl DBI Overview

Historical League’s member list in tab-delimited format. The format is not so interesting in itself. At this point, it’s more important see how to use DBI than to produce pretty output. `dump_members.pl` looks like this:

```perl
#!/usr/bin/perl
# dump_members.pl - dump Historical League's membership list

use strict;
use warnings;
use DBI;

# data source name, username, password, connection attributes
my $dsn = "DBI:mysql:sampdb:localhost";
my $user_name = "sampdm";
my $password = "secret";
my %conn_attrs = (RaiseError => 1, PrintError => 0, AutoCommit => 1);

# connect to database
my $dbh = DBI->connect ($dsn, $user_name, $password, \%conn_attrs);

# issue query
my $sth = $dbh->prepare ("SELECT last_name, first_name, suffix, email,"
. " street, city, state, zip, phone FROM member ORDER BY last_name");
$sth->execute ();

# read and display query result
while (my @ary = $sth->fetchrow_array ())
{
print join ("\t", @ary), "\n";
}
$sth->finish ();

$dbh->disconnect ();
```

To try the script for yourself, either use the copy that’s included in the `sampdb` distribution or create it using a text editor. If you use a word processor, be sure to save the script as plain text. Don’t save it in the word processor’s native format. You’ll probably need to change at least some of the connection parameters, such as the hostname, database name, username, or password. (That will be true for other scripts in this chapter that name the connection parameters as well.) Later, in Section 8.2.9, “Specifying Connection Parameters,” we’ll see how to get parameters from an option file instead of putting them directly in the script.

Now let’s go through the script a piece at a time. The first line contains the standard where-to-find-Perl indicator:

```perl
#!/usr/bin/perl
```

This line is part of every script we’ll discuss in this chapter; I won’t mention it further.

It’s a good idea to include in a script at least a minimal description of its purpose, so the next line is a comment to give anyone who looks at the script a clue about what it does:

```perl
# dump_members.pl - dump Historical League’s membership list
```

Text from a `#` character to the end of a line is considered a comment. It’s a useful practice to sprinkle comments throughout your scripts to explain how they work.

Next we have several use statements:

```perl
use strict;
use warnings;
use DBI;
```

`use strict` tells Perl to require you to declare variables before using them. You can write scripts without putting in a `use strict` line, but it’s useful for catching mistakes, so I recommend you always include it. For example, if you declare a variable `$my_var` but then later erroneously refer to it as `$mw_var`, the following message will appear when you run the script in strict mode:

```
Global symbol "$mw_var" requires explicit package name at line n
```

When you see that, you think, "Huh? I never used any variable named `$mw_var`!" Then you look at line n of your script, see that you misspelled `$my_var` as `$mw_var`, and fix it. Without strict mode, Perl won’t squawk about `$mw_var`; it simply creates a new variable by that name with a value of `undef` (undefined) and uses it without complaint. And you’re left to wonder why your script doesn’t work.

`use warnings` tells Perl to issue a warning if it finds that you use questionable language constructs or perform operations such as printing uninitialized variables. This is useful because it can alert you to code that should be rewritten.

`use DBI` tells the Perl interpreter that it needs to pull in the DBI module. Without this line, an error occurs as soon as you try to do anything DBI-related in the script. It’s unnecessary to indicate which DBD-level driver module to use; DBI activates the right one for you when you connect to your database.

Because we’re operating in strict mode, we must declare the variables the script uses, by means of the `my` keyword. Think of it as though the script is saying "I am explicitly indicating that these are my variables." The next section of the script sets up the variables that specify connection parameters, and then uses them to connect to the database:

```perl
# data source name, username, password, connection attributes
my $dsn = "DBI:mysql:sampdb:localhost";
my $user_name = "sampadm";
my $password = "secret";
my %conn_attrs = (RaiseError => 1, PrintError => 0, AutoCommit => 1);

# connect to database
my $dbh = DBI->connect ($dsn, $user_name, $password, \%conn_attrs);
```

The `connect()` call is invoked as `DBI->connect()` because it’s a method of the DBI class. You don’t really have to know what that means; it’s just a little object-oriented jargon to make your head hurt. (If you do want to know, it means that `connect()` is a function that “belongs” to `DBI`.) `connect()` takes several arguments:

- The data source, also known as the “data source name,” or “DSN.” The DSN indicates which DBD module to use and possibly other parameters.
- The username and password for your MySQL account.
- An optional argument indicating additional connection attributes. If it is given, this argument should be passed as a reference to a hash that specifies connection attribute names and values.

Data source formats are determined by the requirements of the particular DBD module you want to use. For the MySQL driver, allowable DSN formats include either of the following:

`DBI:mysql:db_name`
`DBI:mysql:db_name:hostname`

The capitalization of `dbi` doesn’t matter, but `mysql` must be lowercase. `db_name` represents the name of the database you want to use and `host_name` indicates the host where the server is running. If you omit the hostname, it defaults to `localhost` (Section 8.2.9, “Specifying Connection Parameters,” discusses other allowable data source formats.)

The connection-attribute hash that we’ve specified as the value for `connect_attrs` enables the `RaiseError` attribute and disables `PrintError`. These settings cause DBI to check for database-related errors and exit with an error message if it detects one. (That’s why you don’t see error-checking code anywhere in the `dump_members.pl` script; DBI handles it all.) Section 8.2.3, “Handling Errors,” covers alternative methods of responding to errors.

The attribute hash also enables the `AutoCommit` attribute. Currently, this is not strictly necessary, but it does make explicit that the script enables autocommit mode for transaction handling. The script doesn’t include any explicit transactions, but there is some possibility that DBI will in the future require scripts to specify the `AutoCommit` attribute explicitly. Doing so in scripts now ensures that they are ready if such a change does occur.

To specify the connection attributes, you could instead provide the hash reference directly in the call to `connect()`:

```perl
my $dbh = DBI->connect( $dsn, $user_name, $password,
 { RaiseError => 1, PrintError => 0, AutoCommit => 1 } );
```

Different people find one style or the other easier to read or edit, but operationally both approaches are the same.

If the `connect()` call succeeds, it returns a database handle, which we assign to `$dbh`. By default, `connect()` returns `undef` if it fails. However, because the script enables `RaiseError`, DBI will exit after displaying an error message if something goes wrong in the `connect()` call. (This is true for other DBI methods, too. I’ll describe what they return to indicate an error, but they won’t return at all if RaiseError is enabled.)

After connecting to the database, `dump_members.pl` issues a SELECT statement to retrieve the membership list, and then executes a loop to process each of the rows returned. These rows constitute the result set. To perform a SELECT, prepare the statement first, and then execute it:

```perl
# issue query
my $sth = $dbh->prepare ("SELECT last_name, first_name, suffix, email,"
. " street, city, state, zip, phone FROM member ORDER BY last_name");
$sth->execute ();
```

`prepare()` is invoked using the database handle; it passes the SQL statement to the driver for preprocessing before execution. Some drivers actually do something with the statement at this point. Others just remember it until you invoke `execute()` to cause the statement to be performed. The return value from `prepare()` is a statement handle, here assigned to `$sth`. The statement handle is used for all further processing related to the statement.

Notice that the statement string itself has no terminating semicolon. You no doubt have the habit of terminating SQL statements with a ';' character (developed through long hours of interaction with the `mysql` program). However, it’s best to break yourself of that habit when using DBI, because semicolons often cause statements to fail with syntax errors. The same applies to adding `\n` or `\G` to statement strings—don’t. Those statement terminators are conventions of `mysql` and are not used when issuing statements in DBI scripts. The end of the statement string implicitly terminates the statement and no explicit terminator is necessary.

When you invoke a method without passing it any arguments, you can leave off the parentheses. These two calls are equivalent:

```perl
$sth->execute ();
$sth->execute;
```

I prefer to include the parentheses because they make the call look less like a variable reference to me. Your preference may be different.

After you call `execute()`, the rows of the membership list are available for processing. In the `dump_members.pl` script, the row-fetching loop simply prints the contents of each row as a tab-delimited set of values:

```perl
# read and display query result
while (my @ary = $sth->fetchrow_array ())
{
print join ("\t", @ary), "\n";
}
$sth->finish ();
```
