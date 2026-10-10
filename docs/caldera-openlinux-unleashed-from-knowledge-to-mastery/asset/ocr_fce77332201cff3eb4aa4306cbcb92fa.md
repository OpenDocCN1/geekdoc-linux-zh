```
```
      default:
          printf("I dunno\n");
  }
```
```

Here's how it works:

+   - If x is 1, then one is printed and the switch statement ends because of the break statement.
+   - If x is 2, then two is printed. Execution falls through the next cases and three or four is also printed.
+   - If x is 3, execution falls through to the next case.
+   - If x is 4, three or four is printed and the switch statement ends.
+   - Otherwise, I dunno is printed.

# Warning

> If you do not terminate a group of statements in the switch body with break, execution falls through to the next case. This is occasionally desirable but should be avoided because it is confusing. If you do use fall-through execution, comment that fact prominently. Otherwise, later program maintainers may add cases to the switch body and destroy the fall-through structure.

A switch statement should, in general, have a default label. Otherwise, if the expression does not match any of the case labels, execution continues following the switch statement without any indication of a problem. The default label lets you catch possibilities that shouldn't happen.

# # The while Statement

The while statement looks like this:

```
while ( expr ) statement
```

It works like this: expr is evaluated as for the if statement. If the result is nonzero, the body statement is executed. This repeats until expr evaluates to zero.

Within the body, a continue statement prematurely terminates the execution of the body and restarts the while loop from the testing of expr. A break statement terminates the body and exits the while loop. Execution continues from the statement following the while loop.