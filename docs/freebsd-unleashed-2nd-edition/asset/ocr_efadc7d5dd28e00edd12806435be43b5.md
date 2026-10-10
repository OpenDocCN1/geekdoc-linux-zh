Issue a query of any type to the database by using the `$dbb`->`query` method and setting it to a variable that acts as a handle to the results:

```
`$query = $dbb->query("SELECT Filename, Type FROM Pictures WHERE User_ID='5'");`
```

You can now use the `fetchrow` method to get the first row of the output. The way this works, you can keep calling `fetchrow` over and over (in a loop) until there is no more output; this is how you can apply the same Perl code to each line of output from the database, in whatever order your SQL query specifies:

```
```
while (@picdata = $query->fetchrow) {
  print "@picdata[0], @picdata[1]\n";
}
```
```

Here is a list of other operators that may be useful:

+   * `$dbb`->`quote`—Surround a variable with this operator to quote its contents properly in a query; for example, to ensure that a full name such as “Bob O' Shea” will be properly inserted without the apostrophe causing confusion in the query string, use `$dbb`->`query`("INSERT INTO Users (Fullname) VALUES ('.$dbb->`quote` ($fullname).')");.

+   * `$query`->`numrows`—This will return the number of rows that the query in `$query` will return.

+   * `$query`->`insertid`—If your query was an `INSERT` and the table had an `AUTO_INCREMENT` column that generated a new ID, this function will return that ID so you can use it for future queries.

To connect to PostgreSQL in Perl, you will need to install the /`usr`/`ports`/`databases`/`p5-Pg` port. This module provides much the same functionality as the p5-`Mysql` module does; you can set up a database connection with the following commands:

```
`use Pg;`
```

```
```
$Conn = Pg::setdbLogin(undef,undef,undef,undef,"PictureArchive", 
  "frank","frank's password");
```
```

Next, submit a query with the `$Conn`->`exec` method:

```
`$result = $Conn->exec("SELECT Filename,Type FROM Pictures WHERE User_ID='5'");`
```

Then use `$result`->`fetchrow` as in the MySQL example you saw previously in this chapter. All the possibilities for the `$result` handle can be found in the `perldoc` `Pg` documentation, in the section titled “2. Result.”