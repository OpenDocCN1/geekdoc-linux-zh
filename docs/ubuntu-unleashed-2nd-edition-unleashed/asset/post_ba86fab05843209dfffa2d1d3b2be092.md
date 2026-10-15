
The next function is `preg_match_all()`, which gives you an array of all the matches it found. However, to be most useful, it takes the array to fill with matches as a by-reference parameter and saves its return value for the number of matches that were found.

We suggest you use `preg_match_all()` and `var_dump()` to get a feel for how the function works. This example is a good place to start:

```
```php
<?php
    $string = "This is the best test in the west";
    $result = preg_match_all("/[A-Za-z]est/", $string, $matches);
    var_dump($matches);
?>
```
```

That outputs the following:

```
```text
array(1) {
  [0]=>
  array(3) {
    [0]=>
    string(4) "best"
    [1]=>
    string(4) "test"
    [2]=>
    string(4) "west"
  }
}
```
```

If you notice, the $matches array is actually multidimensional in that it contains one element, which itself is an array containing all the matches to our regular expression. The reason for this is because our expression has no *subexpressions*, meaning no independent matches using parentheses. If we had subexpressions, each would have its own element in the $matches array containing its own array of matches.

Moving on, `preg_replace()` is used to change all substrings that match a regular expression into something else. The basic manner of using this is quite easy: You search for something with a regular expression and provide a replacement for it. However, a more useful variant is *backreferencing*, using the match as part of the replacement. For our example, we will imagine you have written a tutorial on PHP but want to process the text so each reference to a function is followed by a link to the PHP manual.

PHP manual page URLs take the form http://www.php.net/<function>—for example, http://www.php.net/preg_replace. The string we need to match is a function name, which is a string of alphabetic characters, potentially also mixed with numbers and underscores and terminated with two parentheses, (). As a replacement, we will use the match we found, surrounded in HTML emphasis tags (<em></em>), and then with a link to the relevant PHP manual page. Here is how that looks in code:

```
<?php
$regex = ".*/([A-Za-z0-9_]*)(\()/";
$replace = "<em>$1</em> (<a href=\"http://www.php.net/$1\" >manual</a>)";
$haystack = "File_get_contents() is easier than using fopen().";
$result = preg_replace($regex, $replace, $haystack);
echo $result;
?>
```

The $1 is our backreference; it will be substituted with the results from the first subexpression. The way we have written the regular expression is very exact. The [A-Za-z0-9_]* part, which matches the function name, is marked as a subexpression. After that is \(\), which means the exact symbols (and), not the regular expression meanings of them, which means that $1 in the replacement will contain fopen rather than fopen(), which is how it should be. Of course, anything that is not backreferenced in the replacement is removed, so we have to put the () after the first $1 (not in the hyperlink) to repair the function name.

After all that work, the output is perfect:

```
<em>File_get_contents()</em> (<a href="http://www.php.net/file_get_contents">manual</a>) is easier than using <em>fopen()</em> (<a href="http://www.php.net/fopen">manual</a>).
```

## Handling HTML Forms

Given that PHP's primary role is handling web pages, you might wonder why this section has been left so late in the chapter. It is because handling HTML forms is so central to PHP that it is essentially automatic.

Consider this form:

```
<form method="POST" action="thispage.php">
User ID: <input type="text" name="UserID" /> <br />
Password: <input type="password" name="Password" /> <br />
<input type="submit" />
</form>
```

When a visitor clicks Submit, thispage.php is called again and this time PHP has the variables available to it inside the $_REQUEST array. Given that script, if the user enters 12345 and frosties as her user ID and password, PHP provides you with $_REQUEST['UserID'] set to 12345 and $_REQUEST['Password'] set to frosties. Note that it is important that you use HTTP post unless you specifically want GET. POST enables you to send a great deal more data and stops people from tampering with your URL to try to find holes in your script.
