```
```
foreach (SobjectThumbs as SobjectThumb)
{
    $key = (string) SobjectThumb->Key;

    if ($thumbsDist != null)  5
    {
        $thumbs[$key] = 'http://' . $thumbsDist->DomainName
            . '/' . $key;
    }
    else
    {
        $thumbs[$key] = $s3->get_object_url($bucketThumbs, $key);
    }
}

$fileList = array();  6
foreach (Sobjects as Sobject)
{
    $key = (string) Sobject->Key;

    if ($dist != null)
    {
        $url = 'http://' . $dist->DomainName . '/' . $key;
    }
    else
    {
        $url = $s3->get_object_url($bucket, $key);
    }

    $thumbURL = IsSet($thumbs[$key]) ? $thumbs[$key] : '';  7
    $fileList[] = array('thumb' => $thumbURL, 'url' => $url,
        'name' => $key, 'size' => number_format((int)$object->Size));
}

Soutput_title = "Chapter 3 Sample - List of S3 Objects in Bucket"
    . "${bucket}";
Soutput_message = "A simple HTML table displaying of all the objects"
    . "in the ${bucket}" bucket with thumbnails.";

include 'include/list_bucket_objects_thumbs.html.php';

exit(0);
?>
```
```