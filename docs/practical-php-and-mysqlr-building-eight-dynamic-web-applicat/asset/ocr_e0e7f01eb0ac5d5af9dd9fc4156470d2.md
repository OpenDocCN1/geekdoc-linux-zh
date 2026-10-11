# PHP as a Simple Calculator

When you have the ability to create variables, you also have the ability to perform some simple mathematical calculations on them. For those of you who shudder at the thought of math, fear not; you will explore some of the common mathematical uses you will need in PHP.

To begin, create a new file called simplmath.php and add the following code:

```
```php
$cds = 50;
$tapes = 60;

$total = $cds + $tapes;

echo "You have " . $cds . " cds and " . $tapes . " tapes with " . $total . " items!";
```
```

In this example, you first created two variables, called $cds and $tapes, that have numbers stored in them. (If you are reading this book in 2020, tapes were items that stored music on them, a bit like your AstroDisks.) The sixth line of code then uses the + sign to add the $cds and $tapes variables together and stores the result in the $total variable. The final echo line then concatenates all of the variables into a single line that explains how many CDs and tapes there are and the total number of items available.

A number of symbols can be used when performing math. Some of the most common are covered in Table 2-1.

TABLE 2-1 Math Operators in PHP

| OPERATOR | DESCRIPTION | EXAMPLE |
| :--- | :--- | :--- |
| + | Addition | $total = $cds + $tapes; |
| - | Subtraction | $total = $cds - $tapes; |
| * | Multiplication | $total = $cds * $tapes; |
| / | Division | $total = $cds / $tapes; |

One of the great benefits of PHP has been its batteries-included approach to functionality. To help solve a range of problems, a number of facilities and functions are built right into PHP. For example, some numbers don’t divide easily. Imagine that you need to split a range of news stories across a number of different pages. To