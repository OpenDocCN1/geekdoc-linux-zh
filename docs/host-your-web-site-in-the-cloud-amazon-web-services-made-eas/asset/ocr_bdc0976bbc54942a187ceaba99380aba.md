and the function expects the file extension to accurately reflect the contents. To serve its purpose for this chapter the function handles just a few types.

Putting it all together with some argument processing, looping, and error checking, we have a handy command to upload one or more files to S3:

```
```php
#!/usr/bin/php
<?php

error_reporting(E_ALL);

require_once('cloudfusion.class.php');
require_once('include/book.inc.php');

if ($argc < 3) {  // 1
	exit("Usage: " . $argv[0] . " bucket files...\n");
}

$bucket = ($argv[1] == '-' ? BOOK_BUCKET : $argv[1]);  // 2

$S3 = new AmazonS3();

for ($i = 2; $i < $argc; $i++) {  // 3
	$file		= Sargv[$i];
	$data		= file_get_contents($file);
	$contentType = guessType($file);

	if (uploadObject($S3, $bucket, $file, $data,	// 4
			S3_ACL_PUBLIC, $contentType))
	{
		print("Uploaded file '$file' to bucket '${bucket}'\n");
	}
	else
	{
		exit("Could not upload file '$file'"
			" to bucket '${bucket}'\n");
	}
}
```
```