tell fetchrow_hashref() to force column names into a particular lettercase by passing it a NAME_lc or NAME_uc attribute:

```
```
$hash_ref = $sth->fetchrow_hashref ('NAME_lc'); # use lowercase names
$hash_ref = $sth->fetchrow_hashref ('NAME_uc'); # use uppercase names
```
```

+   * The hash contains one element per unique column name. If you're performing a join that returns columns from multiple tables with overlapping names, you won't be able to access all the column values. If you issue the following statement, `fetchrow_hashref()` will return a hash having only one element, name:

```
`SELECT a.name, b.name FROM a INNER JOIN b WHERE a.name = b.name`
```

To avoid this problem, use aliases to make sure that each column has a distinct name. For example, if you rewrite the statement as follows, fetchrow_hashref() will return a reference to a hash with two elements, name and name2:

```
`SELECT a.name, b.name AS name2 FROM a INNER JOIN b WHERE a.name = b.name`
```

# **8.2.5.2 Determining the Number of Rows Returned by a Statement**

How can you tell the number of rows returned by a SELECT or SELECT-like statement? One way is to count the rows as you fetch them. In fact, this is the *only* portable way in DBI to know how many rows a SELECT statement returned. If you're using the MySQL driver, you can call the rows() method using the statement handle after invoking execute(). But this is not portable to other database systems, and the DBI documentation explicitly discourages using rows() for SELECT statements. Even for MySQL, if you've set the mysql_use_result attribute, rows() doesn't return the correct result until you've fetched all the rows. So you may as well just count the rows as you fetch them. (See Appendix H (online), for more information about mysql_use_result.)

# **8.2.5.3 Fetching Single-Row Results**

It's not necessary to run a loop to get your results if the result set consists of a single row. Suppose that you want to write a script, count_members.pl, that tells you the current number of Historical League members. The code to perform the statement looks like this:

```
```
# issue query
my $sth = $dbh->prepare ('SELECT COUNT(*) FROM member');
$sth->execute ();

# read and display query result
my $count = $sth->fetchrow_array ();
$sth->finish ();
$count = "can't tell" if !defined ($count);
print "$count\n";
```
```