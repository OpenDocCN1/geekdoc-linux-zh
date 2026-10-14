In that code, if the condition is true, statements 1 and 2 execute; otherwise, statement 3 runs. Either or both parts can be compound statement blocks:

```
if (condition) {
    statement1;
    statement2;
} else {
    statement3;
    statement4;
}
```

In that code, statements 1 and 2 execute if the condition is true; otherwise, statements 3 and 4 do their stuff. The placement of the braces is up to you. Some programmers prefer them on separate lines as follows:

```
}
else
{
```

# NESTED if-else STATEMENTS

You may nest multiple if-else statements together, creating a multiway decision maker.

The following shows the basic outline for a nested if-else statement:

```
if (condition1)
    statement1;
else if (condition2)
    statement2;
else
    statement3;
```

Take that a line at a time, and be sure to understand how it works. If condition1 is true, then statement1 executes; otherwise, if condition2 is true, statement2 runs. If both condition1 and condition2 are false, statement3 executes. At least one of the three statements is guaranteed to execute. You can carry this idea to extremes, writing code such as this:

```
if (condition1)
    statement1;
else if (condition2)
    statement2;
else if (condition3)
    statement3;
else if (conditionN)
    statementN;
else    // Optional
    defaultStatement; // Optional
```