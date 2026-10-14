# Operator Description

| Operator | Description |
|---|---|
| -and | Match if the tests on both sides of the operator are true. This can be shortened to -a. Note that when no operator is present, -and is implied by default. |
| -or | Match if a test on either side of the operator is true. This can be shortened to -o. |
| -not | Match if the test following the operator is false. This can be abbreviated with an exclamation point (!). |
| ( ) | Group tests and operators together to form larger expressions. This is used to control the precedence of the logical evaluations. By default, find evaluates from left to right. It is often necessary to override the default evaluation order to obtain the desired result. Even if not needed, it is helpful sometimes to include the grouping characters to improve the readability of the command. Note that since the parentheses have special meaning to the shell, they must be quoted when using them on the command line to allow them to be passed as arguments to find. Usually the backslash character is used to escape them. |

With this list of operators in hand, let’s deconstruct our find command. When viewed from the uppermost level, we see that our tests are arranged as two groupings separated by an -or operator.

```
( expression 1 ) -or ( expression 2 )
```

This makes sense because we are searching for files with a certain set of permissions and for directories with a different set. If we are looking for both files and directories, why do we use -or instead of -and? As find scans through the files and directories, each one is evaluated to see whether it matches the specified tests. We want to know whether it is either a file with bad permissions or a directory with bad permissions. It can’t be both at the same time. So if we expand the grouped expressions, we can see it this way: