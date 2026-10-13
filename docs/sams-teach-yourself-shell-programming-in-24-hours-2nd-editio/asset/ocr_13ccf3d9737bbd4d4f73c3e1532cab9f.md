# TABLE 17.3 Assignment Operators in awk

| Operator | Description |
|---|---|
| += | Add |
| -= | Subtract |
| *= | Multiply |
| /= | Divide |
| %= | Modulo (Remainder) |
| ^= | Exponentiation |

Using an assignment operator is shorthand for writing a numeric expression of the form: name=name operator num

Many programmers prefer using the assignment operators because they are slightly more concise than a regular numeric expression.

# The Special Patterns: BEGIN and END

In the previous example, the awk command

```
awk ' { x++ ; print x ; } ' $1
```

prints the value of x each time it is incremented. It would be much nicer if you could print the total number of empty lines. In order to accomplish this, you need to use the special patterns BEGIN and END.

Recall that the general syntax of a command in an awk script is

```
/pattern/ { actions }
```

Usually pattern is a regular expression, but you can also use two special patterns, BEGIN and END. Taking these patterns into account, the general form of an awk command is

```
awk '
BEGIN { actions }
/pattern/ { actions }
/pattern/ { actions }
END { actions }
' files
```

When the BEGIN pattern is specified, awk executes its actions before reading any input. When the END pattern is specified, awk executes its actions before it exits. When these patterns are given the execution of an awk, the script is as follows:

+   1. If a BEGIN pattern is present, it executes the actions it specifies.
+   2. Reads an input line and parses it into fields.