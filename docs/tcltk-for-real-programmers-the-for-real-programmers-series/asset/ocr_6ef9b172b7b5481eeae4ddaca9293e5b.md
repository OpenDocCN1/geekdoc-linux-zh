# 15.4 Coding Tips and Techniques

Use the interpreter to parse input.
Tcl is one of the very few languages that provides the script writer with access to a parse engine. This can save you time (and help you write more robust code) in several ways.

+   * Use procedures instead of switch statements to parse input.
If you are accustomed to C programming, you are used to constructs like this:
```cl
while {[gets stdin cmdLine]} {
    set cmd [lindex $cmdLine 0]
    switch $cmd {
        "cmd1" {cmd1Procedure $cmdLine}
        "cmd2" {cmd2Procedure $cmdLine}
    }
}
```

Whenever you add a new command using a switch statement, you need to add a new pattern to the switch command.
In Tcl, you can write a loop to parse input like this:
```cl
while {[gets stdin cmdLine]} {
    set cmd [lindex $cmdLine 0]
    set cmdName [format "%sprocedure" $cmd]
```

```
# Confirm that the command exists before trying to eval it.
if {[info command $cmdName] != ""} {
    eval $cmdName $cmdLine
}
```

When the requirements change and you need to add a new command, you simply add a new procedure without changing the command parsing code.

+   * Use the info command to match quotes, braces, and brackets.
The info complete command will return a 1 if a command is complete and a 0 if there are opening quotes, braces, or brackets without the appropriate closing quotes, braces, or brackets.