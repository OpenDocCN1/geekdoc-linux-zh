
The above script uses the select method to run a query that will return all items with a Name attribute containing the string *"items"*. It'll then loop through all the returned items and output their attributes and values. Here's an example of the output if the database contained file information about all the files in the **chapter_08** folder from the code archive:

```php
Sres = $sdb->select($query);
if (!$res->isOk())
{
    exit("Select operation failed\n");
}
foreach ($sres->body->SelectResult->Item as $Item)
{
    foreach ($Item->Attribute as $Attribute)
    {
        print($Attribute->Name . ": " . $Attribute->Value . ", ");
    }
    print("\n");
}
exit(0);
?>
```

```
$ php query_domain.php
Hash: a446a0c1d252042cf065e7bc4d743336, Name:
> augment_items.php, Size: 00001191,
Hash: 280434b0478b68eaceaf616329d337e, Name:
> batch_insert_items.php, Size: 00001337,
Hash: 49cb20ea103caeb654ce4aad307ecdc, Name:
> delete_items.php, Size: 00001003,
Hash: e77f57f95676ac156318123c44428c40, Name:
> insert_items.php, Size: 00000937,
```

By default, the select call returns 100 items (or 1MB worth, whichever is smaller) at a time. The limit clause can be used to request the return of up to 2,500 items, although this is still limited to 1MB.

If a select call has failed to return all the items due to these limits, a **NextToken** value will be included in the response. This can be passed to subsequent, repeated calls to select to receive additional results. Here's a hypothetical representation of a loop that takes advantage of the `NextToken` value to make repeated `select` calls until there are no more results returned:

```php
$next = null;
do
{
   $attrs = ($next == null) ? null : array('NextToken' => $next);
   $res   = $sdb->select($query, $attrs);
   $next  = (string) $res->body->SelectResult->NextToken;

   : Process results here...
}
while ($next != null);
```

We'll see more of this kind of loop in the remaining chapters.

## Advanced Queries

Let's alter the previous script so that the query comes from the command line by adding the following code:

```php
# chapter 08/query_domain_cmd.php (excerpt)
#!/usr/bin/php
<?php
error_reporting(E_ALL);

require_once('cloudfusion.class.php');
require_once('include/book.inc.php');

$query = "select * from " . BOOK_FILE_DOMAIN;

if ($argc > 1)
{
    $query .= " where ";

    for ($i = 1; $i < $argc; $i++)
    {
        $query .= ' ' . $argv[$i] . ' ';
    }
}

print("Final query: ${query}\n");

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
$ php query_domain_cmd.php "itemName() in ('disable_mon.php', 'list_metrics.php')"
```

SimpleDB queries have the following general form:

```
select output_list
from domain_name
[where expression]
[order by clause]
[limit clause]
```

Let's take a look at these. The `output_list` can be `*` for all attributes, `itemName()` for the name of the item, or a list of attribute names, or `count(*)` to retrieve an item count instead of items. The `domain_name` refers to the SimpleDB domain, of course.

The optional `where` expressions are a combination of attribute names, constant values, `itemName()`, and operators. The following table shows the operators that can be used in the `where` expression.

### Table 8.1. Available Operators

| Operator | Description |
| :--- | :--- |
| = | Equal to |
| != | Not equal to |
| > | Greater than |
| >= | Greater than or equal to |
| < | Less than |
| <= | Less than or equal to |
| and | Both conditions must be true |
| or | Either condition can be true |
| intersection | Returns results that appear in a pair of independent queries |
| like | Contains the specified constant, with "%" as a wildcard |
| not like | Does not contain the specified constant |
| between/and | In a specified range |
| in | Matches an item from a list |
| is null | Attribute does not exist |
| is not null | Attribute exists |
| every() | Every value of a multi-valued attribute satisfies the expression |

The optional `order` by clause can be used to order the results by a single attribute or item name. All sorts are performed in lexicographical order and the sort attribute must be mentioned by name in the associated expression. It's impossible to sort against null values.

The optional `limit` clause can be used to limit the number of results to a given value.

## Augmenting Items with Additional Data

Once an item has been created, additional calls to the put_attributes method can be used to create additional attributes or additional values for an existing attribute. Let's augment each item in the BOOK_FILE_DOMAIN with the file's modification time using this script:

```php
chapter_08/augment_items.php (excerpt)
#!/usr/bin/php
<?php

error_reporting(E_ALL);

require_once('cloudfusion.class.php');
require_once('include/book.inc.php');

$sdb = new AmazonSDB();
$res1 = $sdb->select("select Name from " . BOOK_FILE_DOMAIN);

if ($res1->isOK())
{
    foreach ($res1->body->SelectResult->Item as $item)
    {
        $itemName = $item->Name;
        $file     = $item->Attribute[0]->Value;

        $modTime = filemtime($file);
        if ($modTime != false)
        {
            $attrs = array('ModTime' => sprintf("%O10s", $modTime));

            $res2 = $sdb->put_attributes(BOOK_FILE_DOMAIN, $itemName, $attrs, false);

            if ($res2->isOK())
            {
                print("Updated item $itemName\n");
            }
            else
            {
                $error = $res2->body->Errors->Error->Message;
                print("Could not update item: $error}\n");
            }
        }
    }
}
else
{
    $error = $res1->body->Errors->Error->Message;
    exit("Could not run query: ${error}\n");
}
exit(0);
?>
```

It's as simple as calling the put_attributes method again for each item supplying the new attribute and value data.

This program illustrates another useful programming model. A SimpleDB query is used to obtain the list of items to be processed. Each item is processed in turn: the file name is extracted from the query results, the file's modification time is fetched, and the item is updated.

The code I just showed you took one slightly cheesy shortcut:

```php
$file = $item->Attribute[0]->Value;
```

The above line accesses the first returned attribute using a positional index. Code like this is fragile and hard to maintain. There's a better way to do this, and I'll show you what it is in just a minute.

## Storing Multiple Values for an Attribute

Storing multiple values for a single attribute is very easy; there are two ways to do this.

If you're storing the values one at a time and want them to accumulate over time, you can simply pass the value false for the replace parameter. You can store multiple modification times using the code from the last section, with repeated calls like so:

```php
$attrs = array('ModTime' => sprintf("%f10s", $modTime));
$res2 = $sdb->put_attributes(BOOK_FILE_DOMAIN, $itemName,
        $attrs, false);
```

You can store several values at the same time like this:

```php
$attrs2 = array('Flavors' => array('Vanilla', 'Chocolate'));  
$res2 = $sdb->put_attributes(BOOK_FILE_DOMAIN, $itemName,
                 $attrs2, false);
```

## Accessing Attribute Values

Let’s improve on the cheesy attribute access code above. Here’s a function to turn the array of SimpleXML nodes in the returned response into a PHP associative array:

```php
chapter_08/include/book.inc.php (excerpt)

function getItemAttributes($item)
{
  $attrs = array();

  foreach ($item->Attribute as $attribute)
  {
    $name = (string) $attribute->Name;
    $value = (string) $attribute->Value;

    if (isset($attrs[$name]))
    {
      if (is_array($attrs[$name]))
      {
        $attrs[$name][] = $value;
      }
      else
      {
        $attrs[$name] = array($attrs[$name], $value);
      }
    }
    else
    {
      $attrs[$name] = $value;
    }
  }
  return $attrs;
}
```
