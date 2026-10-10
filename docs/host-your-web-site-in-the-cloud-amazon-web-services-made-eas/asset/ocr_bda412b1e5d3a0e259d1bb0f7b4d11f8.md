```
```php
print(" Fetch image '$(imageURL)\n");
$image = file_get_contents($imageUrl);
print(" Retrieved " . strlen($image) . " byte image\n");

$imageThumb = thumbnailImage($image, 'image/png');

$key = 'image_' . md5($imageUrl) . '.png';

if (uploadObject($s3, BOOK_BUCKET, $key, $imageThumb))
{
    print( " Stored image in S3 using key '$(key)'\n");
    $$3ImageKeys[] = $key;
}
```
```

The above code uses the `file_get_contents` function to download the images, our `thumbnailImage` function to create the thumbnails, and our `uploadObject` function to upload the new image thumbnails to the S3 bucket.

The message is then passed along the pipeline in the usual fashion:

```
```php
																chapter 06/fetch_images.php (excerpt)
if (count($imageURLs) == count($$3ImageKeys))
{
    $origin    = $messageDetail['Origin'];
    $history   = $messageDetail['History'];
    $pageTitle = $messageDetail['PageTitle'];

    $history[] = 'Processed by ' . $argv[0] . ' at ' . date('c');

    $message = json_encode(array('Action'    => 'RenderImages',
                                 'Origin'    => $origin,
                                 'Data'      => $$3ImageKeys,
                                 'History'   => $history,
                                 'PageTitle' => $pageTitle));

    $res = $sqs->send_message(RENDER_QUEUE, $message);
    print(" Sent page to image renderer\n");

    if ($res->isOk())
    {
        $sqs->delete_message(IMAGE_QUEUE, $receiptHandle);
        print(" Deleted message from fetch queue\n");
```
```