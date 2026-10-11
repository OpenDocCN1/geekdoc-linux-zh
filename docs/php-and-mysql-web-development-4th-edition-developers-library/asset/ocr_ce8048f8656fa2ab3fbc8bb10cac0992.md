However, you must take care that the strings will be interpreted as you want. Consider these factors:

+   * The two types of quotes are not equivalent in Perl. Variable references are interpreted only within double quotes. Therefore, single quotes are not very useful when you want to construct statements by embedding variable references in the statement string. For example, if the value of `$var` is 14, the following two strings are not equivalent:
+     ```sql
+     "SELECT * FROM member WHERE member_id = $var"
+     'SELECT * FROM member WHERE member_id = $var'
+     ```
+     The resulting strings as Perl interprets them as follows:
+     ```sql
+     'SELECT * FROM member WHERE member_id = 14'
+     'SELECT * FROM member WHERE member_id = $var'
+     ```
+     Clearly, the first string is more like something you’d want to pass to the MySQL server. For the second, the server will interpret `$var` as the literal name of a column in the `member` table.

+   * Single quotes and double quotes are not always equivalent in MySQL. If the server is running with the `ANSI_QUOTES` SQL mode disabled, you can indeed use either type of quote to quote a string. But if `ANSI_QUOTES` is enabled, strings must be quoted with single quotes; double quotes can be used only for quoting identifiers such as database or table names. Consequently, it’s safest to quote strings with single quotes, because that works regardless of whether `ANSI_QUOTES` is on or off.

At the Perl level, an alternative to quoting strings with double quotes is to use the `qq()` construct, which tells Perl to treat everything between `qq(` and `)` as a double-quoted string. (Think of double–q as meaning “double-quote.”) For example, these two lines are equivalent:

```
```
$date = '2008-09-16';
$date = qq(2008-09-16);
```
```

When you use `qq()`, you can construct statements without thinking so much about quoting issues because you can use quote characters (single or double) freely within the statement string without having to escape them. In addition, variable references are interpreted. Both properties of `qq()` are illustrated by the following `INSERT` statement:

```
```
$id = 14;
$date = '2008-09-16';
$stmt = qq(INSERT INTO absence VALUES($id, '$date'));
```
```

You don’t have to use `‘` and `’` as the `qq` delimiters. Other forms, such as `qq( )` and `qq//,` will work, too, as long as the closing delimiter doesn’t occur within the string. I prefer `qq( )` because the `')` character is less likely than `’` or `'/` to occur within the text of the statement and be mistaken for the end of the statement string. For example, `’` occurs