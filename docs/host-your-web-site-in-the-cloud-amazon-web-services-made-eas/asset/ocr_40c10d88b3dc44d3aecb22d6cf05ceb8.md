Let's take a look at this code:

+   First, we instantiate new **AmazonS3** and **AmazonCloudFront** objects.

+   Here we determine whether there's a CloudFront distribution for each of our buckets.

+   Once again we use our **getBucketObjects** function to retrieve all the objects from our two buckets.

+   We iterate through all the objects in our thumb bucket, and populate the **$thumbs** array using the object keys as array keys and storing their URLs.

+   If there's a CloudFront distribution for our thumbnails, we use its URL; otherwise, we use the standard S3 URL.

+   We do the same operation for all the objects in the specified bucket; this is stored in the **$fileList** array and will be used in the HTML output.

+   This is a new addition from the **list_bucket_objects_page.php** script to the **$fileList** array. The thumbnail URL is saved if there's a matching thumbnail, otherwise an empty string is stored.

Here's the HTML template that generates the output: