# 15.4 What Is the Perl DBI?

The bind_param() method takes up to three arguments. The first argument represents the position of the parameter in the placeholder; so if the position is 1, then that would be represented by the first ? (placeholder) to be filled in with a value, and if the position is 2, that would be represented by the second ? and so on. The second argument to bind_param() is the actual value that will replace the ?; last is an optional parameter that hints as to the data type of the replacement value, (typically a number or string). The data type for a placeholder cannot be changed after the first bind_param() method call. However, it can be left unspecified, in which case it defaults to the previous value.

Two ways to handle the data type are either as an anonymous hash or as a DBI constant, like so:

```
$sth->bind_param(2, $value, { TYPE => SQL_INTEGER }); # Hash
$sth->bind_param(1, $value, SQL_INTEGER); # DBI Constant
```

# EXAMPLE 15.33

```
use DBI;
my $driver="DBI:mysql*";
my $database="sample_db";
my $user="root";
my $password="quizlegacy1";
my $host="localhost";

my $dbh = DBI->connect ("$driver:$database:$host", "$user",
"$password") or die "Can't connect: " . $DBI-erstr;
1 my $sth=$dbh->prepare("SELECT name, wins, losses FROM teams
where name LIKE ? "?) or die "Can't prepare sql statement: " .
$dbh->errstr;

2 $sth->bind_param(1, "Ch%");
3 $sth->execute();
4 $sth->dump_results();
$sth->finish();
$dbh->disconnect();

[Output]
'Cheyenne Chargers', '6', 14
'Chico Hardhats', '21', '25'
```

# EXPLANATION

+   1. A SQL statement is prepared with a placeholder to serve as a template for the query.
+   2. The bind_param() method takes two arguments: the position of the placeholder and the value (Ch%) that will be replace the ? in the query. Since there is only one parameter, the position is 1. If you had two parameters, the second one would be 2.
+   3. Since the parameters were bound to the statement with bind_param, the execute method does not require arguments.
+   4. The dump_results method is used to quickly output the results returned from the database after the query was executed.