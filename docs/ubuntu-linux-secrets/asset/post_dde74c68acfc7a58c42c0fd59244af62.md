
will produce the output:

My favorite fruit is a banana

Notice that when you use an associative array variable in the echo statement, you must enclose it with braces. This is different from numerical arrays, which don’t need the braces.

## Iterating Through Arrays

The tricky part of working with array and associative array variables is extracting all of the data they contain. If you use associative array variables, you may have no way of knowing what key values the array contains. Even if you use numeric array variables, there’s no guarantee that the key numbers are sequential (you can assign a value to $myarray[6] without assigning a value to $myarray[3], $myarray[4], or $myarray[5]).

Fortunately for us, the thoughtful programmers who developed PHP came up with a simple solution. The foreach statement iterates through an array, extracting every key/value pair defined within the array, one at a time.

There are a couple of ways to use the foreach statement with an array. The first method extracts only the value stored in the array, without regard to the key:

```
$myarray = array("state"=>"Illinois", "city"=>"Chicago", "zip"=>"60633");
foreach ($myarray as $value)
{
 echo "The value is $value<br>\n";
}
```

In this code snippet, the foreach statement loops through the $myarray array variable. Each value stored in the array is extracted as the variable $value and can be used anywhere within the foreach loop. Notice that the $value variable is a normal variable and can be used without the braces.

The second way to extract array values pulls the entire key/value pair:

```
$myarray = array("state"=>"Illinois", "city"=>"Chicago", "zip"=>"60633");
foreach ($myarray as $key => $value)
{
 echo "The $key value is $value<br>\n";
}
```

Now you have access to both the key and the data value within the array. Again, the $key and $value variables are normal variables you can use anywhere within the foreach loop to represent the key and data value.

## Structured Commands

The PHP programming language supports program flow control using structured commands. The most common methods are the if-then statements and various looping statements. This section discusses both of these structured command statements.

### if-then Statements

A standard if-then statement executes one or more statements based on evaluating a condition. If the condition is true, the statements are executed. This feature allows you to execute PHP code based on the results of a comparison, such as adding tax to a price only if the item is a luxury item. The basic format of the if-then statement in PHP is

```
if (condition)
{
    code block 1
} elseif {
    code block 2
} else {
    code block 3
}
```

The if-then statement contains the statements it controls within braces and the condition it evaluates within parentheses. The condition must be an expression that results in either a true or false Boolean value.

You can check for all sorts of conditions, such as whether a number is a specific value or within a range of values, or whether a string value is equal to specific text (for example, checking for database records that are marked as active).

Let's create a test file to demonstrate using the if-then statement. Follow these steps:

1. Open a text editor and enter this code:

```
<html>
<body>
<h1>Random number test</h1>
<?php
$value = rand(0, 100);
if ($value > 50) {
    echo "<h2>The value is big: $value</h2>\n";
} elseif ($value > 25) {
    echo "<h2>The value is medium: $value</h2>\n";
} else {
    echo "<h2>The value is small: $value</h2>\n";
}
?>
</body>
</html>
```

2. Save the file in the /var/www folder as a file called randomtest.php.

3. Open a browser window and go to the URL http://localhost/randomtest.php.

This script uses the rand() PHP function to generate a random integer value between 0 and 100, which it stores in the variable $value. The script then uses that variable in three separate if-then statements.

You can run the PHP script multiple times by clicking the reload button on your browser. Each time you reload the web page, the script generates a new random number, producing a different answer.
