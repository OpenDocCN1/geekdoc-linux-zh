In the simple example of the teams table, if the data is inserted for two teams, and the number of wins and losses for the two teams is accidentally swapped, an update would require both teams be modified, not just one. Suppose you are updating more than one table and the update statements in one table succeed and those in the other fail. A classic example is that you take money out of a savings account in one table and put it in a checking account in another table. The deposit succeeds but the withdrawal fails. The tables are then in an inconsistent state. A transaction is a set of SQL statements that succeed or fail all as a unit. For example, INSERT, UPDATE, and DELETE statements may be executed as a group. If one fails, then none of the statements is executed.

By default, the MySQL client runs with autocommit mode enabled. DBI also runs with autocommit mode on by default. This means that as soon as you execute any statement that modifies the data in a table, as long as no errors are returned, MySQL immediately commits the statement to the database, and any changes to the affected tables are made permanent.

To use transactions with MySQL, autocommit mode must be disabled. We can do that in a Perl script when connecting to the database by setting the hash value of AutoCommit => 0 as shown in the following example.

In the examples shown so far, we have connected to a database, the hash options available to the connect() method for error handling were used, PrintError and RaiseError. To use transactions, we need to turn off the AutoCommit attribute, turn RaiseError on, and optionally leave PrintError on or off (on being the default).

![](bbox=[0.03, 0.61, 0.97, 0.67])

```
1  my $dbh = DBI->connect( 'dbi:mysql:sample_db', 'root', 'quigley1',{
     PrintError => 0,
     RaiseError => 1,
     AutoCommit => 0
   });
```

RaiseError tells DBI to die with the $DBI::errstr message if there are errors, and PrintError (by default turned on) tells DBI to send a warning with the $DBI::errstr message and the program will continue to execute.

# 15.6.1 Commit and Rollback

Commit means in a transaction that a set of statements will be executed and sent to the database as a group. If all of the statements are successful, the group is committed and the database is modified. If, however, there is an error in any one of the statements in the group, a rollback command is issued, which returns all the tables back to their previous state.