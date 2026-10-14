
Using these two, we can write a script that reads all the text from one file, filea.txt, and writes it to another, fileb.txt:

```
<?php
    $text = file_get_contents("filea.txt");
    file_put_contents('fileb.txt', $text);
?>
```

Because PHP enables us to treat network sockets like files, we can also use file_get_contents() to read text from a website, like this:

```
<?php
    $text = file_get_contents("http://www.slashdot.org");
    file_put_contents('fileb.txt', $text);
?>
```

The problem with using file_get_contents() is that it loads the whole file into memory at once; that's not practical if you have large files or even smaller files being accessed by many users. An alternative is to load the file piece by piece, which can be accomplished through the following five functions: fopen(), fclose(), fread(), fwrite(), and feof(). The f in those function names stands for file, so they open, close, read from, and write to files and sockets. The last function, feof(), returns true if the end of the file has been reached.

The fopen() function takes a bit of learning to use properly, but on the surface it looks straightforward. Its first parameter is the filename you want to open, which is easy enough. However, the second parameter is where you specify how you want to work with the file, and you should specify one of the following:

- r—Read only; it overwrites the file
- r+—Reading and writing; it overwrites the file
- w—Write only; it erases the existing contents and overwrites the file
- w+—Reading and writing; it erases the existing content and overwrites the file
- a—Write only; it appends to the file
- a+—Reading and writing; it appends to the file
- x—Write only, but only if the file does not exist
- x+—Reading and writing, but only if the file does not exist

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

To make that script a little more exciting, we can stir in a new function, filesize(), that takes a filename (not a file handle, but an actual filename string) as its only parameter and returns the file's size in bytes. Using that new function brings the script to this:

```
<?php
$file = fopen("filea.txt", "ab");
fwrite($file, "The filesize was " . filesize("filea.txt") . "\n");
fclose($file);
?>
```

Although PHP automatically cleans up file handles for you, it is still best to use fclose() yourself so you are always in control.

## Miscellaneous

Several functions do not fall under the other categories and so are covered here. The first one is isset(), which takes one or more variables as its parameters and returns true if they have been set. It is important to note that a variable with a value set to something that would be evaluated to false—such as 0 or an empty string—still returns true from isset() because it does not check the value of the variable. It merely checks that it is set; hence, the name.

The unset() function also takes one or more variables as its parameters, simply deleting the variable and freeing up the memory. With these two, we can write a script that checks for the existence of a variable and, if it exists, deletes it (see Listing 25.5).

### LISTING 25.5 Setting and Unsetting Variables

```
<?php
$name = "Ildiko";
if (isset($name)) {
    echo "Name was set to $name\n";
    unset($name);
} else {
    echo "Name was not set";
}

if (isset($name)) {
    echo "Name was set to $name\n";
    unset($name);
} else {
    echo "Name was not set";
}
?>
```

That script runs the same isset() check twice, but it unset()s the variable after the first check. As such, it prints "Name was set to Ildiko" and then "Name was not set".

Perhaps the most frequently used function in PHP is exit, although purists will tell you that it is in fact a language construct rather than a function. exit terminates the processing of the script as soon as it is executed, meaning subsequent lines of code are not executed. That is really all there is to it; it barely deserves an example, but here is one just to make sure:

```
<?php
exit;
echo "Exit is a language construct!\n";
?>
```

That script prints nothing because the exit comes before the echo.
