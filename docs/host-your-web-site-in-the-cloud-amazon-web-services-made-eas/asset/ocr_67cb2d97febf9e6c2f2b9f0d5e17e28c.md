```
```
require_once('cloudfusion.class.php');
require_once('include/book.inc.php');

$usage = "DataTransfer-Out-Bytes";
```
```

I'll display outbound data transferred. This represents the number of bytes of S3 object data transferred from S3 to the outside world. Of course, feel free to replace the value in quotes with another type of usage such as DataTransfer-In-Bytes (the number of bytes of data transferred from the outside world to S3) or StorageObjectCount (the number of objects stored in the bucket), or even TimedStorage-ByteHrs (the number of byte-hours consumed by the data stored in the bucket).

By the way, a byte-hour is totally unrelated to the amount of time you spend in a dentist's chair. It represents the sum of the number of bytes stored multiplied by the number of hours they were stored. One of my buckets has a bytes-hour usage value of 14,597,270,160. This means that the bucket held about 608 megabytes for the 24-hour period starting August 18th, 2009.

The script will report on the usage for each S3 bucket, so we create the usual access objects and fetch the list of buckets:

```
```php
// chapter_10/bucket_usage_page.php (excerpt)
$S3   = new AmazonS3();
$Sdb  = new AmazonSDB();

$_buckets = $S3->get_bucket_list();
```
```

Now we need to do some date arithmetic. We'll report on the range of dates starting from the previous day and going back six days before that, or a full week's worth of data. The following code sets up $firstDay and $lastDay for a date range query, and also creates the $days array, with a year-month-day representation of each date in the range. Here we go: