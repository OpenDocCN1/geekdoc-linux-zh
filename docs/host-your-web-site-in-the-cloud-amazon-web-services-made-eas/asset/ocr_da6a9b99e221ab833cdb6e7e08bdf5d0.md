```
$thumbOut = thumbnailImage($imageOut, "image/jpeg");

$imageKey = $Key . '.jpg';
$thumbKey = $Key . '_thumb.jpg';

if (!uploadObject($S3, CL_BUCKET,
    $imageKey, $imageOut,
    S3_ACL_PUBLIC, "image/jpeg") ||
!uploadObject($S3, CL_BUCKET,
    $thumbKey, $thumbOut,
    S3_ACL_PUBLIC, "image/jpeg"))
{
    return false;
}

$imageURL = $S3->get_object_url(CL_BUCKET, $imageKey);
$thumbURL = $S3->get_object_url(CL_BUCKET, $thumbKey);
}
else
{
    $imageURL = null;
    $thumbURL = null;
}
```

We'll use the unique key we generated at the start of this function (in the variable `$Key`) for the SimpleDB item as the key for our images in S3 with a slight modification. We'll use `$Key . '.jpg'` for the full size image and `$Key . '_thumb.jpg'` for the thumbnail. This is convenient, but it means we're unable to handle more than one image per classified ad. That's fine for now; if we want to support more images per item in the future, it'll be easy to change.

The item description must also be stored in S3 (we'll use that `$Key` value again):

```
if (uploadObject($S3,
    CL_BUCKET,
    $Key,
    $description,
    S3_ACL_PUBLIC))
{
    $descriptionURL =
```