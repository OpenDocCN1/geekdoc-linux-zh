```
<?php
    echo "Hello, " . "world!";
    echo "Hello, world!" . "\n";
?>
```

There are two “special” operators in PHP that are not covered here and yet are used frequently. Before we look at them, though, it’s important that you see how the comparison operators (such as <, <=, and !=) are used inside conditional statements.

# ## Conditional Statements

In a *conditional statement* you instruct PHP to take different actions depending on the outcome of a test. For example, you might want PHP to check whether a variable is greater than 10 and, if so, print a message. This is all done with the *if* statement, which looks like this:

```
if (your condition) {
    // action to take if condition is true
} else {
    // optional action to take otherwise
}
```

The *your condition* part can be filled with any number of conditions you want PHP to evaluate, and this is where the comparison operators come into their own. For example:

```
if ($i > 10) {
    echo "11 or higher";
} else {
    echo "10 or lower";
}
```

PHP looks at the condition and compares $i to 10. If it is greater than 10, it replaces the whole operation with 1; otherwise, it replaces it with 0. So, if $i is 20, the result looks like this:

```
if (1) {
    echo "11 or higher";
} else {
    echo "10 or lower";
}
```

In conditional statements, any number other than 0 is considered to be equivalent to the Boolean value *true*, so *if* (1) always evaluates to *true*. There is a similar case for strings—if your string has any characters in, it evaluates to *true*, with empty strings evaluating to *false*. This is important because you can then use that 1 in another condition through && or || operators. For example, if you want to check whether $i is greater than 10 but less than 40, you could write this: