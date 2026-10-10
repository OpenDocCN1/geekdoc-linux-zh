```
print("Could not add item!\n");
}
?>
```

The add_item.php script allows us to add an item like so:

```
$ php add_item.php city state date price category
    "Title" "Description" [image_url]
```

We need to create one more Get function; this one retrieves the entire list of classified ads for a given city and state:

```
cloudlist/include/cloudfunctions.inc.php (excerpt)
function getItems($sdb, $city, $state)
{
    $query =
        "select * from " . CL_ITEM_DOMAIN .
        " where City=\"${city}\" and State=\"${state}\"";

    return runQuery($sdb, $query);
}
```

In the interests of testing and monitoring, we'll write a utility script to call all three of our Get functions. This allows us to verify that the rest of our application is working as desired:

```
cloudlist/dump.php (excerpt)
#!/usr/bin/php
<?php

error_reporting(E_ALL);

require_once('cloudfusion.class.php');
require_once('include/cloudfunctions.inc.php');

$sdb = new AmazonSDB();

print("Cities\n");
print("======\n");
$Cities = getCities($sdb);
print_r($Cities);
```