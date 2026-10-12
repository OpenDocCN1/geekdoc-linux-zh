The break statement can be used to terminate an iteration loop, such as a for, until, or repeat command.

exit statements can be used to exit a shell program. You can optionally use a number after exit. If the current shell program has been called by another shell program, the calling program can check for the code (the $? or $status variable, depending on the shell) and make a decision accordingly.

# Using Functions in Shell Scripts

As with other programming languages, shell programs also support functions. A function is a piece of a shell program that performs a particular process; you can reuse the same function multiple times within the shell program. Functions help eliminate the need for duplicating code as you write shell programs.

The following is the format of a function in pdksh and bash:

```
func(){
    Statements
}
```

You can call a function as follows:

```
func param1 param2 param3
```

The parameters param1, param2, and so on are optional. You can also pass the parameters as a single string—for example, $@. A function can parse the parameters as if they were positional parameters passed to a shell program from the command line as command-line arguments, but instead use values passed inside the script. For example, the following script uses a function named Displaymonth() that displays the name of the month or an error message if you pass a month number out of the range 1 to 12. This example works with pdksh and bash:

```
#!/bin/sh
Displaymonth() {
    case $1 in
        01 | 1) echo "Month is January";;
        02 | 2) echo "Month is February";;
        03 | 3) echo "Month is March";;
        04 | 4) echo "Month is April";;
        05 | 5) echo "Month is May";;
        06 | 6) echo "Month is June";;
        07 | 7) echo "Month is July";;
        08 | 8) echo "Month is August";;
        09 | 9) echo "Month is September";;
        10) echo "Month is October";;
        11) echo "Month is November";;
        12) echo "Month is December";;
    esac
}
```

![](bbox=[0.88, 0.42, 0.96, 0.48])