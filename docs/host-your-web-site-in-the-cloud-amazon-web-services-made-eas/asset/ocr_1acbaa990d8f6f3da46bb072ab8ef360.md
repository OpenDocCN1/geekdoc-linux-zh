```
```php
sleep($sleep);
$sleep *= 2;
}
while(++$try < 6);
return false;
}
```
```

This version of our function will try up to six times to create a new object in a bucket. Each time it tries, the length of the pause (before the next try) doubles.

Our next function helps us determine a file's content type:

```
```php
// chapter_04/include/book.inc.php (excerpt)

function guessType($file)
{
    $info = pathinfo($file, PATHINFO_EXTENSION);
    switch (strtolower($info))
    {
        case "jpg":
        case "jpeg":
            return "image/jpg";
        case "png":
            return "image/png";
        case "gif":
            return "image/gif";
        case "htm":
        case "html":
            return "text/html";
        case "txt":
            return "text/plain";
        default:
            return "text/plain";
    }
}
```
```

Given a filename, this function uses the file's extension to make a very simple guess as to the content type of the file. There's no inspection of the file's content at all,