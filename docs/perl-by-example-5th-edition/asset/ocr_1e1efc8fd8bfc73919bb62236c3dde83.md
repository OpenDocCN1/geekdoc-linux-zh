# EXPLANATION

+   A list of lowercase letters is assigned to array @alpha.
+   Each item in the list is aliased to $ _ and printed, one at a time, until there are no more items in the list. Could also say: print for @alpha;

# 7.4.3 Loop Control

To interrupt the normal flow of control within a loop, Perl provides labels and simple control statements. These statements are used for controlling a loop when some condition is reached; that is, the control is transferred directly to either the bottom or the top of the loop, skipping any statements that follow the control statement condition.

Labels.   Labels are optional but you can use them to control the flow of a loop. (Note that you can attach them to any statement, not just loops.) By themselves, labels do nothing. They are used with the loop control modifiers, listed next. A block by itself, whether or not it has a label, is equivalent to a loop that executes only once. If labels are capitalized, they will not be confused with reserved words.

# EXAMPLE 7.24

```
LABEL: while (Expression) {Block}
LABEL: while (Expression) {Block} continue{Block}
LABEL: for (Expression; Expression; Expression)
      {BLOCK}
LABEL: foreach Variable (Array) {Block}
LABEL: {Block} continue {Block}
```

To control the flow of loops, the following simple statements may be used within the block:

```
next next LABEL
last
last LABEL
redo
redo LABEL
goto LABEL
```

The next statement restarts the next iteration of the loop, skipping over the rest of the statements in the loop and reevaluating the loop expression, like a C, awk, or shell continue statement. Since a block is a loop that iterates once, you can use next (with a continue block, if provided) to exit the block early.

The last statement leaves or breaks out of a loop and is like the break statement in C, awk, and shell. Since a block is a loop that iterates once, you can use last to break out of a block.

The redo statement restarts the block without evaluating the loop expression again.