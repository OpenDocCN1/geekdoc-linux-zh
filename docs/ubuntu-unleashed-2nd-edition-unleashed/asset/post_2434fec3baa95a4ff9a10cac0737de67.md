
Then save this script as echo_i.php:

```php
<?php
    echo $i;
?>
```

If you run include1.php, PHP loops from 10 to 0 and includes echo_i.php each time. For its part, echo_i.php just prints the value of $i, which is a crazy way of performing an otherwise simple operation, but it does demonstrate how included files share data. Note that the include keyword in include1.php is inside a PHP block, but we reopen PHP inside echo_i.php. This is important because PHP exits PHP mode for each new file, so you always have a consistent entry point.

## Basic Functions

PHP has a vast number of built-in functions that enable you to manipulate strings, connect to databases, and more. There is not room here to cover even 10% of the functions; for more detailed coverage of functions, check the "Reference" section at the end of this chapter.

## Strings

Several important functions are used for working with strings, and there are many more less frequently used ones for which there is not enough space here. We are going to look at the most important here, ordered by difficulty—easiest first!

The easiest function is strlen(), which takes a string as its parameter and returns the number of characters in there, like this:

```php
<?php
$ourstring = " The Quick Brown Box Jumped Over The Lazy Dog ";
echo strlen($ourstring);
?>
```

Keep in mind that trim() returns the trimmed string, so that outputs "The Quick Brown Box Jumped Over The Lazy Dog". We can modify that so trim() passes its return value to strlen() so that the code trims it and then outputs its trimmed length:

`echo strlen(trim($ourstring));`

PHP always executes the innermost functions first, so the previous code takes $ourstring, passes it through trim(), uses the return value of trim() as the parameter for strlen(), and prints it.

Of course, everyone knows that boxes do not jump over dogs—the usual phrase is "the quick brown fox." Fortunately, there is a function to fix that problem: str_replace(). Note that it has an underscore in it; PHP is inconsistent on this matter, so you really need to memorize the function name.

The str_replace() function takes three parameters: the text to search for, the text to replace it with, and the string you want to work with. When working with search functions, people often talk about needles and haystacks—in this situation, the first parameter is the needle (the thing to find), and the third parameter is the haystack (what you are searching through).

So, we can fix our error and correct box to fox with this code:

`echo str_replace("Box", "Fox", $ourstring);`

There are two little addendums to make here. First, note that we have specified "Box" as opposed to "box" because that is how it appears in the text. The str_replace() function is a case-sensitive function, which means it does not consider "Box" to be the same as "box". If you want to do a non-case-sensitive search and replace, you can use the str_ireplace() function, which works in the same way.

The second addendum is that, because we are actually changing only one character (B to F), we need not use a function at all. PHP enables you to read (and change) individual characters of a string by specifying the character position inside braces ({ and }). As with arrays, strings are zero based, which means in the $ourstring variable $ourstring{0} is T, $ourstring{1} is h, $ourstring{2} is e, and so on. We could use this instead of str_replace(), like this:

```php
<?php
$ourstring = "  The Quick Brown Box Jumped Over The Lazy Dog  ";
$ourstring{18} = "F";
echo $ourstring;
?>
```

You can extract part of a string using the substr() function, which takes a string as its first parameter, a start position as its second parameter, and an optional length as its third parameter. Optional parameters are common in PHP. If you do not provide them, PHP assumes a default value. In this case, if you specify only the first two parameters, PHP copies from the start position to the end of the string. If you specify the third parameter, PHP copies that many characters from the start. We can write a simple script to print "Lazy Dog" by setting the start position to 38, which, remembering that PHP starts counting string positions from 0, copies from the 39th character to the end of the string:

```php
echo substr($ourstring, 38);
```

If we just want to print the word "Lazy," we need to use the optional third parameter to specify the length as 4, like this:

```php
echo substr($ourstring, 38, 4);
```

The substr() function can also be used with negative second and third parameters. If you specify just parameter one and two and provide a negative number for parameter two, substr() counts backward from the end of the string. So, rather than specifying 38 for the second parameter, we can use -10, so it takes the last 10 characters from the string. Using a negative second parameter and positive third parameter counts backward from the end string and then uses a forward length. We can print "Lazy" by counting 10 characters back from the end and then taking the next four characters forward:

```php
echo substr($ourstring, -10, 4);
```

Finally, we can use a negative third parameter, too, which also counts back from the end of the string. For example, using "-4" as the third parameter means to take everything except the last four characters. Confused yet? This code example should make it clear:

```php
echo substr($ourstring, -19, -11);
```

That counts 19 characters backward from the end of the string (which places it at the 0 in Over) and then copies everything from there until 11 characters before the end of the string. That prints "Over the". The same thing could be written using -19 and 8, or even 29 and 8—there is more than one way to do it!

Moving on, the strpos() function returns the position of a particular substring inside a string; however, it is most commonly used to answer the question, "Does this string contain a specific substring?" You need to pass it two parameters: a haystack and a needle (yes, that's a different order from str_replace()!).

In its most basic use, strpos() can find the first instance of "Box" in our phrase, like this:

```php
echo strpos($ourstring, "Box");
```

This outputs 18 because that is where the B in Box starts. If strpos() cannot find the substring in the parent string, it returns false rather than the position. Much more helpful, though, is the ability to check whether a string contains a substring; a first attempt to check whether our string contains the word The might look like this:
