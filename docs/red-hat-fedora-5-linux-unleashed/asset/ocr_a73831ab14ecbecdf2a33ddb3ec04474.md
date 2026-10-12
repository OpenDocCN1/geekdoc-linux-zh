+   • r—Read only; it overwrites the file
+   • r+—Reading and writing; it overwrites the file
+   • w—Write only; it erases the existing contents and overwrites the file
+   • w+—Reading and writing; it erases the existing content and overwrites the file
+   • a—Write only; it appends to the file
+   • a+—Reading and writing; it appends to the file
+   • x—Write only, but only if the file does not exist
+   • a+—Reading and writing, but only if the file does not exist

Optionally, you can also add b (for example, a+b or rb) to switch to binary mode. This is recommended if you want your scripts and the files they write to work smoothly on other platforms.

When you call fopen(), you should store the return value. It is a resource known as a file handle, which the other file functions all need to do their jobs. The fread() function, for example, takes the file handle as its first parameter and the number of bytes to read as its second, returning the content in its return value. The fclose() function takes the file handle as its only parameter and frees up the file.

So, we can write a simple loop to open a file, read it piece by piece, print the pieces, and then close the handle:

```
<?php
    $file = fopen("filea.txt", "rb");
    while (!feof($file)) {
        $content = fread($file, 1024);
        echo $content;
    }
    fclose($file);
?>
```

That only leaves the fwrite() function, which takes the file handle as its first parameter and the string to write as its second. You can also provide an integer as the third parameter, specifying the number of bytes you want to write of the string, but if you exclude this, fwrite() writes the entire string.

If you recall, you can use a as the second parameter to fopen() to append data to a file. So, we can combine that with fwrite() to have a script that adds a line of text to a file each time it is executed:

```
<?php
    $file = fopen("filea.txt", "ab");
    fwrite($file, "Testing\n");
    fclose($file);
?>
```