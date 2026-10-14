
Without explanation, that code is essentially meaningless; however, it expands into the following five lines of code:

```php
if ($age < 18) {
    $age_description = "child";
} else {
    $age_description = "adult";
}
```

The ternary operator is so named because it has three operands: a condition to check (`$age < 18` in the previous code), a result if the condition is true (`"child"`), and a result if the condition is false (`"adult"`). Although we hope you never have to use the ternary operator, it is at least important to know how it works in case you stumble across it.

The other special operator is the execution operator, which is the backtick symbol (`` ` ``). The position of the backtick key varies depending on your keyboard, but it is likely to be just to the left of the 1 key (above Tab). The execution operator executes the program inside the backticks, returning any text the program outputs. For example:

```php
<?php
$output = `ls -l`;
echo $output;
?>
```

That executes the ls program, passing in -l (a lowercase L) to get the long format, and stores all its output in `$output`. You can make the command as long or as complex as you like, including piping to other programs. You can also use PHP variables inside the command.

## Switching

Having multiple if statements in one place is ugly, slow, and prone to errors. Consider the code in Listing 25.3.

### LISTING 25.3 How Multiple Conditional Statements Lead to Ugly Code

```php
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
                echo "Cat age is 4";
            } else {
                echo "Cat age is unknown";
            }
        }
    }
}
?>
```

Even though it certainly works, it is a poor solution to the problem. Much better is a switch/case block, which transforms the previous code into what’s shown in Listing 25.4.

### LISTING 25.4 Using a switch/case Block

```php
<?php
    $cat_age = 3;

    switch ($cat_age) {
        case 1:
            echo "Cat age is 1";
            break;
        case 2:
            echo "Cat age is 2";
            break;
        case 3:
            echo "Cat age is 3";
            break;
        case 4:
            echo "Cat age is 4";
            break;
        default:
            echo "Cat age is unknown";
    }
?>
```

Although it is only slightly shorter, it is a great deal more readable and much easier to maintain. A `switch/case` group is made up of a `switch()` statement in which you provide the variable you want to check, followed by numerous case statements. Notice the `break` statement at the end of each case. Without that, PHP would execute each case statement beneath the one it matches. Calling `break` causes PHP to exit the switch/case. Notice also that there is a `default` case at the end that catches everything that has no matching case.

It is important that you do not use `case default:` but merely `default:`. Also, it is the last case label, so it has no need for a break statement because PHP exits the `switch`/`case` block there anyway.

## Loops

PHP has four ways you can execute a block of code multiple times: while, for, foreach, and do...while. Of the four, only do...while sees little use; the others are popular and you will certainly encounter them in other people's scripts.

The most basic loop is the while loop, which executes a block of code for as long as a given condition is true. So, we can write an infinite loop—a block of code that continues forever—with this PHP:

```php
<?php
    $i = 10;
    while ($i >= 10) {
        $i += 1;
        echo $i;
    }
?>
```

The loop block checks whether `$i` is greater than or equal to 10 and, if that condition is true, adds 1 to `$i` and prints it. Then it goes back to the loop condition again. Because `$i` starts at 10 and we only ever add numbers to it, that loop continues forever. With two small changes, we can make the loop count down from 10 to 0:

```php
<?php
    $i = 10;
    while ($i >= 0) {
        $i -= 1;
        echo $i;
    }
?>
```

So, this time we check whether `$i` is greater than or equal to 0 and subtract 1 from it with each loop iteration. while loops are typically used when you are unsure of how many times the code needs to loop because while keeps looping until an external factor stops it.

With a for loop, you specify precise limits on its operation by giving it a declaration, a condition, and an action. That is, you specify one or more variables that should be set when the loop first runs (the declaration), you set the circumstances that will cause the loop to terminate (the condition), and you tell PHP what it should change with each loop iteration (the action). That last part is what really sets a for loop apart from a while loop: You usually tell PHP to change the condition variable with each iteration.
