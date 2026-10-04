# 4.2 Command Evaluation and Substitutions

brackets, the command processor will be called recursively until there are no further bracketed commands. When there are no more phrases to be substituted, the command is evaluated, and the result is passed to the pre-vious level of recursion to substitute for the bracketed string.

The next example shows how a command is evaluated. The recursion is shown by the indentation level.

Let's examine this command:

```
set x [expr [set a 3] + 4 + $a]
```

The command is scanned left to right for the first phrase to be substituted. The scanner encounters the left square bracket, and the command evaluator is reentered with that subset of the command.

```
expr [set a 3] + 4 + $a
```

This command is again scanned, and again there is a bracket, so the command evaluator is called again with that subset:

```
set a 3
```

There are no more levels of brackets and no substitutions to perform, so this command is evaluated, the variable a is set to the value 3, and 3 is returned.

The recursive call returned 3, so the bracketed command is replaced by 3, and the command now resembles this:

```
expr 3 + 4 + $a
```

The variables are now substituted, and $a is replaced by 3, making the new command:

```
expr 3 + 4 + 3
```

This is evaluated, and the result (10) is returned.

The substitution is performed, and the command is now:

```
set x 10
```

This is evaluated, the variable x is set to 10, and tclsh returns 10.