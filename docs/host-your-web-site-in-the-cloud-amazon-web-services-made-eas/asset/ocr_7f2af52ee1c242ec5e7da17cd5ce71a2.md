Similarly, the usage data files for Amazon CloudFront use the `Resource` field to identify the account data associated with a particular CloudFront distribution. Because the data format contains common elements and some service-specific variants, Amazon SimpleDB makes an ideal storage system for it. We will need a domain:

```
```text
chapter_10/include/book.inc.php (excerpt)

define('BOOK_AWS_USAGE_DOMAIN', 'aws_usage');
```
```

We can use a modified version of the domain creation program from Chapter 8 to create this domain:

```
```text
chapter_10/create_domain.php (excerpt)

:::
$res = $sdb->create_domain(BOOK_AWS_USAGE_DOMAIN);
:::
```
```

Let's put together a program to import data from one or more CSV files specified on the command line. Here's what we need to start off:

```
```text
chapter_10/import_usage.php (excerpt)

#!/usr/bin/php
<?php

error_reporting(E_ALL);

require_once('cloudfusion.class.php');
require_once('include/book.inc.php');

if ($argc == 1)
{
    exit("Usage: " . $argv[0] . " CSV_FILE ...\n");
}
```
```

The script expects to find one or more CSV files on the command line and the code above performs this check. It then outputs a helpful message if there are too few command line arguments.