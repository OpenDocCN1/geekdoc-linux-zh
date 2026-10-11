15.4 What Is the Perl DBI?

571

# 15.4.7 The ? Placeholder and Parameter Binding

Placeholders, represented by a ?, are used to optimize how queries are handled. Placeholders provide a template for a query and represent values that will be assigned to fields at a later time. They are used primarily with SELECT, INSERT, UPDATE, and DELETE statements. Values need to be “bound” to each placeholder before the statement can be executed. There are two ways to bind parameters: in the execute statement or with the bind_params method.

When a query is prepared by DBI, the database has to plan how it can best handle the query. The statement handle is used to store the prepared plan for the query, called the **execution plan**. Normally, once a query has been executed, the plan is discarded. When placeholders are used, instead of discarding the execution plan, the database accepts the placeholder in a template and makes a plan around it—making the template usable for future queries.

The ? represents values, such as *name* = ?, where *name* is a field name in the database table and its value will be supplied a value later on. (Remember, the ? represents a value, not a field name; for example, ? = "john" is wrong.)

**Binding Parameters in the execute Statement.** The execute method can take arguments representing the values of the placeholders, and those values are replaced in the prepared plan each time the method is called. DBI has to figure out the data type of the value. (Not all databases and DBI drivers support placeholders. See http://dev.mysql.com/doc/refman/5.7/en/sql-syntax-prepared-statements.html.)

In the following example, we will use a placeholder to be filled in later as an argument to the execute method.

EXAMPLE 15.30

```
use DBI;
my $driver = "DBI::mysql";
my $database = "sample_db";
my $user = "root";
my $host = "localhost";

my $dbh =
    DBI->connect( $driver:$database:$host;user=$user;
        password=quigley1" or die "Can't connect: " . DBI->errstr;

1 my $sth = $dbh->prepare( SELECT name, wins, losses FROM teams
          WHERE name = ?") or die "Can't prepare sql statement"
      . DBI->errstr;

    print "Enter the team name: ";
2 chomp( $team_name = <STDIN>);
```