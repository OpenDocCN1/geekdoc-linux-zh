```
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

To make that script a little more exciting, we can stir in a new function, filesize(), that takes a filename (not a file handle, but an actual filename string) as its only parameter and returns the file's size in bytes. Using that new function brings the script to this:

```
<?php
$file = fopen("filea.txt", "ab");
fwrite($file, "The filesize was" . filesize("filea.txt") . "\n");
fclose($file);
?>
```

Although PHP automatically cleans up file handles for you, it is still best to use fclose() yourself so you are always in control.

# Miscellaneous

Several functions do not fall under the other categories and so are covered here. The first one is isset(), which takes one or more variables as its parameters and returns true if they have been set. It is important to note that a variable with a value set to something that would be evaluated to false—such as 0 or an empty string—still returns true from isset() because it does not check the value of the variable. It merely checks that it is set; hence, the name.

The unset() function also takes one or more variables as its parameters, simply deleting the variable and freeing up the memory. With these two, we can write a script that checks for the existence of a variable and, if it exists, deletes it (see Listing 31.9).