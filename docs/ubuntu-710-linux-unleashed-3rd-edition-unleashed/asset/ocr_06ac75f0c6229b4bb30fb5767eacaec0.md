Without explanation, that code is essentially meaningless; however, it expands into the following five lines of code:

```
if ($age < 18) {
$age_description = "child";
} else {
$age_description = "adult";
}
```

The ternary operator is so named because it has three operands: a condition to check ($age < 18 in the previous code), a result if the condition is true ("child"), and a result if the condition is false ("adult"). Although we hope you never have to use the ternary operator, it is at least important to know how it works in case you stumble across it.

The other special operator is the execution operator, which is the backtick symbol, `. The position of the backtick key varies depending on your keyboard, but it is likely to be just to the left of the 1 key (above Tab). The execution operator executes the program inside the back ticks, returning any text the program outputs. For example:

```
<?php
$! = `ls -l`;
echo $!;
?>
```

That executes the ls program, passing in -l (a lowercase L) to get the long format, and stores all its output in $!. You can make the command as long or as complex as you like, including piping to other programs. You can also use PHP variables inside the command.

# Switching

Having multiple if statements in one place is ugly, slow, and prone to errors. Consider the code in Listing 25.3.

LISTING 25.3 How Multiple Conditional Statements Lead to Ugly Code

```
<?php
$cat_age = 3;

if ($cat_age == 1) {
    echo "Cat age is 1";
} else {
    if ($cat_age == 2) {
        echo "Cat age is 2";
    } else {
        if ($cat_age == 3) {
            echo "Cat age is 3";
        } else {
            if ($cat_age == 4) {
```