```
$ssdb = new AmazonSDB();
$res = $ssdb->select($query);
: process the results...

?>
```

Now we can run arbitrary queries, like so:

```
$ php query_domain_cmd.php
```

The above command will retrieve all the records—the default action for this script.

We specify a query like so:

```
$ php query_domain_cmd.php "Size < '00000900'"
```

This command will find all files smaller than 900 bytes.

The special field itemName() can be used to refer to the item’s name in a select query:

```
$ php query_domain_cmd.php "itemName() like '%items%'"
```

The above command will retrieve items with names containing "items".

And finally, this command is used to retrieve items with the specified names:

```
$ php query_domain_cmd.php "itemName() in
➝('disable_mon.php', 'list_metrics.php')"
```

SimpleDB queries have the following general form:

```
select output_list
from domain_name
[where expression]
[order by clause]
[limit clause]
```