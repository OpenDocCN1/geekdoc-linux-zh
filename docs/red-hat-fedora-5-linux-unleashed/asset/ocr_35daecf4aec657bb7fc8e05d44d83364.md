To make that script a little more exciting, we can stir in a new function, filesize(), that takes a filename (not a file handle, but an actual filename string) as its only parameter and returns the file’s size in bytes. Using that new function brings the script to this:

```
`<?php
$file = fopen("filem.txt", "rb");
fprintf($file, "The filesize was" . filesize("filem.txt") . "\n");
fclose($file);
?>`
```

Although PHP automatically cleans up file handles for you, it is still best to use fclose() yourself so that you are always in control.

# Miscellaneous

Several functions do not fall under the other categories and so are covered here. The first one is isset(), which takes one or more variables as its parameters and returns true if they have been set. It is important to note that a variable with a value set to something that would be evaluated to false—such as 0 or an empty string—still returns true from isset() because it does not check the value of the variable. It merely checks that it is set; hence, the name.

The unset() function also takes one or more variables as its parameters, simply deleting the variable and freeing up the memory. With these two, we can write a script that checks for the existence of a variable and, if it exists, deletes it (see Listing 32.5).

# **LISTING 32.5** Setting and Unsetting Variables

```
`<?php
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
?>`
```

That script runs the same isset() check twice, but it unset()s the variable after the first check. As such, it prints “Name was set to Ildiko” and then “Name was not set”.