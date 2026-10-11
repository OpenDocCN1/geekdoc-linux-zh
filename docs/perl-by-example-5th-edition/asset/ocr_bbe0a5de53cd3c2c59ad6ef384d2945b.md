# chapter 
15

# Perl Connects 
with MySQL

By the time you finish this chapter, you should be able to read and write the following Perl code:

```
use DBI;
$dbh = DBI->connect('dbi:mysql:sample_db','root','letmein') or die
	"Connection Error: $DBI->errstr\n";
$sql = "select * from teams";
$sth = $dbh->prepare($sql);
$sth->execute or die "SQL Error: $sth->errstr\n";
while (@row = $sth->fetchrow_array) {
	print "@row\n";
}
$sth->finish;
$dbh->disconnect;
```

# 15.1 Introduction

The user has filled out a form and submitted it with a list of items he wants to purchase. Information for that user is stored in a database in a table called *customers*. You want to open the database and add the new order directly from your Perl program. And you may want to retrieve all the previous orders and product information for that customer and format the data for a Web page, or use it in an email message, or send it to a spreadsheet, all from your Perl program. This is all possible with Perl and the Perl DBI module, an object-oriented database interface that allows you to connect to any relational database and use Perl methods to perform all the necessary operations for opening and closing the database, as well as send SQL queries to create tables, update and delete them, retrieve and modify records, manage transactions, and display results.