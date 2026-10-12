The second addendum is that because we are actually changing only one character (B to F), we need not use a function at all. PHP enables you to read (and change) individual characters of a string by specifying the character position inside braces ( { and } ). As with arrays, strings are zero-based, which means in the $sourstring variable $sourstring(0) is T, $sourstring(1) is h e, $sourstring(2) is e, e, and so on. We could use this instead of str_replace(), like this:

```
<?php

sourstring = " The Quick Brown Box Jumped Over The Lazy Dog ";
$sourstring[19] = "F";

echo $sourstring;
?>
```

You can extract part of a string using the substr() function, which takes a string as its first parameter, a start position as its second parameter, and an optional length as its third parameter. Optional parameters are common in PHP. If you do not provide them, PHP assumes a default value. In this case, if you specify only the first two parameters, PHP copies from the start position to the end of the string. If you specify the third parameter, PHP copies that many characters from the start.

We can write a simple script to print "Lazy Dog " by setting the start position to 38, which, remembering that PHP starts counting string positions from 0, copies from the 39th character to the end of the string:

```
echo substr($sourstring, 38);
```

If we just want to print the word "Lazy", we need to use the optional third parameter to specify the length as 4, like this:

```
echo substr($sourstring, 38, 4);
```

The substr() function can also be used with negative second and third parameters. If you specify just parameter one and two and provide a negative number for parameter two, substr() counts backward from the end of the string. Rather than specifying 38 for the second parameter, we can use -10 so that it takes the last 10 characters from the string. Using a negative second parameter and positive third parameter counts backward from the end string and then uses a forward length. We can print "Lazy" by counting 10 characters back from the end and then taking the next four characters forward:

```
echo substr($sourstring, -10, 4);
```

Finally, we can use a negative third parameter, too, which also counts back from the end of the string. For example, using "-4" as the third parameter means to take everything except the last four characters. Confused yet? This code example should make it clear:

```
echo substr($sourstring, -19, -11);
```