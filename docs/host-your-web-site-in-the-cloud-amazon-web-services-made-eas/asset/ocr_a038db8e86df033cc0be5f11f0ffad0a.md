Here's what the returned data looks like:

```
```
Array
(
    [Hash] => c7158ad4d0961016fb3f531ccc90da5e
    [Size] => 00001535
    [Name] => query_domain_cmd.php
    [ModTime] => 1249514406
    [Flavors] => Array
    (
        [0] => Chocolate
        [1] => Vanilla
    )
)
```
```

# Deleting Attributes

If you've no more need for an attribute, you can use the delete_attributes method to delete it like this:

```
```
// chapter_08/delete_attrs.php (excerpt)
#!/usr/bin/php
<?php

error_reporting(E_ALL);
require_once('cloudfussion.class.php');
require_once('include/book.inc.php');

$ssdb = new AmazonSDB();

$attrs = array('ModTime', 'Flavor');

$res1 = $ssdb->select("select Name from " . BOOK_FILE_DOMAIN);
if ($res1->isOK())
{
    foreach ($res1->body->SelectResult->Item as $item)
    {
        $itemName = (string)$item->Name;

        $res2 = $ssdb->delete_attributes(BOOK_FILE_DOMAIN,
            $itemName, $attrs);
```
```