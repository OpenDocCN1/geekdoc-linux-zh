# # The repeat Statement

tcsh has an iteration statement that has no equivalent in pdksh or bash. This is the repeat statement. The repeat statement executes a single command a specified number of times. The syntax for the repeat statement is the following:

```
```text
repeat  count  command
```
```

The following is an example of the repeat statement. It takes a set of numbers as command-line options and prints that number of periods to the screen. This program acts as a very primitive graphing program.

```
```text
#
foreach num ($*)
    repeat $num echo -n "."
    echo ""
end
```
```

> **NOTE**
Any repeat statement can be rewritten as a while or for statement. The repeat syntax is just more convenient.

# # Functions

The shell languages enable you to define your own functions. These functions behave in much the same way as functions you define in C and other programming languages. The main advantage of using functions as opposed to writing all of your shell code in line is for organizational purposes. Code written using functions tends to be much easier to read and maintain and also tends to be smaller, because you can group common code into functions instead of putting it everywhere it is needed. The tcsh shell does not support functions.

The syntax for creating a function in bash and pdksh is the following:

```
```text
fname () {
    shell commands
}
```
```

pdksh also allows the following syntax:

```
```text
function fname {
    shell commands
}
```
```