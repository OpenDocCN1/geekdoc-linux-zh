# LISTING 27.4 Continued

```
```PHP
    case 4:
        echo “Cat age is 4”;
        break;
    default:
        echo “Cat age is unknown”;
}
?>
```
```

Although it is only slightly shorter, it is a great deal more readable and much easier to maintain. A switch/case group is made up of a switch ( ) statement in which you provide the variable you want to check, followed by numerous case statements. Notice the break statement at the end of each case. Without that, PHP would execute each case statement beneath the one it matches. Calling break causes PHP to exit the switch/case. Notice also that there is a default case at the end that catches everything that has no matching case.

It is important that you do not use case default:: but merely default::. Also, it is the last case label, so it has no need for a break statement because PHP exits the switch/case block there anyway.

# Loops

PHP has four ways you can execute a block of code multiple times: while, for, foreach, and do…while. Of the four, only do…while sees little use; the others are popular and you will certainly encounter them in other people’s scripts.

The most basic loop is the while loop, which executes a block of code for as long as a given condition is true. So you can write an infinite loop—a block of code that continues forever—with this PHP:

```
```PHP
<?php
$ i = 10;
while ($i >= 10) {
$i += 1;
echo $i;
}
?>
```
```

The loop block checks whether $i is greater or equal to 10 and, if that condition is true, adds 1 to $i and prints it. Then it goes back to the loop condition again. Because $i starts at 10 and only numbers are added to it, that loop continues forever. With two small changes, you can make the loop count down from 10 to 0:

```
```PHP
<?php
$i = 10;
while ($i >= 0) {
```
```