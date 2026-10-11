```
```
# put out initial part of page
my $title = "$db_name Database Browser";
print header ();
print start_html (-title => $title, -bgcolor => "white");
print h1 ($title);

# parameters to look for in URL
my $tbl_name = param ("tbl_name");
my $sort_col = param ("sort_col");
```

```

```
```
# If $tbl_name has no value, display a clickable list of tables.
# Otherwise, display contents of the given table. $sort_col, if
# set, indicates which column to sort by.

if (!defined ($tbl_name))
{
    display_table_names ($dbh, $db_name)
}
else
{
    display_table_contents ($dbh, $db_name, $tbl_name, $sort_col);
}

print end_html ();
```

```

It's easy to find out what value a parameter has because CGI.pm does all the work of finding out what information the Web server passes to the script. We need only call param() with the name of the parameter in which we're interested. In the main body of db_browse.pl, that parameter is named tbl_name. If it's not set, this is the initial invocation of the script and it displays the table list. Otherwise, it displays the contents of the table named by the tbl_name parameter, sorted by the column named in the sort_col parameter.

The display_table_names() function generates the initial page. display_table_names() retrieves the table list and writes out a bullet list in which each item is the name of a table in the same database:

```
```
sub display_table_names
(
my ($dbh, $db_name) = @_;

    print p ("Select a table by clicking on its name:");

    # retrieve reference to single-column array of table names
    my $sth = $dbh->prepare (qq
    SELECT TABLE_NAME FROM INFORMATION_SCHEMA.TABLES
    WHERE TABLE_SCHEMA = ? ORDER BY TABLE_NAME
```

```