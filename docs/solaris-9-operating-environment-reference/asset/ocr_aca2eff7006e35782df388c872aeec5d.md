# 1516

-s Silence warning messages (not error) that are normally printed on the
diagnostic output.

-t Ignore all characters from the beginning of a line up to including
the Tab character for the purpose of detecting a control statement.
If a control statement is found, discard all characters up to
including the Tab.

vc recognizes the following version control statements.
:asg keyword=value

Assign values to keywords. An asg statement overrides the assignment
for the corresponding keyword on the vc command line and all previous
asg statements for that keyword. Keywords that are declared but are
not assigned values have null values.

:dcl keyword, ..., keyword
Declare keywords. All keywords must be declared.

:if condition
:end Skip lines of the standard input. If condition is true, copy all lines
between the statement and the matching statement to the
standard output. If conditionis false, discard all intervening lines,
including control statements. Note that intervening statements and
matching statements are recognized solely for the purpose of
maintaining the proper if-matching.

The syntax of a condition is:

```
cond ::= "not" <or>
or ::= <and> | <and> "||" <or>
and ::= <exp> | <exp> "&&" <and>
exp ::= "(" <or> ")" | "< <value> <op> <value>
op ::= "=" | "!=" | "<" | ">"
value ::= ARBITRARY ASCII string> | <numeric string>
```

The available operators and their meanings are:

+   = Equal.
!= Not equal.
& AND.
| OR.
> Greater than.
< Less than.
() Used for logical groupings.

You can use not only immediately after an if. When not is present, it inverts
t value of the entity.
> and < operate only on unsigned integer values (for example, : 012 > 12 is false).
All other operators take strings as arguments (for example, : 012 != 12 is true).