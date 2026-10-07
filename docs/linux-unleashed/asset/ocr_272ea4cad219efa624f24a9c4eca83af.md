The second argument to the `if` command is a Tcl script, which can contain any number of Tcl commands. This script is executed if the expression contained in the first argument evaluates to True.

The `if` commands can have one or more `elseif` commands and one `else` command associated with them. The syntax for these commands is shown here:

```
if {expr} {
    commands
}
elif {expr} {
    commands
}
elif {expr} {
    commands
}
else {
    commands
}
```

The commands associated with the first `if` or `elseif` whose expression evaluates to True are executed. If none of these expressions evaluate to True, the commands associated with the `else` command are executed.

> **WARNING**

The open brace must occur on the same line as the word that precedes it. This is because new lines are treated as command separators. If you enter an `if` command where the `if {expr}` portion of the command appears on one line and the rest is on the next line, it is treated as two separate commands.

# The for Command

The `for` command in Tcl provides a way of implementing for loops. Tcl for loops are very similar to for loops in other languages, such as C. The `for` command expects four arguments. The first argument is a script that is used to initialize the counter. The second argument is an expression that is evaluated each time through the loop to determine whether to continue. The third argument is used to define the increment to be used on the counter. The fourth argument is the set of commands to be executed each time through the loop.

```
for { set i 0} {$i < 10} {incr I 1} {
    puts [expr 2 * $i]
}
```

The preceding loop executes ten times. The counter `i` is initially set to 0. The `for` loop executes while `i` is less than 10, and the value of `i` is increased by 1 each time through