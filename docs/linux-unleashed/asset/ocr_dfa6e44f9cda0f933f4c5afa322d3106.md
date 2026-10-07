The `Tcl switch` command is equivalent to the `case` statement found in Pascal and some other languages. This `switch` command compares the value that is stored in the `thing` variable (which must be set prior to these statements, of course) with the string `car` and the string `truck` to see if it matches either of them. If the value of the `thing` variable is equal to `car`, then `thing is a car` is displayed on the screen. If the value of the `thing` variable is equal to `truck`, then `thing is a truck` is displayed on the screen. If neither of these cases is true, the `default` clause is executed and `I don't know what this thing is` displays on the screen.

> **TIP**

Whenever you need to check to see if a variable is equal to one of a number of values, use a `switch` command instead of an `if` command with multiple `elseif` clauses. This makes the code much easier to read and understand.

# Comments

It is always a good idea to include comments in any Tcl code you write—or code you write in any other language, for that matter. This becomes especially important if any of the following situations are possible:

+   - Someone else needs to look at or maintain your code.
- Your programs get large.
- You won't be looking at code that you have written for long periods of time after you write it.

Chances are that at least one of these situations will come up with Tcl code you have written.

Comments cannot be placed in the middle of a command. They must occur between commands. The pound sign (#) is used to inform Tcl to expect a comment.

```
```
# This is a valid comment

set a 1 ;  # This is a valid comment

set a 1    # This is an invalid comment
```
```

The third comment shown here is invalid because it occurs in the middle of a command. Remember that Tcl interprets everything up to a newline character or a semicolon to be part of the command.