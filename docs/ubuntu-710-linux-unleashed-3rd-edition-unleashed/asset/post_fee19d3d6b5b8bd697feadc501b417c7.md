
Then save this script as echo_i.php:

```
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

```
<?php
$ourstring = " The Quick Brown Box Jumped Over The Lazy Dog ";
echo strlen($ourstring);
?>
```

We will be using that same string in subsequent examples to save space. If you execute that script, it outputs 48 because 48 characters are in the string. Note the 2 spaces on either side of the text, which pad the 44-character phrase up to 48 characters.

We can fix that padding with the trim() function, which takes a string to trim and returns it with all the whitespace removed from either side. This is a commonly used function because all too often you encounter strings that have an extra new line at the end or a space at the beginning. This cleans it up perfectly.

Using trim(), we can turn our 48-character string into a 44-character string (the same thing, without the extra spaces), like this:

```
echo trim($ourstring);
```

Keep in mind that `trim()` returns the trimmed string, so that outputs "The Quick Brown Box Jumped Over The Lazy Dog". We can modify that so `trim()` passes its return value to `strlen()` so that the code trims it and then outputs its trimmed length:

```
echo strlen(trim($ourstring));
```

PHP always executes the innermost functions first, so the previous code takes $ourstring, passes it through `trim()`, uses the return value of `trim()` as the parameter for `strlen()`, and prints it.

Of course, everyone knows that boxes do not jump over dogs—the usual phrase is “the quick brown fox.” Fortunately, there is a function to fix that problem: `str_replace()`. Note that it has an underscore in it; PHP is inconsistent on this matter, so you really need to memorize the function name.

The `str_replace()` function takes three parameters: the text to search for, the text to replace it with, and the string you want to work with. When working with search functions, people often talk about *needles* and *haystacks*—in this situation, the first parameter is the needle (the thing to find), and the third parameter is the haystack (what you are searching through).

So, we can fix our error and correct *box* to *fox* with this code:

```
echo str_replace("Box", "Fox", $ourstring);
```

There are two little addendums to make here. First, note that we have specified "Box" as opposed to "box" because that is how it appears in the text. The `str_replace()` function is a *case-sensitive* function, which means it does not consider "Box" to be the same as "box". If you want to do a non-case-sensitive search and replace, you can use the `str_ireplace()` function, which works in the same way.

The second addendum is that, because we are actually changing only one character (B to F), we need not use a function at all. PHP enables you to read (and change) individual characters of a string by specifying the character position inside braces ({ and }). As with arrays, strings are zero based, which means in the string variable $ourstring[0] is T, $ourstring[1] is h, $ourstring[2] is e, and so on. We could use this instead of `str_replace()`, like this:

```
<?php
    $ourstring = " The Quick Brown Box Jumped Over The Lazy Dog ";
    $ourstring{18} = "F";
    echo $ourstring;
?>
```

You can extract part of a string using the `substr()` function, which takes a string as its first parameter, a start position as its second parameter, and an optional length as its third parameter. Optional parameters are common in PHP. If you do not provide them, PHP assumes a default value. In this case, if you specify only the first two parameters, PHP
