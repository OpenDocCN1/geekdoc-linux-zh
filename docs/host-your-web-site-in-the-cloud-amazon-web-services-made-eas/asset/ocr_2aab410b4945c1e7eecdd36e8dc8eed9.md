We'll use the PHP Simple HTML DOM Parser³ to parse the HTML. Download the file from the site and put it in your **include** folder. The script setup and loop outline look like this:

```
chapter_06/parse_page.php (excerpt)

```php
#!/usr/bin/php
<?php

error_reporting(E_ALL);

require_once('cloudfusion.class.php');
require_once('include/simple_html_dom.php');
require_once('include/book.inc.php');

$sqs = new AmazonSQS();
$s3 = new AmazonS3();

while (true)
{
    $message = pullMessage($sqs, $queueParse);

    if ($message != null)
    {
        : process the message...
    }
}
?>
```
```

Let's examine what happens inside the loop for each message pulled from the parse queue. The first step is to access the page from S3. The parser allows us to combine fetching and parsing, so this is really simple:

```
chapter_06/parse_page.php (excerpt)

```php
$messageDetail = $message['MessageDetail'];
$receiptHandle = (string)$message['ReceiptHandle'];
$pageURL       = $messageDetail['Data'];

print("Processing URL `${pageURL}`\n");
$dom = new simple_html_dom();
$dom->load_file($pageURL);
```
```

³ http://simplehtmldom.sourceforge.net/