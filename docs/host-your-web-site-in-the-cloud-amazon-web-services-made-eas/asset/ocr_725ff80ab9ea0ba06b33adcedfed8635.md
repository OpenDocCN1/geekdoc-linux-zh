```
```
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
```

It's as simple as calling the put_attributes method again for each item supplying the new attribute and value data.

This program illustrates another useful programming model. A SimpleDB query is used to obtain the list of items to be processed. Each item is processed in turn: the file name is extracted from the query results, the file's modification time is fetched, and the item is updated.

The code I just showed you took one slightly cheesy shortcut:

```
```
$file = $item->Attribute[0]->Value;
```
```

The above line accesses the first returned attribute using a positional index. Code like this is fragile and hard to maintain. There's a better way to do this, and I'll show you what it is in just a minute.

# ## Storing Multiple Values for an Attribute

Storing multiple values for a single attribute is very easy; there are two ways to do this.

If you're storing the values one at a time and want them to accumulate over time, you can simply pass the value false for the replace parameter. You can store multiple modification times using the code from the last section, with repeated calls like so:

```
```
$attrs = array('ModTime' => sprintf("%f10s", $modTime));
$res2 = $sdb->put_attributes(BOOK_FILE_DOMAIN, $itemName,
        $attrs, false);
```
```