```
<span style="color:#888;font-size:0.9em">chapter_04/list_bucket_objects_page.php (excerpt)</span>
<?php
    error_reporting(E_ALL);

    require_once('cloudfusion.class.php');
    require_once('include/book.inc.php');

    $bucket = isset($_GET['bucket']) ? $_GET['bucket'] : BOOK_BUCKET; <span style='background:#1976D2;color:white;border-radius:50%;padding:2px 6px'>1</span>

    $S3 = new AmazonS3();

    $objects = getBucketObjects($S3, $bucket); <span style='background:#1976D2;color:white;border-radius:50%;padding:2px 6px'>2</span>

    $fileList = array();

    foreach ($objects as $object) <span style='background:#1976D2;color:white;border-radius:50%;padding:2px 6px'>3</span>
    {
        $key = $object->Key;
        $url = $S3->getObject_url($bucket, $key);
        $fileList[] = array('url' => $url, 'name' => $key,
        'size' => number_format((int)$object->Size)); <span style='background:#1976D2;color:white;border-radius:50%;padding:2px 6px'>4</span>
    }

    $output_title = "Chapter 3 Sample - List of S3 Objects in Bucket' .
    '${bucket}'];
    $output_message = "A simple HTML table displaying of all the' .
    'objects in the '${bucket}' bucket.";
    include 'include/list_bucket_objects.html.php'; <span style='background:#1976D2;color:white;border-radius:50%;padding:2px 6px'>5</span>

    exit(0);
?>
```

This code generates a web page and can accept an optional bucket argument in the URL query string. Let’s rip this one apart and see how it works:

+   <span style='background:#1976D2;color:white;border-radius:50%;padding:2px 6px'>1</span> This code checks to see if the bucket argument was supplied. If it was, then it’s used as the value of $bucket. Otherwise, the default value, the BOOK_BUCKET constant, is used.

+   <span style='background:#1976D2;color:white;border-radius:50%;padding:2px 6px'>2</span> Here we call our custom getBucketObjects function that fetches the list of objects in the given bucket and stores them in the $objects array.