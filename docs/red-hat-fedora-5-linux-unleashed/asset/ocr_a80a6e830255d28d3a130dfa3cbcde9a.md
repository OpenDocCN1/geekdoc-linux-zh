# Including Other Files

Unless you are restricting yourself to the simplest programming ventures, you will want to share code among your scripts at some point. The most basic need for this is to have a standard header and footer for your website, with only the body content changing. However, you might also find yourself with a small set of custom functions you use frequently, and it would be an incredibly bad move to simply copy and paste the functions into each of the scripts that use them.

The most common way to include other files is with the include keyword. Save this script as include1.php:

```
<?php
    for($i = 10; $i >= 0; $i -= 1) {
        include 'echo_i.php';
    }
?>
```

Then save this script as echo_i.php:

```
<?php
    echo $i;
?>
```

If you run include1.php, PHP loops from 10 to 0 and includes echo_i.php each time. For its part, echo_i.php just prints the value of $i, which is a crazy way of performing an otherwise simple operation, but it does demonstrate how included files share data. Note that the include keyword in include1.php is inside a PHP block, but we reopen PHP inside echo_i.php. This is important because PHP exits PHP mode for each new file, so you always have a consistent entry point.

# Basic Functions

PHP has a vast number of built-in functions that enable you to manipulate strings, connect to databases, and more. There is not room here to cover even 10% of the functions; for more detailed coverage of functions, check the “Reference” section at the end of this chapter.

# Strings

Several important functions are used for working with strings, and there are many less frequently used ones for which there is not enough space here. We are going to look at the most important here, ordered by difficulty—easiest first!

The easiest function is strlen(), which takes a string as its parameter and returns the number of characters in there, like this: