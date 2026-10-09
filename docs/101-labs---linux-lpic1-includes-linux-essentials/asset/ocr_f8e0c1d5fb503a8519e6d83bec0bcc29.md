# Task 3:

To understand single quotes, double quotes, and backquotes, enter the following:

```
hello="echo hello"

echo "$hello"

echo '$hello'

echo `$hello`
```

The output should be as follows:

```
echo hello
$hello
hello
```

Double quotes allow for variables to have their values referenced. Single quotes are always literal, while backquotes *execute* the command (including variable references) within those quotes.

# Notes:

In some cases, you will want to reference variables with the `$\{variable\}` syntax. This is equivalent to `$variable`, but the reasons for choosing one over the other are beyond the scope of this lab.

Backquotes also have an alternative syntax:

```
$(echo hello)
```

This syntax is generally preferred over backquotes. We only mention backquotes to distinguish them from single quotes and ensure the differences are clear.