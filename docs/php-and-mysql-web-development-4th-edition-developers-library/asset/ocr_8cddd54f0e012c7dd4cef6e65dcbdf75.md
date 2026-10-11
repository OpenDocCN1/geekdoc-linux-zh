After putting `html_begin()` and `html_end()` in `samppb_pdo.php`, the Historical League home page can be modified to use them. The resulting script (`index3.php`) looks like this:

```
```php
<?php
# USHL home page - version 3

require_once 'samppb_pdo.php';

$title = 'U.S. Historical League';
html_begin ($title, $title);
?>

<p>Welcome to the U.S. Historical League Web Site.</p>

<?php
try
{
    $dbh = sapph_connect ();
    $sth = $dbh->query ('SELECT COUNT(*) FROM member');
    $count = $sth->fetchColumn (0);
    print ("<p>The League currently has $count members.</p>");
    $dbh = NULL; # close connection
}
catch (PDOException $e) { } # empty handler (catch but ignore errors)

html_end ();
?>
```

```

Notice that the PHP code has been split into two pieces, with the literal HTML text of the welcome message appearing between the pieces. Copy `index3.php` to the `usht1` directory in your Web server’s document tree, naming it `index.php` to replace the file of that name that is there now.

The use of functions for generating the initial and final part of the page provides an important capability. If you want to change the look of your page headers or footers, just modify the functions appropriately, and every script that uses them will be affected automatically. For instance, you might want to put a message “Copyright USHL” at the bottom of each Historical League page. Adding the message to a page-trailer function such as `html_end()` is an easy way to do that.

# 9.1.3 A Simple Data-Retrieval Page

The script that we’ve embedded in the Historical League home page runs a query that returns just a single row (the member-ship count). Our next script shows how to process a multiple-row result set (the full contents of the `member` table). This is the PHP equivalent of the DBI script `dump_members_p1` developed in Section 8.2.2, “A Simple DBI Script,” so we’ll call it `dump_members.php`. The PHP version differs from the DBI version in that