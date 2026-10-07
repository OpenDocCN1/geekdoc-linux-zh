# 280 Lab 6.1: Typed Variables and Scope

However, if you put a dollar sign in front of the variable name to the left of the equal sign, you will get an error message from the shell telling you "assignment requires lvalue" because the shell will try to use the value of i as the name of the variable to receive the assignment. An "lvalue" is something that makes sense to put on the left side of an equal sign, so it has to be the name of a variable.

![](bbox=[0.023, 0.087, 0.137, 0.149])

+   b) In the double parentheses command, do the j and k on the right side of the equal sign represent characters, or are they references to variables?

Answer:They are references to variables.

The shell doesn't require dollar signs in variable references in let and double parentheses commands because there is no ambiguity if you leave them out. Consider the following interaction:

```
meat=food
((potatoes=food))
print meat=$meat potatoes=$potatoes
meat= potatoes=0
```

Even neither meat nor potatoes is declared to be a numeric variable, the second assignment gives the value zero to potatoes because it is done in the context of an arithmetic expression. The first command interprets food as a value to be assigned to meat in the usual way, but you can't use the letters f-o-o-d as a number, the shell interprets food as the name of a variable. Assuming that you haven't assigned any value to the variable named food, the shell quietly uses the value zero.

+   c) In both the let and the double parentheses commands, what arithmetic operation is being performed?

Answer:In both cases, the values of two variables are being added together.

If you have never written a computer program before, the statements may look like illogical equations; it would not make sense to say that something is equivalent to itself else (unless, perhaps something else is "nothing"). However, if you recognize the equal sign as the symbol for assignment, it should be clear that the two commands replace the current value of the variable on the left side of the equal sign