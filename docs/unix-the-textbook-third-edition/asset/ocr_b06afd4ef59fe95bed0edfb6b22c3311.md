```
while condition
do
  cmd1
  ...
  break
  ...
  cmdn
done
echo "..."
...
```

```
while condition
do
  cmd1
  ...
  continue
  ...
  cmdn
done
echo "..."
...
```

This iteration is over and there are no more iterations

This iteration is over; do the next iteration

# FIGURE 12.7 Semantics of the break and continue commands.

In the following in-chapter exercises, you will write shell scripts with loops by using the for, while, and until statements.

# EXERCISE 12.11

Write a shell script that takes a list of host names on your network as command line arguments and displays whether the hosts are up or down. Use the ping command to display the status of a host and the for statement to process all host names.

# EXERCISE 12.12

Rewrite the script in Exercise 12.11, using the while statement. Rewrite it again, using the until statement.

# 12.6.6 The case Statement

The case statement provides a mechanism for multiway branching similar to a nested if statement. However, the structure provided by the case statement is more readable. You would use the case statement when you can—that is, when you are testing a single variable able to several distinct patterns. You would not use it when you want to test more than one variable. The following is a brief description of the statement.

```
SYNTAX
case test-string in
pattern1)   command-list1
            ;;
pattern2)   command-list2
            ;;
...
patternN)   command-listN
            ;;
esac
```

Purpose: To implement multiway branching like a nested if