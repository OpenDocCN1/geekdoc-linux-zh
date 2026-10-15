# LISTING 29.3 Continued

```
echo "Cat age is 4";
} else {
    echo "Cat age is unknown";
}
}
}
?>
```

Even though it certainly works, it is a poor solution to the problem. Much better is a switch/case block, which transforms the previous code into what’s shown in Listing 29.4.

# LISTING 29.4 Using a switch/case Block

```
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

Although it is only slightly shorter, it is a great deal more readable and much easier to maintain. A switch/case group is made up of a switch() statement in which you provide the variable you want to check, followed by numerous case statements. Notice the break statement at the end of each case. Without that, PHP would execute each case statement beneath the one it matches. Calling break causes PHP to exit the switch/case. Notice also that there is a default case at the end that catches everything that has no matching case.