The last line uses modulus, which for some people takes a little bit of effort to understand. The result of $1 % 11 is 0 because $1 is set to 55 and modulus works by dividing the left operand (55) by the right operand (11) and returning the remainder. 55 divides by 11 exactly five times, and so has the remainder 0.

The concatenation operator, a period, sounds scarier than it is: It just joins strings together. For example:

```
```php
<?php
echo 'Hello, ' . 'world!';
echo 'Hello, world!' . "\n";
?>
```
```

There are two “special” operators in PHP that are not covered here and yet are used frequently. Before we look at them, though, it’s important that you see how the comparison operators (such as <, <=, and !=) are used inside conditional statements.

# Conditional Statements

In a conditional statement you instruct PHP to take different actions depending on the outcome of a test. For example, you might want PHP to check whether a variable is greater than 10 and, if so, print a message. This is all done with the if statement, which looks like this:

```
```text
if (your condition) {
    // action to take if condition is true
} else {
    // optional action to take otherwise
}
```
```

The your condition part can be filled with any number of conditions you want PHP to evaluate, and this is where the comparison operators come into their own. For example:

```
```php
if ($i > 10) {
    echo "11 or higher";
} else {
    echo "10 or lower";
}
```
```

PHP looks at the condition and compares $i to 10. If it is greater than 10, it replaces the whole operation with 1; otherwise, it replaces it with 0. So, if $i is 20, the result looks like this:

```
```php
if (1) {
    echo "11 or higher";
} else {
    echo "10 or lower";
}
```
```