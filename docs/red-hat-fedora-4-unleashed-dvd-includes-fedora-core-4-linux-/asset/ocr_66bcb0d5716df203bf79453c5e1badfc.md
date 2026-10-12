# LISTING 31.8 Browsing Arrays with the Array Cursor

```
<?
php
$array = array("first\n", "second\n", "third\n", "fourth\n", "fifth\n");
echo current($array);
echo next($array);
echo next($array);
echo end($array);
echo prev($array);
echo reset($array);
?>
```

That outputs the following:

+   first  
+   second  
+   third  
+   fifth  
+   fourth  
+   first

The array cursor is frequently used when the foreach loop is impractical, which is quite rare.

# Files

As you will have learned from elsewhere in the book, the UNIX philosophy is that everything is a file. In PHP, this is also the case: A selection of basic file functions is suitable for opening and manipulating files, but those same functions can also be used for opening and manipulating network sockets. We cover both here.

Two basic read and write functions for files make performing these basic operations easy. They are file_get_contents(), which takes a filename as its only parameter and returns the file’s contents as a string, and file_put_contents(), which takes a filename as its first parameter and the data to write as its second parameter.

Using these two, we can write a script that reads all the text from one file, filea.txt, and writes it to another, fileb.txt:

```
<?
php
$text = file_get_contents("filea.txt");
file_put_contents("fileb.txt", $text);
?>
```

Because PHP enables us to treat network sockets like files, we can also use file_get_contents() to read text from a website, like this: