The `elif` statement is an abbreviation of `else if`. This statement is executed only if none of the expressions associated with the `if` statement or any `elif` statements before it were true. The commands associated with the `else` statement are executed only if none of the expressions associated with the `if` statement or any of the `elif` statements were true.

In `tsh`, the `if` statement has two different forms. The first form provides the same function as the `bash` and `pdksb if` statement. This form of `if` statement has the following syntax:

```
```
if (expression1) then
commands
else if (expression2) then
commands
else
commands
endif
```
```

The second form of `if` statement provided by `tsh` is a simple version of the first `if` statement. This form of `if` statement evaluates only a single expression. If the expression is true, it executes a single command; if the expression is false, nothing happens. The syntax for this form of `if` statement is the following:

```
```
if (expression) command
```
```

This statement can be written using the first form of `if` statement by writing the `if` without any `else` or `else if` clauses. This form just saves a little typing.

The following is an example of a `bash` or `pdksb if` statement. This statement checks to see whether there is a `.profile` file in the current directory:

```
```
if [ -f .profile ]
then
    echo "There is a .profile file in the current directory."
else
    echo "Could not find the .profile file."
fi
```
```

The same statement written using the `tsh` syntax is shown here:

```
```
#
if ( { -f .profile } ) then
    echo "There is a .profile file in the current directory."
else
    echo "Could not find the .profile file."
endif
```
```