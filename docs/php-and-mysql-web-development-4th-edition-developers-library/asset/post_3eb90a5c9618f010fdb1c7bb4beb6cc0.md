
However, you must take care that the strings will be interpreted as you want. Consider these factors:

- The two types of quotes are not equivalent in Perl. Variable references are interpreted only within double quotes. Therefore, single quotes are not very useful when you want to construct statements by embedding variable references in the statement string. For example, if the value of `$var` is 14, the following two strings are not equivalent:

  ```perl
  "SELECT * FROM member WHERE member_id = $var"
  'SELECT * FROM member WHERE member_id = $var'
  ```

  The resulting strings as Perl interprets them are as follows:

  ```perl
  'SELECT * FROM member WHERE member_id = 14'
  'SELECT * FROM member WHERE member_id = $var'
  ```

  Clearly, the first string is more like something you’d want to pass to the MySQL server. For the second, the server will interpret `$var` as the literal name of a column in the `member` table.

- Single quotes and double quotes are not always equivalent in MySQL. If the server is running with the `ANSI_QUOTES` SQL mode disabled, you can indeed use either type of quote to quote a string. But if `ANSI_QUOTES` is enabled, strings must be quoted with single quotes; double quotes can be used only for quoting identifiers such as database or table names. Consequently, it’s safest to quote strings with single quotes, because that works regardless of whether `ANSI_QUOTES` is on or off.

At the Perl level, an alternative to quoting strings with double quotes is to use the `qq()` construct, which tells Perl to treat everything between `qq(` and `)` as a double-quoted string. (Think of double-q as meaning “double-quote.”) For example, these two lines are equivalent:

```perl
$date = '2008-09-16';
$date = qq(2008-09-16);
```

When you use `qq()`, you can construct statements without thinking so much about quoting issues because you can use quote characters (single or double) freely within the statement string without having to escape them. In addition, variable references are interpreted. Both properties of `qq()` are illustrated by the following `INSERT` statement:

```perl
$id = 14;
$date = '2008-09-16';
$stmt = qq(INSERT INTO absence VALUES($id, '$date'));
```

You don’t have to use `(` and `)` as the `qq` delimiters. Other forms, such as `qq//` and `qq{} `, will work, too, as long as the closing delimiter doesn’t occur within the string. I prefer `qq( )` because the `')` character is less likely than `’` or `'/` to occur within the text of the statement and be mistaken for the end of the statement string. For example, `’` occurs within the `INSERT` statement just shown, so `qq()` would not be a useful construct for quoting the statement string.

## 8.2 Perl DBI Overview

The `qq()` construct can cross line boundaries, which is useful if you want to make the statement string stand out from the surrounding **Perl** code:

```perl
$id = 14;
$date = "2008-09-16";
$stmt = qq(
    INSERT INTO absence VALUES($id,'$date')
);
```

This is also useful if you simply want to format your statement on multiple lines to make it more readable. For example, the `SELECT` statement in the `dump_members.pl` script looks like this:

```perl
$sth = $dbh->prepare ("SELECT last_name, first_name, suffix, email,"
                    . " street, city, state, zip, phone FROM member ORDER BY last_name");
```

With `qq()`, it could be written like this instead:

```perl
$sth = $dbh->prepare (qq{
    SELECT
        last_name, first_name, suffix, email,
        street, city, state, zip, phone
    FROM member
    ORDER BY last_name
});
```

It’s true that double-quoted strings can cross line boundaries, too. But I find that `qq()` statements stand out better than two lone `"` characters and make the statement easier to read. This book uses both forms; see which you prefer.

The `qq()` construct takes care of quoting issues at the **Perl** lexical level so that you can use quotes in a string easily without having **Perl** complain about them. However, you must also think about **SQL**-level syntax. Consider this attempt to insert a row into the *member* table:

```perl
$last = "O'Malley";
$first = "Brian";
$expiration = "2013-09-01";
$rows = $dbh->do (qq{
    INSERT INTO member (last_name,first_name,expiration)
    VALUES('$last','$first',$expiration')
});
```

The resulting string that `do()` sends to **MySQL** looks like this:

```sql
INSERT INTO member (last_name,first_name,expiration)
VALUES('O'Malley','Brian','2013-09-01')
```

That is not legal SQL because for `'O'Malley'` a single quote occurs within a single-quoted string. We encountered this quoting problem earlier in Chapter 7. There we dealt with the issue by using the `mysql_real_escape_string()` function. DBI provides a similar mechanism: For each quoted value that you want to use literally in a statement, call the `quote()` method and use its return value instead. The preceding example is more properly written as follows:

```perl
$last = $dbh->quote ('O\'Malley');
$first = $dbh->quote ('Brian');
$expiration = $dbh->quote ('2013-09-01');
$rows = $dbh->do (qq{
    INSERT INTO member (last_name, first_name, expiration)
    VALUES ($last, $first, $expiration)
});
```

Now the string that `do()` sends to MySQL looks like this, with the quote that occurs within the quoted string properly escaped:

```sql
INSERT INTO member (last_name, first_name, expiration)
VALUES ('O\'Malley','Brian','2013-09-01')
```

Note that when you refer to `$last` and `$first` in the statement string, you do not add any surrounding quotes; the `quote()` method supplies them for you. If you add quotes yourself, your statement will have too many of them, as shown by the following example:

```perl
$value = 'paul';
$quoted_value = $dbh->quote ($value);
print "The quoted value is: $value\n";
print "The quoted value is: $quoted_value\n";
```

These statements produce the following output:

```text
The quoted value is: 'paul'
The quoted value is: ''paul''
```

In the second case, the string contains too many quotes.

### 8.2.7 Placeholders and Prepared Statements

In the preceding sections, we constructed statements by putting data values to be inserted or used as selection criteria directly into the statement string. It's not necessary to do this. DBI allows you to use special markers called 'placeholders' within a statement string, and then supply the values to be used in place of those markers when the statement is executed. This is called 'binding the values to the statement.' One reason for doing this is that you get the character-quoting benefits of the `quote()` method without having to invoke `quote()` explicitly. Another reason is improved performance: If you're executing a statement over and over within a loop, you can prepare it first and then execute it multiple times. This avoids the overhead of preparing the statement before each execution.

As an illustration of how placeholders work, suppose that you're beginning a new semester at school and you want to clear out the *student* table for your gradebook and then initialize it with the new students by using a list of student names contained in a file. Without placeholders, you can delete the existing table contents and load the new names like this:

```perl
$dbh->do (qq( DELETE FROM student ));    # delete existing rows
while (<>) {                              # read each input line,
                                          # use it to add a new row
    chomp;
    $s_ = $dbh->quote ($_);
    $dbh->do (qq( INSERT INTO student SET name = $s_ ));
}
```

This approach requires that you handle special characters in the data values yourself by calling *quote()*. It's also inefficient, because the basic form of the *INSERT* statement is the same each time, and *do()* calls *prepare()* and *execute()* each time through the loop. It's more efficient to call *prepare()* a single time to set up the *INSERT* before entering the loop and invoke only *execute()* within the loop. That avoids all invocations of *prepare()* but one. DBI allows this to be done as follows:

```perl
$dbh->do (qq( DELETE FROM student ));     # delete existing rows
my $sth = $dbh->prepare (qq( INSERT INTO student SET name = ? ));
while (<>) {                              # read each input line,
                                          # use it to add a new row
    chomp;
    $sth->execute ($_);
}
```

In general, if you find yourself calling *do()* inside a loop, it's better to invoke *prepare()* prior to the loop and *execute()* inside it. Note the '?' character in the *INSERT* statement. That's the placeholder. When *execute()* is invoked, you pass the value to be substituted for the placeholder when the statement is sent to the server. DBI automatically quotes special characters in the value, so there is no need to call *quote()*. Some things to note about placeholders:

- Do not enclose the placeholder character in quotes within the statement string. If you do, it will not be recognized as a placeholder.
- Do not use the *quote()* method to specify placeholder values, or you will get extra quotes in the values you're inserting.
- You can have more than one placeholder in a statement string, but be sure to pass as many values to *execute()* as there are placeholder markers.
